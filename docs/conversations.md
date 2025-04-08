## Conversation Management

### List Conversations

**GET** `/api/conversations/list`

Returns all conversations for a user.

**Response**:
```json
[
  {
    "id": 1,
    "name": "Conversation Name",
    "created_at": "2025-03-26T12:00:00"
  }
]
```

### Get Conversation Messages

**GET** `/api/conversations/{conversation_id}`

**Query Parameters**:
- **page**: Page number (default: 1)
- **pageSize**: Messages per page (default: 20)

**Response**:
```json
{
  "messages": [
    {
      "id": 1,
      "role": "user",
      "content": "Hello",
      "created_at": "2025-03-26T12:00:00"
    },
    {
      "id": 2,
      "role": "assistant",
      "content": "Hi there!",
      "created_at": "2025-03-26T12:00:01"
    }
  ],
  "totalPages": 1
}
```

### Create Conversation

**POST** `/api/conversations/`

**Request Body**:
```json
{
  "name": "New Conversation"
}
```

**Response**:
```json
{
  "id": 3,
  "name": "New Conversation",
  "created_at": "2025-03-26T12:30:00"
}
```

### Rename Conversation

**PUT** `/api/conversations/{conversation_id}`

**Request Body**:
```json
{
  "name": "Updated Name"
}
```

**Response**:
```json
{
  "success": true
}
```

### Delete Conversation

**DELETE** `/api/conversations/{conversation_id}`

**Response**:
```json
{
  "success": true
}
```
