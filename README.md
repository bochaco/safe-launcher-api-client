# SAFE Launcher API client

This project aims at providng a Postman collection for sending REST requests compatible with SAFE Launcher API.

## Requests

The following is the list of API requests implemented in the Postman collection.

- **Authorization:**
	- [Authorize app](https://api.safedev.org/auth/authorize-app.html)
	- [Validate app authorization](https://api.safedev.org/auth/validate-app-authorization.html)
	- [Revoke app](https://api.safedev.org/auth/revoke-app.html)
 
- **NFS API:**
	- [Create directory](https://api.safedev.org/nfs/directory/create-directory.html)
	- [Get directory](https://api.safedev.org/nfs/directory/get-directory.html)
	- [Update directory](https://api.safedev.org/nfs/directory/update-directory.html)
	- [Move directory](https://api.safedev.org/nfs/directory/move-directory.html)
	- [Delete directory](https://api.safedev.org/nfs/directory/delete-directory.html)
	- [Create file](https://api.safedev.org/nfs/file/create-file.html)
	- [Get file metadata](https://api.safedev.org/nfs/file/get-file-metadata.html)
	- [Get file](https://api.safedev.org/nfs/file/get-file.html)
	- [Update file metadata](https://api.safedev.org/nfs/file/update-file-metadata.html)
	- [Move file](https://api.safedev.org/nfs/file/move-file.html)
	- [Delete file](https://api.safedev.org/nfs/file/delete-file.html)
	
- **DNS API:**
	- [Create long name](https://api.safedev.org/dns/create-long-name.html)
	- [Create long name and service](https://api.safedev.org/dns/create-long-name-and-service.html)
	- [Add service](https://api.safedev.org/dns/add-service.html)
	- [List long names](https://api.safedev.org/dns/list-long-names.html)
	- [List services](https://api.safedev.org/dns/list-services.html)
	- [Get home directory](https://api.safedev.org/dns/get-home-directory.html)
	- [Get file](https://api.safedev.org/dns/get-file.html)
	- [Delete service](https://api.safedev.org/dns/delete-service.html)
	- [Delete long name](https://api.safedev.org/dns/delete-long-name.html)

## Environment variables

A collection of environment variables is also available and needed by the requests in the Postman collection.

Some of the requests contain a pre-request script, post-request script (in the form of Postman "tests"), or both. 

These scripts are used to set/read values to/from the environment variables which are needed to manipulate dynamic data obtained during the interaction with the SAFE Launcher.
> E.g., the authorization token obtained when invoking the "POST /auth" API is then needed in the header of every subsequent request, therefore using environment variables is how this information is shared among different Postman requests.
