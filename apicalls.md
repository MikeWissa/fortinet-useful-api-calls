## Get IP addresses lists corresponding to a group name
curl -sk -X GET "https://firewallIP/api/v2/cmdb/firewall/addrgrp/groupname" -H "Authorization: Bearer apikeyhere" --compressed | jq -r '.results[0].member[].q_origin_key'

## GET IP addresses corresponding to a ZTNA tag
curl -sk -X GET "https://ip-address/api/v2/monitor/firewall/address-dynamic?mkey=EMS1_ZTNA_tag_name&vdom=root" -H "Authorization: Bearer yourtokenhere" --compressed |  jq -r '.results.EMS1_ZTNA_tag_name.addrs[]'

**replace yourtokenhere with your api key**

**replace tag_name with the tag name you want to identify corresonding IP addresses that belong to it**

## Get group address objects accommodating for fqdn, ipaddr, different types
curl -sk -X GET "https://firewallIP/api/v2/cmdb/firewall/addrgrp/TEST_GROUP" -H "Authorization: apitoken" --compressed | \\
jq -r '.results[0].member[].q_origin_key' | \
xargs -I{} bash -c 'if [[ "{}" =~ ^[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+$ ]]; then echo "{}"; else result=$(curl -sk -X GET "https://firewallIP/api/v2/cmdb/firewall/address/{}" -H "Authorization: Bearer token" --compressed); echo $result | jq -r ".results[0] | if .type == \"ipmask\" then .subnet | split(\"/\")[0] elif .type == \"fqdn\" then .fqdn else empty end"; fi'
