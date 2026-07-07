# Tests

## With JWT

```shell
USER_JWT=$(curl -L -X POST https://lemur-3.cloud-iam.com/auth/realms/localdemo/protocol/openid-connect/token -H "Content-Type: application/x-www-form-urlencoded" -d "client_id=bapi" -d "client_secret=$CLIENT_SECRET" -d "scope=openid" -d "username=e.ripley@mail.com" -d "password=$USER_PASS" -d "grant_type=password" | jq -r '.access_token')
curl https://bapi.localdemo.mageekbox.eu/anthropic/v1/messages \
    -H "anthropic-version: 2023-06-01" \
    -H "content-type: application/json" \
    -H "Authorization: Bearer $USER_JWT" \
    --data \
'{
    "model": "anthropic.claude-opus-4-7",
    "max_tokens": 1024,
    "messages": [
        {"role": "user", "content": "what fish has a pink flesh?"}
    ]
}'
```

```shell
USER_JWT=$(curl -L -X POST https://lemur-3.cloud-iam.com/auth/realms/localdemo/protocol/openid-connect/token -H "Content-Type: application/x-www-form-urlencoded" -d "client_id=bapi" -d "client_secret=$CLIENT_SECRET" -d "scope=openid" -d "username=e.ripley@mail.com" -d "password=$USER_PASS" -d "grant_type=password" | jq -r '.access_token')
curl https://bapi.localdemo.mageekbox.eu/anthropic/v1/messages \
    -H "anthropic-version: 2023-06-01" \
    -H "content-type: application/json" \
    -H "Authorization: Bearer $USER_JWT" \
    --data \
'{
    "model": "anthropic.claude-opus-4-7",
    "max_tokens": 1024,
    "messages": [
        {"role": "user", "content": "what is a go routine"}
    ]
}'
```


```shell
USER_JWT=$(curl -L -X POST https://lemur-3.cloud-iam.com/auth/realms/localdemo/protocol/openid-connect/token -H "Content-Type: application/x-www-form-urlencoded" -d "client_id=bapi" -d "client_secret=$CLIENT_SECRET" -d "scope=openid" -d "username=e.ripley@mail.com" -d "password=$USER_PASS" -d "grant_type=password" | jq -r '.access_token')
curl https://bapi.localdemo.mageekbox.eu/anthropic/v1/messages \
    -H "anthropic-version: 2023-06-01" \
    -H "content-type: application/json" \
    -H "Authorization: Bearer $USER_JWT" \
    --data \
'{
    "model": "anthropic.claude-opus-4-7",
    "max_tokens": 1024,
    "messages": [
        {"role": "user", "content": "what is a go struct"}
    ]
}'
```

```shell
USER_JWT=$(curl -L -X POST https://lemur-3.cloud-iam.com/auth/realms/localdemo/protocol/openid-connect/token -H "Content-Type: application/x-www-form-urlencoded" -d "client_id=bapi" -d "client_secret=$CLIENT_SECRET" -d "scope=openid" -d "username=a.ripley@mail.com" -d "password=$USER_PASS" -d "grant_type=password" | jq -r '.access_token')
curl https://bapi.localdemo.mageekbox.eu/anthropic/v1/messages \
    -H "anthropic-version: 2023-06-01" \
    -H "content-type: application/json" \
    -H "Authorization: Bearer $USER_JWT" \
    --data \
'{
    "model": "anthropic.claude-opus-4-7",
    "max_tokens": 1024,
    "messages": [
        {"role": "user", "content": "what is a go interface?"}
    ]
}'
```

```shell
USER_JWT=$(curl -L -X POST https://lemur-3.cloud-iam.com/auth/realms/localdemo/protocol/openid-connect/token -H "Content-Type: application/x-www-form-urlencoded" -d "client_id=bapi" -d "client_secret=$CLIENT_SECRET" -d "scope=openid" -d "username=a.ripley@mail.com" -d "password=$USER_PASS" -d "grant_type=password" | jq -r '.access_token')
curl https://bapi.localdemo.mageekbox.eu/anthropic/v1/messages \
    -H "anthropic-version: 2023-06-01" \
    -H "content-type: application/json" \
    -H "Authorization: Bearer $USER_JWT" \
    --data \
'{
    "model": "anthropic.claude-opus-4-7",
    "max_tokens": 1024,
    "messages": [
        {"role": "user", "content": "what is a go struct"}
    ]
}'
```

```shell
USER_JWT=$(curl -L -X POST https://lemur-3.cloud-iam.com/auth/realms/localdemo/protocol/openid-connect/token -H "Content-Type: application/x-www-form-urlencoded" -d "client_id=bapi" -d "client_secret=$CLIENT_SECRET" -d "scope=openid" -d "username=b.weiland@mail.com" -d "password=$USER_PASS" -d "grant_type=password" | jq -r '.access_token')
curl https://bapi.localdemo.mageekbox.eu/anthropic/v1/messages \
    -H "anthropic-version: 2023-06-01" \
    -H "content-type: application/json" \
    -H "Authorization: Bearer $USER_JWT" \
    --data \
'{
    "model": "anthropic.claude-haiku-4-5",
    "max_tokens": 1024,
    "messages": [
        {"role": "user", "content": "what is a go routine?"}
    ]
}'
```
