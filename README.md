## Authentication Process
OAuth2 is the primary method for authenticating with the GitHub API. It ensures secure access without needing to share login credentials.

There are two main ways to authenticate using OAuth:


	•	Personal Access Tokens (PATs): These act as a password replacement and grant access to GitHub APIs based on the permissions given when creating the token.
 
	•	OAuth App Authorization: This is more commonly used for third-party applications that access the GitHub API on behalf of a user.


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

### Test Authentication in Postman
1. You can test various endpoints of your choice,
   For example:

   GET https://api.github.com/user

   Use Case:
   - You use this endpoint when you want to get the profile data of the user who is making API requests      after they’ve authenticated.

## Core Endpoints  
### 1. Get User Info
   
   -Endpoint: `GET /user`
   
   -Description: Retrieves information abou the authenticated user.
   
   -Request:
     
  ```bash
   curl -H "Authorization: Bearer YOUR_PERSONAL_ACCESS_TOKEN" https://api.github.com/user
  ```
     
   -Response:

  ```json
{
  "login": "octocat",
  "id": 1,
  "avatar_url": "https://github.com/images/error/octocat_happy.gif",
  "name": "The Octocat",
  "company": "GitHub",
  "email": "octocat@github.com"
  "location": "San Francisco",
  "email": "octocat@github.com",
  "public_repos": 2,
  "public_gists": 1,
  "followers": 20,
  "following": 0,
  "created_at": "2008-01-14T04:33:35Z",
  "updated_at": "2008-01-14T04:33:35Z"
}
```
  -Authentication: Requires a Bearer token (Personal Access Token or OAuth Token).

### 2. List Repositories

   -Endpoint: `GET /user/repos`

   -Description: Lists all repositories for the authenticated user.

   -Request:

   ```bash
    curl -H "Authorization: Bearer YOUR_PERSONAL_ACCESS_TOKEN" https://api.github.com/user/repos
  ```
   -Response: Returns an array of repositories, including the repository name, owner, and description.

### 3. Get Commits  

   -Endpoint: `GET /repos/{owner}/{repo}/commits`

   -Description: Retrieves a list of commits for the specified repository.

   -Request:

  ```bash
    curl -H "Authorization: Bearer YOUR_PERSONAL_ACCESS_TOKEN" https://api.github.com/repos/{owner}/{repo}/commits
  ```

   -Response: A list of commit details, including commit message, author, and date.

### 4. Create Issues

   -Endpoint: `POST /repos/{owner}/{repo}/issues`

   -Description: Creates a new issue in a repository.

   -Request:

   ```bash
    curl -X POST -H "Authorization: Bearer YOUR_PERSONAL_ACCESS_TOKEN" \
     -d '{"title":"Issue Title", "body":"Issue body description"}' \
     https://api.github.com/repos/{owner}/{repo}/issues
  ```
   -Response: Returns the details of the created issue.

  
 ## Error Handling

 When interacting with the GitHub API, users may encounter various errors. Below are the common errors and how to resolve them.
 
1. Common HTTP Status Codes

	•	401 Unauthorized: Missing or invalid token.

		Solution: Include a valid token in the request header.

	•	403 Forbidden: Lack of permission to access user data.

		Solution: Verify user permissions.

3. Error Handling for Core Endpoints

GET /user:

	•	401 Unauthorized: Missing or invalid token.
	•	Solution: Include a valid token in the request header.
	•	403 Forbidden: Lack of permission to access user data.
	•	Solution: Verify user permissions.

GET /user/repos:

	•	401 Unauthorized: Missing or invalid access token.
	•	Solution: Provide a valid token.
	•	404 Not Found: No repositories found or they are private.
	•	Solution: Confirm user’s repositories and access permissions.

GET /repos/{owner}/{repo}/commits:

	•	401 Unauthorized: No valid authentication provided.
	•	Solution: Ensure the correct token with the necessary scopes.
	•	404 Not Found: Repository does not exist or is private.
	•	Solution: Ensure the repository exists and is accessible.

POST /repos/{owner}/{repo}/issues:

	•	401 Unauthorized: Invalid or missing access token.
	•	Solution: Include a valid token.
	•	403 Forbidden: Lack of write permissions to the repository.
	•	Solution: Check that the authenticated user has write access.
	•	422 Unprocessable Entity: Missing required fields or invalid data.
	•	Solution: Ensure the required fields are provided and properly formatted.

 3. Rate Limiting

GitHub API enforces rate limits. Exceeding these limits will return a 403 Forbidden error.

	•	403 Forbidden (Rate Limit Exceeded):
	•	Solution: Check the response headers for X-RateLimit-Remaining and X-RateLimit-Reset. Wait until the rate limit resets before retrying the request.


    
     

  
   
