# Sử dụng floating debug view 

Debug view sẽ hiển thị dưới dạng một floating button chạy service và cần có quyền **SYSTEM_ALERT_WINDOW**. Tính năng này đang được phát triển và đã có thể thử nghiệm.

📌 **Một vài tính năng thử nghiệm**

- Thêm nút mở ad inspector của admob thay vì lắc.
- Xem các thông số isPremium, TimebetweenInter, versionNameDisable, Class IgnoreAdResume ...
- Xem thông tin ad được bật, id, trạng thái ad trong thư viện như [Error, Loading, Loaded, Error] realtime.
- Xem thông tin chi tiết về các callback của một ad theo space realtime.
- Xuất log ad vào file txt để debug.

```kotlin
    AdsSDK.showDebugView(context: Context) // chạy service debug view
    AdsSDK.hideDebugView(context: Context) // dừng service debug view
    AdsSDK.autoShowDebugView(value: Boolean, keepDebugViewWhenAppDestroy: Boolean): AdsSDK // tự động hiển thị khi app chạy
```