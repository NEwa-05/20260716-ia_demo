# Tests

## With JWT

### Exhaust OPUS user quota

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

### Check Haiku availability for the same user

```shell
USER_JWT=$(curl -L -X POST https://lemur-3.cloud-iam.com/auth/realms/localdemo/protocol/openid-connect/token -H "Content-Type: application/x-www-form-urlencoded" -d "client_id=bapi" -d "client_secret=$CLIENT_SECRET" -d "scope=openid" -d "username=e.ripley@mail.com" -d "password=$USER_PASS" -d "grant_type=password" | jq -r '.access_token')
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

### Check Opus availability for another user of the same team

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

### Exhaust team quota

```shell
USER_JWT=$(curl -L -X POST https://lemur-3.cloud-iam.com/auth/realms/localdemo/protocol/openid-connect/token -H "Content-Type: application/x-www-form-urlencoded" -d "client_id=bapi" -d "client_secret=$CLIENT_SECRET" -d "scope=openid" -d "username=a.ripley@mail.com" -d "password=$USER_PASS" -d "grant_type=password" | jq -r '.access_token')
curl https://bapi.localdemo.mageekbox.eu/anthropic/v1/messages \
    -H "anthropic-version: 2023-06-01" \
    -H "content-type: application/json" \
    -H "Authorization: Bearer $USER_JWT" \
    --data \
'{
    "model": "anthropic.claude-haiku-4-5",
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
    "model": "anthropic.claude-haiku-4-5",
    "max_tokens": 1024,
    "messages": [
        {"role": "user", "content": "what is a go struct"}
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
    "model": "anthropic.claude-haiku-4-5",
    "max_tokens": 1024,
    "messages": [
        {"role": "user", "content": "what is a go function, give me an example"}
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
    "model": "anthropic.claude-haiku-4-5",
    "max_tokens": 1024,
    "messages": [
        {"role": "user", "content": "is there a way to nested func in go, give me an example"}
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
    "model": "anthropic.claude-haiku-4-5",
    "max_tokens": 1024,
    "messages": [
        {"role": "user", "content": "is there a way to nested func in go, give me an example"}
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
    "model": "anthropic.claude-haiku-4-5",
    "max_tokens": 1024,
    "messages": [
        {"role": "user", "content": "what is a go function, give me an example"}
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
    "model": "anthropic.claude-haiku-4-5",
    "max_tokens": 1024,
    "messages": [
        {"role": "user", "content": "how can I use a go function within the said go function, give me an example"}
    ]
}'
```

### test another user/team quota

```shell
USER_JWT=$(curl -L -X POST https://lemur-3.cloud-iam.com/auth/realms/localdemo/protocol/openid-connect/token -H "Content-Type: application/x-www-form-urlencoded" -d "client_id=bapi" -d "client_secret=$CLIENT_SECRET" -d "scope=openid" -d "username=b.weiland@mail.com" -d "password=$USER_PASS" -d "grant_type=password" | jq -r '.access_token')
curl https://bapi.localdemo.mageekbox.eu/anthropic/v1/messages \
    -H "anthropic-version: 2023-06-01" \
    -H "content-type: application/json" \
    -H "Authorization: Bearer $USER_JWT" \
    --data \
'{
    "model": "anthropic.claude-opus-4-7",
    "max_tokens": 1024,
    "messages": [
        {"role": "user", "content": "how can I use a go function within the said go function, give me an example"}
    ]
}'
```

```shell
USER_JWT=$(curl -L -X POST https://lemur-3.cloud-iam.com/auth/realms/localdemo/protocol/openid-connect/token -H "Content-Type: application/x-www-form-urlencoded" -d "client_id=bapi" -d "client_secret=$CLIENT_SECRET" -d "scope=openid" -d "username=b.weiland@mail.com" -d "password=$USER_PASS" -d "grant_type=password" | jq -r '.access_token')
curl -v https://bapi.localdemo.mageekbox.eu/anthropic/v1/messages \
    -H "anthropic-version: 2023-06-01" \
    -H "content-type: application/json" \
    -H "Authorization: Bearer $USER_JWT" \
    --data \
'{
    "model": "anthropic.claude-haiku-4-5",
    "max_tokens": 1024,
    "messages": [
        {"role": "user", "content": "how can I use a go function within the said go function, give me an example"}
    ]
}'
```
