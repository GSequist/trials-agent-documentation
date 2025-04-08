### Bearer Token Authentication

The trials-agent API supports authentication via Azure Active Directory OAuth 2.0 flow, providing secure access using bearer tokens.

#### Authentication Flow

1. **Initiate Login**: Direct users to the Azure login endpoint to begin authentication

**GET** /azure-login

{
  "login_url": "https://login.microsoftonline.com/..."
}

2. **Complete Authentication**: After successful Azure authentication, the user is redirected to the callback URL

**GET** /azure-callback

3. Upon successful authentication, the endpoint returns:

{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "bearer",
  "email": "user@example.com"
}

4. **Using token**: Using the Token: Include the token in subsequent API requests using the Authorization header

Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...

**Example API Request with Bearer Token**

import requests

# Store the token received from /azure-callback
token = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."

# Use the token in subsequent API calls
headers = {
    "Authorization": f"Bearer {token}",
    "Content-Type": "application/json"
}

response = requests.get(
    "https://api.trials-agent.example.com/conversations",
    headers=headers
)

data = response.json()