

### Kiểm tra Block Rule đang được áp dụng trên thiết bị
/api/v1/interact/filter/query/<device_id>

## ví dụ kết quả trả về
```
"Content": [
    {
        "BlockApp": [
        "GOOGLE"        // đang chặn App google
        ],
        "BlockGroup": null,
        "BlockIp": [
        "1.1.1.1"       // đang chặn IP 1.1.1.1
        ],
        "BlockWeb": [
        "google.com"    // đang chặn web(domain) google.com
        ],
        "IpAddr": "192.168.9.9",    // Client được áp dụng
        "MacAddr": "",
        "RuleName": "ok",
        "Updated": 1722432928325
    }
]
```


### Thêm Block rule
### "ipaddr": là ip của client cần áp dụng rule này, nếu để trống thì rule sẽ áp dụng với toàn bộ client
### "blockapp": là danh sách các APP ID mà flow cung cấp
### "blockip": là danh sách địa chỉ Ip cần chặn
### "blockweb": là địa chỉ web cần chặn
### các trường blockapp, blockip, blockweb để mảng rỗng nếu không không chặn 
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
### Cập nhật Block Rule
### nếu "ipaddr" để rỗng, rule sẽ được cập nhật sẽ được áp dụng cho toàn bộ client
### các trường blockapp, blockip, blockweb sẽ được ghi đè bằng các giá trị mới.
###
PUT /api/v1/interact/filter/create/<device_id>
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

### Xóa các block rule
### những giá trị trong các trường: blockapp, blockip, blockweb được liệt kê sẽ bị xóa 
### Ví dụ trong trường hợp dưới đây sẽ xóa ip "123.123.123.123" khỏi danh sách chặn ip
### Muốn xóa toàn bộ rule thì cần list rule hiện đang được áp dụng trên hệ thống (GET API)
DELETE /api/v1/interact/filter/create/<device_id>
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

