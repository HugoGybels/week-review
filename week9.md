<style>
body {
  font-size: 14px !important;
  font-family: Inconsolata, Monaco, Consolas, 'Courier New', Courier !important;
  text-align: justify !important;
  text-justify: inter-word !important;
  line-height: 1.45;
  color: #3f3f3f;
}
h1 {
  font-size: 2.6em !important;
  font-family: inherit !important;
  font-weight: 300 !important;
  line-height: 1.1 !important;
  color: inherit !important;
  outline: none !important;
  text-decoration : none !important;
}
h2 {
  font-weight: 300 !important;
  line-height: 1.1 !important;
  color: inherit !important;
  font-size: 2.15em !important;
}
h3 {
  font-weight: 300 !important;
  line-height: 1.1 !important;
  color: inherit !important;
  font-size: 1.8em !important;
}
img {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.codeTitle {
  font-style: italic;
  line-height: 0%;
  font-size: 80%;
}
</style>
# OSISoft Internship - Week 9

Here is a quick summary of my ninth week.

## Where I was

After studying the different options I had last week, it turned out that my best chances seem to be using winHTTP with the GSoap plugin, but I will have to find new possibilities to configure this plugin.


## What I did

### Tracing the connection

First, I tried to trace the connection, using **fiddler** on both the ODEBC Client and the DASA and also regarding which connection attempt can I see in the **AF Logs**.

> Note: I use stateless connection so I only see the sessions corresponding to the authentication.

<div class="codeTitle">Request : </div>
```
Client :
  gSoap/2.8
Security :
  Authorization: Negociate
  Authorization Header (Negotiate) appears to contain a Kerberos ticket:
```
<div class="codeTitle">Answer : </div>
```
HTTP/1.1 401 Unauthorized :
  Cookies ? Login :
    WWW-Authenticate: Negotiate
    WWW-Authenticate: Basic realm=""
    connection: close
```

On the data access server, we can see one connection from the ODBC User that should be then forwarded. but the second one is "ANONYMOUS LOGON" and I think this may be the problem already :

![logon](img/logon.png)

Finally I have the same error as for the second hop on the DAS on the AF logs, so the connection is still forwarded even if it does not succeed.

#### Using WinHTTP


## What I have to do