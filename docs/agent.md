The agentic architecture enables long-running tasks performing research for user.

### Streaming

The agent processes queries and streams responses in three types of chunks:

- **Text chunks**: Regular conversational text
- **Tool calls**: Notifications when the agent needs to use a tool
- **Tool results**: Data returned from tool execution

This allows for real-time visibility into the agent's reasoning process.

### Multi-Agent Capabilities

The system can dynamically invoke specialized agents for different tasks:

- **Research Agent**: Searches for information using search tools
- **Data Analysis Agent**: Processes structured data from files
- **Code Execution Agent**: Runs and tests code snippets

### Tool Integration

The agent can use various tools:

- **Search**: Web search capabilities
- **Calculator**: Mathematical operations
- **File Analysis**: Extracts information from user files
- **Code Execution**: Runs Python code in a sandboxed environment
- **Image Analysis**: Processes and extracts information from images

### Example Tool Call Flow

User asks: *"What's in this image and how does it relate to the stock market data from my CSV?"*

- Agent streams: (text) "I'll analyze your image and CSV file..."
- Agent streams: (tool_call) `{"tool_name": "image_analyzer", "args": {"image_path": "user_image.jpg"}}`
- Agent streams: (tool_result) `{"description": "Graph showing stock price trends"}`
- Agent streams: (tool_call) `{"tool_name": "csv_analyzer", "args": {"file_path": "stocks.csv"}}`
- Agent streams: (tool_result) `{"data": {"trends": [...], "summary": "..."}}`
- Agent streams: (text) "The image shows... which correlates with your data..."

### Advanced Visualization Tools

Document Generator
The agent can create beautifully formatted academic documents with rich formatting:

Purpose: Creates publication-ready documents with Markdown formatting, LaTeX math expressions, and embedded figures
Content Support: Headers, emphasis, code blocks, math expressions, tables, task lists
Figure Integration: Can embed images from the workspace with captions
When Used: For comprehensive reports, analysis summaries, or research papers

```json
{
  "text": "# Analysis Report\n\nThe data shows a **significant correlation** between variables.\n\n## Mathematical Model\n\n$$y = mx + b$$\n\nWhere $m=2.3$ and $b=0.7$",
  "figures": [
    {
      "path": "correlation_graph.png",
      "caption": "Figure 1: Correlation between variables X and Y"
    }
  ]
}
```

### Live Chart

The agent can generate interactive charts for data visualization:

Chart Types: Line, bar, and radar charts
Customization: Titles, labels, colors, and dataset configuration
Real-time Rendering: Charts appear directly in the conversation
When Used: For data analysis, trend visualization, or comparative studies

```json
{
  "type": "bar",
  "title": "Monthly Revenue Growth",
  "data": {
    "labels": ["Jan", "Feb", "Mar", "Apr"],
    "datasets": [
      {
        "label": "2024",
        "data": [65, 59, 80, 81],
        "backgroundColor": "rgba(75, 192, 192, 0.2)"
      },
      {
        "label": "2023",
        "data": [45, 55, 65, 70],
        "backgroundColor": "rgba(153, 102, 255, 0.2)"
      }
    ]
  }
}
```