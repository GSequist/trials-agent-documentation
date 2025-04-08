## File Management

Files are stored in user-specific directories and can be referenced in chat messages for analysis by the agent system.

### File Usage by Agent

Files uploaded through the API are used in multiple ways:

- **Image Analysis**: Images are base64 encoded and sent to the agent for visual processing
- **Document Processing**: The agent can access and analyze uploaded documents
- **File Reference**: Users can reference files in messages (e.g., "Please analyze data.csv")

### File Lifecycle

- Upload via `/upload/{user_id}`
- Reference in chat via the `images` parameter or message text
- Agent processes file content using appropriate tools
- File remains available for future conversations until deleted

### Upload File

**POST** `/api/files`

**Form Data**:
- **file**: File to upload (multipart/form-data)

**Response**:
```json
{
  "status": "success",
  "fileName": "example.txt"
}
```

**Error Response** (if file size limit exceeded):
```json
{
  "status": "error",
  "message": "file size exceeded"
}
```

### List Files

**GET** `/api/files`

**Response**:
```json
[
  "file1.txt",
  "image.jpg"
]
```

### Download File

**GET** `/api/files/{file_name}`

Returns the a pre-signed link as a file download.

### Delete File

**DELETE** `/api/files/{file_name}`

**Response**:
```json
{
  "success": true
}
```
