# Accounts

To change your account, run this script in a bash shell,
setting the correct values for the four variables at the top:

```bash
OLD_PASSWORD=<insert old password here>
OLD_USERNAME=<insert old username here>
NEW_PASSWORD=<insert new password here>
NEW_USERNAME=<insert new username here>

curl -v -X PUT \
  -H "Origin: https://upowdb.xyz" \
  -d "{\"username\":\"${NEW_USERNAME}\",\"password\":\"${NEW_PASSWORD}\"}" \
  https://${OLD_USERNAME}:${OLD_PASSWORD}@api.upowdb.xyz/api/v1/account
```