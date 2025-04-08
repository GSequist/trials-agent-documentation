## Chat Functionality

### Send Message and Stream Response

**GET** `/api/chat/{conversation_id}`

**Query Parameters**:
- **message**: User's input message
- **images**: JSON array of image filenames to include (optional)

**Response**: Server-sent events stream with the following event types:

- **Text Chunks**: `data: {"type": "text", "content": "Partial response..."}`
- **Tool Calls**: `data: {"type": "tool_call", "tool_name": "search", "args": {"query": "example"}}`
- **Tool Results**: `data: {"type": "tool_result", "tool_name": "search", "result": {"data": "search results"}}`
- **End of Stream**: `data: [DONE]`

### Stop Stream

**POST** `/api/stop/{conversation_id}/{stream_id}`

Stops an active streaming response.

**Response**:
```json
{
  "status": "stopping"
}
```