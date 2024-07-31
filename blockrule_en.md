

## Check Block Rule is applied on device

GET /api/v1/interact/filter/query/<device_id>

Example of return result
```
"Content": [
    {
        "BlockApp": [
        "GOOGLE"        //  blocking App google
        ],
        "BlockGroup": null,
        "BlockIp": [
        "1.1.1.1"       //  blocking IP 1.1.1.1
        ],
        "BlockWeb": [
        "google.com"    //  blocking web(domain) google.com
        ],
        "IpAddr": "192.168.122.81",    //  Client is applied
        "MacAddr": "",
        "RuleName": "ok",
        "Updated": 1722432928325
    }
]
```

## Add Block rule
- "ipaddr": is ip of the client to apply this rule, if left blank, the rule will apply to all clients
- "blockapp": is the list of APP IDs provided by the flow
- "blockip": is the list of IP addresses to block
- "blockweb": is the web address to block
- the fields blockapp, blockip, blockweb leave the array empty if not blocked

POST /api/v1/interact/filter/create/<device_id>

```
{
  "options": {
    "rulename": "block rule client 192.168.122.81",
    "ipaddr": "192.168.122.81",
    "blockapp": [
      "TIKTOK"
    ],
    "blockip": [
      "123.123.123.123"
    ],
    "blockweb": [
      "xxx.com"
    ]
  }
}
```

## Update Block Rule
- if "ipaddr" is empty, the updated rule will be applied to all clients
- the blockapp, blockip, blockweb fields will be overwritten (previous values) with new values.


PUT /api/v1/interact/filter/update/<device_id>
```
{
  "options": {
    "rulename": "block rule client 192.168.122.81",
    "ipaddr": "192.168.122.81",
    "blockapp": [
      "TIKTOK"
    ],
    "blockip": [
      "123.123.123.123"
    ],
    "blockweb": [
      "xxx.com"
    ]
  }
}
```

## Delete block rules
- the values ​​in the fields: blockapp, blockip, blockweb listed will be deleted
- For example, in the case below, it will delete ip "123.123.123.123" from the list of blocked ips
- To delete all rules, you need the list of rules currently applied on the system (View Get Api)
- Fields: blockapp, blockip, blockweb will be empty, after deleting all values

DELETE /api/v1/interact/filter/delete/<device_id>
```
{
  "options": {
    "rulename": "block rule client 192.168.122.81",
    "ipaddr": "192.168.122.81",
    "blockapp": [],
    "blockip": [
      "123.123.123.123"
    ],
    "blockweb": []
  }
}
```

