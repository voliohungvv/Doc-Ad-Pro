# Thư viện Ad-Pro

Vui lòng luôn update phiên bản mới nhất
```
implementation 'com.android.fullhd.adssdk:AdsPro:1.0.7'
```

```grovy
maven{
    url = "........"
    allowInsecureProtocol = true   
}
```


# Các tính năng hỗ trợ chính
- Custom layout loading cho tất cả các loại Ad
- Cached các ad full màn hình theo 2 loại key chính [SpaceName, ID Ad]
- Chỉ định version app không load ad.
- Floating debug view hiển thị các trạng thái ad realtime.
- Chỉ load ad thật khi thoả mãn tên version app chỉ có [0-9,.], version name có độ dài là 5, 6 và debug = false.
- Timebetween cho các ad full màn hình,
- Time reload cho các ad view
