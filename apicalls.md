## Get IP addresses lists corresponding to a group name
curl -sk -X GET "https://firewallIP/api/v2/cmdb/firewall/addrgrp/groupname" -H "Authorization: Bearer apikeyhere" --compressed | jq -r '.results[0].member[].q_origin_key'

## GET IP addresses corresponding to a ZTNA tag
curl -k -X GET "https://ip-address/api/v2/monitor/firewall/address-dynamic?mkey=EMS1_ZTNA_tag_name&vdom=root" -H "Authorization: Bearer yourtokenhere" --compressed |  jq -r '.results.EMS1_ZTNA_tag_name.addrs[]'
** replace yourtokenhere with your api key
** replace tag_name with the tag name you want to identify corresonding IP addresses that belong to it
