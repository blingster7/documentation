# User Sync

## Overview
Buyers that want to sync their user IDs with TripleLift may use one of the following endpoints:

|Endpoint|Description|Parameters|
|--- |--- |--- |
|/xuid|This endpoint will store the members user ID. This ID will subsequently be available on bid requests to this member.|mid: Member ID of the partner buying inventory. This is the TripleLift member ID. You will be given a single member ID, so this will be static through all your calls. This must be a positive integer.xuid: Your external user ID for this user.dongle: A short code provided by TripleLift to ensure our partners don't accidentally override another's mappings. This will be constant for all your requests.|
|/getuid|This endpoint will return the TripleLift user ID for this particular request.|redir: The URL that the request should be redirected to. The user ID macro "$UID" will be replaced with that user's ID. This must be URL encoded.|

## Samples

**/xuid**
http://eb2.3lift.com/xuid?mid=tl_value_sample123&xuid=my_external_user_id&dongle=tl_value_sample456

**/getuid**
http://eb2.3lift.com/getuid?redir=http%3A%2F%2Fyoursite.com%2FtlUid%3D$UID%26abc%3D456

## Examples
There are 2 main things to consider – who stores the mapping (TL or partner) and who initiates the syncing (TL, partner, or both).

TripleLift initiates, TripleLift stores:
1. TL calls Partner's sync endpoint: http(s)://{partner-sync-endpoint}?redir=http://eb2.3lift.com/xuid?mid=tl_value_sample123&xuid=my_external_user_id&dongle=tl_value_sample456
2. Partner redirects (HTTP GET) back to TL sync endpoint while replacing the macro placeholder with the actual Partner user ID (http://eb2.3lift.com/xuid?mid=tl_value_sample123&xuid=partner_value_789&dongle=tl_value_sample456)
3. TL receives the HTTP redirect, extracts Partner user ID and records the mapping
