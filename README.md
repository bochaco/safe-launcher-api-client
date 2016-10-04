# SAFE Launcher API client

This project aims at providng a Postman collection for sending REST requests compatible with SAFE Launcher API delivered with SAFE Network TEST 9.


## Requests

The following is the list of API requests implemented in the Postman collection

- **Authorization:**
	- ***POST /auth***: to authorize the client app with the SAFE Launcher (see [Authorize app](https://api.safedev.org/auth/authorize-app.html) )
	- ***GET /auth***: to verify that the client app is currently authorized by SAFE Launcher (see [Validate app authorization](https://api.safedev.org/auth/validate-app-authorization.html) )
	- ***DELETE /auth***: to revoke the current authorized token (see [Revoke app](https://api.safedev.org/auth/revoke-app.html))
 
- **AppendableData:**
	- ***GET /appendableData/handle/:id***: to fetch an appendable data handle (e.g. [Fetch the appendable data handle](https://tutorials.safedev.org/email-app/send-an-email.html#fetch-the-appendable-data-handle))
	- ***GET /appendableData/encryptKey/:handleId***: to get the public encryption key (e.g. [Get the encryption key](https://tutorials.safedev.org/email-app/send-an-email.html#get-the-encryption-key))
	- ***PUT /appendableData/:handleId/:dataMapId***: to append data to an appendable data (e.g. [Append the email to the appendable data](https://tutorials.safedev.org/email-app/send-an-email.html#append-the-email-to-the-appendable-data))

- **ImmutableData:**
	- ***POST /immutableData***: to create an immutable data (e.g. [Save the email as immutable data](https://tutorials.safedev.org/email-app/send-an-email.html#save-the-email-as-immutable-data))
	- ***GET /immutableData/:dataMapId***: to read an immutable data. Note this can only be used if the immutable data encryption type is *SYMMETRIC*.


## Environment variables

A collection of environment variables is also available and needed by the requests in the Postman collection.

Some of the requests contain a pre-request script, post-request script (in the form of Postman "tests"), or both. 

These scripts are used to set/read values to/from the environment variables which are needed to manipulate dynamic data obtained during the interaction with the SAFE Launcher.
> E.g., the authorization token obtained when invoking the "POST /auth" API is then needed in the header of every subsequent request, therefore using environment variables is how this information is shared among different Postman requests.

The following is the list of the available requests in the Postman collection, with their corresponding description of the environment variables each makes use of:

#### Authorization
| Request		| pre-script | path | header | body | post-script |
| ----------------- | ------------ | ------ | --------- | ------ | -------------- |
| POST /auth 	| 	|	| 	| 	| **"token"** env variable is set with the authorization token received in the response body. |
| GET /auth	| 	|	| the **"token"** env variable is read to send the auth token. | 	| 	|
| DELETE /auth | 	|	| the **"token"** env variable is read to send the auth token. | 	| 	|

#### AppendableData
| Request		| pre-script | path | header | body | post-script |
| ----------------- | ------------ | ------ | --------- | ------ | -------------- |
| GET /appendableData/handle/:id	| the **"recipient-email-id"** env variable is read and its sha256 digest is calculated and stored in **"hash-email-id"** env variable.  | the **"hash-email-id"** env variable value is passed in the request path as the id. | the **"token"** env variable is read to send the auth token. | 	| the "appendable-data-handle" env variable is set with the value of the Handle-Id value obtained from the response header. |
| GET /appendableData/encryptKey/:handleId	| 	| the **"appendable-data-handle"** env variable value is passed in the request path as the handle id. | the **"token"** env variable is read to send the auth token. | 	| the **"appendable-encryption-key"** env variable is set with the value of the Handle-Id value obtained from the response header. |
| PUT /appendableData/:handleId/:dataMapId | 	| the **"appendable-data-handle"** and **"datamap-handle"** env variables values are passed in the request path as the handle id and data map id respectively. | the **"token"** env variable is read to send the auth token. | 	|  |

#### ImmutableData
| Request		| pre-script | path | header | body | post-script |
| ----------------- | ------------ | ------ | --------- | ------ | -------------- |
| POST /immutableData 	| the **"iso-time"** env variable is set with the current time. |	| the **"token"** env variable is read to send the auth token. Also the **"appendable-encryption-key"** env variable value is used as the encryption-key-handle header. | the **"iso-time"** env variable is used as a helper for the body content. | the **"datamap-handle"** env variable is set with the value of the Handle-Id value obtained from the response header. |
| GET /immutableData/:dataMapId 	| 	| the **"datamap-handle"** env variable value is passed in the request path as the data map id. | the **"token"** env variable is read to send the auth token. | 	|  |


## Sending an email

You can send an email in the SAFE network compatible with the SAFE Mail app provided in SAFE Network Test 9. This can be achieved by using the quests provided out of the box:

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
