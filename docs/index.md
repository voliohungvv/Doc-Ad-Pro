## Tổng quan thư viện Ad-Pro

Các thông tin fix lỗi, tính năng, thay đổi hàm, logic mới nhất ở đây [Cập nhật version](log-update.md) . Phải đọc để nắm được tổng quan.

<span style="color: red;"> Có thể các tính năng, các hàm fix, update, remove có thể khác do chưa kịp chính sửa trong các mục ad tương ứng. Hãy theo dõi [Cập nhật version](log-update.md)</span>.

Vui lòng luôn update phiên bản mới nhất
```
implementation 'com.android.fullhd.adssdk:AdsPro:1.2.11' // cũng chưa chắc phải mới nhất :) 
```

Với phiên bản hỗ trợ ktx dưới 1.8
```
implementation 'com.android.fullhd.adssdk:AdsPro:1.0.9-ktx-support-below-1.8' // cũng chưa chắc phải mới nhất :)
```

```grovy
maven{
    url = "........"
}
```

<span style="color: red;">Note: Thư viện dần triển khai và hỗ trợ dạng high floor. Bản 1.1.1 sẽ là bản cuối cùng ổn định và không có high floor. Từ bạn tiếp theo 1.2.0 bản buộc phải update lại file json ads trên cả "remote" và dưới "ứng dụng" </span>.

- Tools hỗ trợ ad [Tool chuyển đổi json format, export json ... ](https://drive.google.com/drive/folders/1P7HglFxnaO1J3YcnrbT9XaijNZYlf4ne)


- Nếu dùng từ 1.1.1 trở xuống [Triển khai nhanh](started_below_1.2.md)
- Nếu dùng từ 1.2.0 trở lên   [Triển khai nhanh](started_above_1.2.md)
## Các tính năng hỗ trợ chính
- Custom layout loading cho tất cả các loại Ad
- Cached các ad full màn hình theo 2 loại key chính [SpaceName, ID Ad]
- Chỉ định version app không load ad.
- Floating debug view hiển thị các trạng thái ad realtime.
- Chỉ load ad thật khi thoả mãn tên version app chỉ có [0-9,.], version name có độ dài là 5, 6 và debug = false.
- Timebetween cho các ad full màn hình,
- Time reload cho các ad view
