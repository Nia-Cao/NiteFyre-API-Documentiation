# Authentication

This document outlines the NiteFyre API authentication endpoints.

Currently the API will return a 401 plus an error message if a login attempt or bearer token is invalid.

Example:
```
{
  "status": "invalid combination"
}
```

## /api/authentication/login

The login endpoint currently requires 2 values, "email" and "password". These values are sent to the endpoint as JSON in the request body.

Example:
```
{
  "email": "email",
  "password": "password"
}
```
Upon sucessful validation, the server will reply with a 'user object'.

Example:
```
{
	"username": "Niamh",
	"uuid": "niamh",
	"token": "{{JWT TOKEN}}",
	"email": "{{USER EMAIL}}",
	"discriminator": "0000",
	"systemFlairs": [
		"Owner",
		"Developer",
		"Royal Chungus"
	],
	"created": null,
	"avatarURL": "{{PROFILE IMG URL}}"
}
```

The UUID returned for most users will be in the standard UUID format, developers and certain user can have customised user ID's.

## /api/authentication/refreshuser

This endpoint takes the bearer token, checks for validity and if valid, returns a new copy of the 'user object'. This is useful for refreshing after profile data change.

## /api/authentication/newuser

This endpoint registers a new user on the API. To register a new user, use the same format as logging in.

Example:
```
{
  "email": "email",
  "password": "password"
}
```
The new user endpoint is currently very simple for testing, and performs little user validation. If registration is sucessful, a 'user object' will be returned.

Example:

```
{
	"username": "Niamh",
	"uuid": "niamh",
	"token": "{{JWT TOKEN}}",
	"email": "{{USER EMAIL}}",
	"discriminator": "0000",
	"systemFlairs": [
		"Owner",
		"Developer",
		"Royal Chungus"
	],
	"created": null,
	"avatarURL": "{{PROFILE IMG URL}}"
}
```

This is the same user object that is returned after a sucessful login. The API and services can be used as soon as a 'user object' is received.

If the email already exists the API will return a 401 plus a message.

Example:
```
{
  "status": "email exists"
}
```
### Things to note

Currently the users password for registration and login is in plain text format. If you are developing an application for the platform, you should make users aware that the API and your application are in development phases, and that they should follow good practice regarding unique passwords.

The API will be improved to require password hashing by the client, however for ease of Alpha stage testing, passwords can currently be sent in plain text.
