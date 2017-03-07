# ChatAPI-Curl
ChatAPI-Curl

The following are required to use the Chat API:

1) Login on the User Interface with Global Manager credentials.
2) Go to the Administration menu, then the Chat API Config screen
3) Enter the callback URL (where you would receive callback events).

----------------------------------------------------
Notice: the GLOBAL MANAGER can log-in any user without knowing their password.
The example below logs in agent bandre@syniverse using the Global Manager credentials. AGENT and PROPERTY MANAGER can log-in only themselves.
----------------------------------------------------

Successful registration (to receive events):

In the response there is session id - “58a64ba3e4b04a24a92da9e6” in the example below. This will be used in all messages on callback.

curl --request POST --header 'Content-Type: application/json' --user 'username@company-name:password' 'https://chat.syniverse.com/scg-web-chat-api/api/v2/integration/' --data '{"user":"username@company-name"}'
{
  "id" : "58a64ba3e4b04a24a92da9e6",
  "createdAt" : 1487303539483,
  "createdBy" : "syniverse@company-name",
  "expiresAt" : 1487505139676,
  "allowedTo" : {
    "id" : "573b2353e4b0c82f17c8b53e",
    "role" : "AGENT",
    "name" : "AGENT 007"
  }
}



If the Chat API is not enabled for your company:

curl --request POST --header 'Content-Type: application/json' --user 'username@company-name:password' 'https://chat.syniverse.com/scg-web-chat-api/api/v2/integration/' --data '{"user":"username@company-name"}'
{
  "timestamp" : 1487300502700,
  "status" : 409,
  "error" : "Conflict",
  "message" : "Integration is not enabled",
  "path" : "/scg-web-chat-api/api/v2/integration/"
}

If the user is not registered for the Chat API:

curl --request POST --header 'Content-Type: application/json' --user 'username@company-name:password' 'https://chat.syniverse.com/scg-web-chat-api/api/v2/integration/' --data '{"user":"username@company-name"}'
{
  "timestamp" : 1487300390036,
  "status" : 401,
  "error" : "Unauthorized",
  "message" : "Bad credentials",
  "path" : "/scg-web-chat-api/api/v2/integration/"
}


Successful Deregistration (to end a session):

Use the session id (“57f67f03e4b069fff308639b” in the example below) to deregister. This will log the user out and stop callbacks for that session.

curl --request DELETE --header 'Content-Type: application/json' --user 'username@company-name:password' 'http://twowaychat.com/scg-web-chat-api/api/v2/integration/57f67f03e4b069fff308639b'


