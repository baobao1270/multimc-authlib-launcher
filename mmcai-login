#!/bin/bash
SERVER_ENDPOINT=$1

if [ -z "$SERVER_ENDPOINT" ]; then
    echo "Usage: $0 <server-endpoint>"
    echo "Example: $0 https://example.yggdrasil.yushi.moe/api/yggdrasil"
    exit 1
fi

if [ $(uname) = "Linux" ]; then
    alias base64="base64 -w 0"
fi

echo "Using server endpoint: $SERVER_ENDPOINT"
echo "Waiting for server response..."
server_name=$(curl -s "$SERVER_ENDPOINT" | jq -r ".meta.serverName")
echo "Server name: $server_name"
echo "Note: when entering password, there is no echo on the screen."

read    -p "Username: " username
read -s -p "Password: " password

echo "Getting client token..."
client_token=$(dd if=/dev/urandom count=1 | base64 | cut -c1-128)

curl -s -X POST -H "Content-Type: application/json" "$SERVER_ENDPOINT/authserver/authenticate" -d "{\"username\": \"$username\", \"password\": \"$password\", \"requestUser\": true, \"clientToken\": \"$client_token\"}" > authlib-token.json
access_token=$(cat authlib-token.json | jq -r ".accessToken")
if [ -z "$access_token" ]; then
    echo "Failed to get access token."
    exit 1
fi

prefetch_data=$(curl -s "$SERVER_ENDPOINT" | base64)
echo "CLIENT_TOKEN=$client_token" > authlib.env
echo "SERVER_ADDRESS=$SERVER_ENDPOINT" >> authlib.env
echo "PREFETCH_DATA=$prefetch_data" >> authlib.env

echo "Login Success!"
