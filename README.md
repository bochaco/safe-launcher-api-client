# SAFE Launcher API client

TODO: Add explanations of how the requests work and how the environment variables are used for each of them. 
For the time being this is how it can be used:

1. Import the collection and the environment variables into Postman
2. Set the recipient's email id in the "recipient-email-id" environment variable
3. Execute the requests in the following order: 
  * POST /auth
  * GET /auth (optional: to verify it was authorized)
  * GET /appendableData/handle
  * GET /appendableData/encryptKey
  * POST /immutableData (edit the body beforehand, if you want to change the email's content. Note the time is calculated automatically)
  * GET /immutableData (optional: to verify the DataMap's content)
  * PUT /appendableData/handle
