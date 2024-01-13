## Get IP addresses lists corresponding to a group name
curl -sk -X GET "https://firewallIP/api/v2/cmdb/firewall/addrgrp/groupname" -H "Authorization: Bearer apikeyhere" --compressed | jq -r '.results[0].member[].q_origin_key'
