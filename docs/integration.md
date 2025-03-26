## Client Integration

### Example: Processing Streamed Responses

```javascript
const eventSource = new EventSource(`/api/chat/${userId}/${conversationId}?message=${message}`);

eventSource.onmessage = (event) => {
  if (event.data === "[DONE]") {
    eventSource.close();
    return;
  }

  const data = JSON.parse(event.data);

  switch (data.type) {
    case "text":
      // Append text to UI
      break;
    case "tool_call":
      // Display tool being called
      break;
    case "tool_result":
      // Display tool results, possibly with visualization
      break;
  }
};

// To stop the stream
const stopStream = () => {
  fetch(`/api/stop/${userId}/${conversationId}/${streamId}`, {
    method: 'POST',
    headers: {
      'Authorization': `Bearer ${token}`
    }
  });
  eventSource.close();
};
```

### Handling Rich Visualization Outputs

When processing streamed responses, special handling is required for document_generator and live_chart tool results:

#### Document Generator

```javascript
case "tool_result":
  if (data.toolName === "document_generator") {
    const docData = data.result;
    
    // Create container for the document
    const docContainer = document.createElement('div');
    docContainer.className = 'formatted-document';
    
    // Render the markdown content
    const textContent = document.createElement('div');
    textContent.innerHTML = markdownToHtml(docData.text); // Use your preferred markdown renderer
    docContainer.appendChild(textContent);
    
    // Render figures if present
    if (docData.figures && docData.figures.length > 0) {
      const figuresContainer = document.createElement('div');
      figuresContainer.className = 'document-figures';
      
      docData.figures.forEach(figure => {
        const figureDiv = document.createElement('figure');
        
        // Create image element
        const img = document.createElement('img');
        img.src = figure.url || `/download/${userId}?file=${figure.path}`;
        img.alt = figure.caption;
        figureDiv.appendChild(img);
        
        // Create caption
        const caption = document.createElement('figcaption');
        caption.textContent = figure.caption;
        figureDiv.appendChild(caption);
        
        figuresContainer.appendChild(figureDiv);
      });
      
      docContainer.appendChild(figuresContainer);
    }
    
    messageContainer.appendChild(docContainer);
  }
  break;
```

#### Live Chart

Agent sometimes visualizes analyzed data streaming a live chart:

```javascript
case "tool_result":
  if (data.toolName === "live_chart") {
    const chartData = data.result;
    
    // Create canvas for chart
    const chartContainer = document.createElement('div');
    chartContainer.className = 'chart-container';
    
    const canvas = document.createElement('canvas');
    const chartId = `chart-${Date.now()}`;
    canvas.id = chartId;
    chartContainer.appendChild(canvas);
    
    messageContainer.appendChild(chartContainer);
    
    // Render chart using Chart.js or similar library
    const ctx = document.getElementById(chartId).getContext('2d');
    new Chart(ctx, {
      type: chartData.type,
      data: chartData.data,
      options: {
        responsive: true,
        plugins: {
          title: {
            display: true,
            text: chartData.title
          }
        }
      }
    });
  }
  break;
```