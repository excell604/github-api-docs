## Authentication Process
GitHub API requires OAuth2 or a Personal Access Token (PAT) to authenticate API requests. To access the API, you need to generate a token with the correct scopes and include it in your request headers.

### Steps to Generate a Personal Access Token (PAT)
1. Log in to your GitHub account.
2. Go to your **Profile** > **Settings**.
3. Under **Developer Settings**, click on **Personal Access Tokens**.
4. Click **Generate New Token**.
5. Select the appropriate scopes for your token, such as `repo`, `user`, and `gist`.
6. Click **Generate Token** and copy it.

N.B Remember to always store you token in a secure location and never share publicly.

### Example cURL Request for Authentication:
curl -H "Authorization: Bearer YOUR_PERSONAL_ACCESS_TOKEN" https://api.github.com/user

### How to Authenticate in Postman:
1. Open Postman.
2. In the Authorization tab, select **Bearer Token**.
3. Paste your Personal Access Token into the token field.
4. Send the request.
