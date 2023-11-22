
## Quickstart

#### Start docker container

```bash
make
```

----

## API calls

 - All API calls are in JSON.
 - Even error pages should adhere to this convention.
 - We use a loose JSON RPC protocol.

### User endpoints

 - These calls work for both borrowers and lenders

#### Authorization/Authentication endpoints

---
GET **/api/logout**
 - arguments: None
 - returns: {}

   - Erase the local session/auth cookie.
   - If logged in, deletes the cookie on the server as well so it can't be reused.

Curl:
```bash
curl -D- localhost:2777/api/logout
```

Result:
```bash
HTTP/1.1 200 OK
Date: Thu, 09 Nov 2023 19:40:00 GMT
Server: WSGIServer/0.2 CPython/3.10.12
Content-Type: application/json
X-Frame-Options: DENY
Content-Length: 2
Vary: Cookie
X-Content-Type-Options: nosniff
Referrer-Policy: same-origin
Cross-Origin-Opener-Policy: same-origin

{}
```

---
GET **/api/login**
 - arguments:
   - *username*: string

     Usually an email
     
   - *password*: string

     we'll digest this eventually/soon

  - returns either:
    - error on login failure
    - success.  you get the sessionid for informational purposes, but it isn't used anywhere.

On Failure:

    {"error": {"message": "login error"}}

On success:
Curl:
```bash
curl -D- localhost:2777/api/login\?username=admin\&password=adminx
```

Result:
```bash
HTTP/1.1 200 OK
Date: Thu, 09 Nov 2023 19:33:46 GMT
Server: WSGIServer/0.2 CPython/3.10.12
Content-Type: application/json
X-Frame-Options: DENY
Vary: Cookie
Content-Length: 61
X-Content-Type-Options: nosniff
Referrer-Policy: same-origin
Cross-Origin-Opener-Policy: same-origin
Set-Cookie:  csrftoken=rH75OwIqoUTcJ34Mti1uWBCxgU5Ws3fA; expires=Thu, 07 Nov 2024 19:33:46 GMT; Max-Age=31449600; Path=/; SameSite=Lax
Set-Cookie:  sessionid=ka0v3dr1tiuj8b7rp9d2mqllvwc9bypn; expires=Thu, 23 Nov 2023 19:33:46 GMT; HttpOnly; Max-Age=1209600; Path=/; SameSite=Lax

{"result": {"sessionid": "ka0v3dr1tiuj8b7rp9d2mqllvwc9bypn"}}
```

---
GET **/api/status**
 - arguments: None
 - returns: User authentication status and roles

On Failure:

Curl:
```
curl -D- localhost:2777/api/status
```

Result:
```bash
HTTP/1.1 200 OK
Date: Thu, 09 Nov 2023 19:40:04 GMT
Server: WSGIServer/0.2 CPython/3.10.12
Content-Type: application/json
X-Frame-Options: DENY
Content-Length: 51
Vary: Cookie
X-Content-Type-Options: nosniff
Referrer-Policy: same-origin
Cross-Origin-Opener-Policy: same-origin

{"response": {"authenticated": false, "roles": {}}}
```

On Success:

Curl:
```
curl -D- -HCookie:sessionid=gcdto7zt3f6v20ec8it2khqxuj6ho6br localhost:2777/api/status
```

Result:
```bash
HTTP/1.1 200 OK
Date: Thu, 09 Nov 2023 19:43:35 GMT
Server: WSGIServer/0.2 CPython/3.10.12
Content-Type: application/json
X-Frame-Options: DENY
Content-Length: 81
Vary: Cookie
X-Content-Type-Options: nosniff
Referrer-Policy: same-origin
Cross-Origin-Opener-Policy: same-origin

{"response": {"authenticated": true, "roles": {"founder": true, "lender": true}}}
```


#### Feature endpoints

---
GET /api/feature/list

---
GET /api/feature/set

---
GET /api/feature/clear

### Lender endpoints

#### Application lists

---
GET /api/applications/all

---
GET /api/applications/pending



----

## OLD STUFF

Frontend Quickstart
==

```bash
cd frontend/foresight
npm install
npm run dev
```
# foresight-reskin
# foresight-reskin
# foresight-reskin
# foresight-reskin
# foresight-reskin
