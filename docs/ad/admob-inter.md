# AdmobInter
##  [Doc Admob](https://developers.google.com/admob/android/interstitial?hl=vi)

Với định dạng ad này quảng cáo load trước sẽ bị hết giá trị sau 1 tiếng  do vậy . Ad sau 1 tiếng kể từ khi load mà chưa được hiển thị sẽ rơi vào trạng thái **Error**.

## **Hỗ trợ các định dạng**

- interstitial

## **Hiển thị**

Hàm hiển thị một ad inter **Đã có trạng thái loaded** lên toàn màn hình

> **space:** Đây là tên của ad trong file config cần hiển thị .

> **lifecycle:** lifecycle này sẽ giúp hiển thị ad khi activity/fragment quay trở lại resume, tránh show dưới background. Đối số này có thể null nhưng bạn sẽ phải chấp nhận ad có thể failed to show nếu app in background.

> **autoShowLoading** : True sẽ hỗ trở hiển thị dialog loading. False sẽ không hiển thị.

> **ignoreTimeBetweenAd:** Thời gian tối thiểu giữa 2 lần show ad .True sẽ không bị ràng buộc bởi thời gian 2 lần show ad cùng **Key cached**. False sẽ chịu ảnh hưởng bởi timebetween trong thư viện.

> **adCallback :**  Callback lại trạng thái ad .

```kotlin
    AdmobInter.show(
        space: String,  
        lifecycle: Lifecycle?,  
        adCallback: AdCallback? = null,  
        autoShowLoading: Boolean = false,  
        ignoreTimeBetweenAd: Boolean = false,
    )
```

## **Load trước**

Load trước ad để hiển thị ad nhanh hơn.

> **space:** Đây là tên của ad trong file config cần hiển thị .

> **timeoutMillisecond:** Thời gian timeout load ad phản hồi.  mặc định là 18_000 milisec

> **adCallback :**  Callback lại trạng thái ad .

```kotlin
	AdmobInter.load(
        space: String,
        adCallback: AdCallback? = null,
        timeoutMillisecond: Long = 18_000L
    )
```

## **load và hiển thị**

Hàm sẽ bắt đầu load một ad và  hiển thị luôn lên toàn màn hình

> **space:** Đây là tên của ad trong file config cần hiển thị .

> **lifecycle:** lifecycle này sẽ giúp hiển thị ad khi activity/fragment quay trở lại resume, tránh show dưới background. Đối số này có thể null nhưng bạn sẽ phải chấp nhận ad có thể failed to show nếu app in background.

> **autoShowLoading** : True sẽ hỗ trở hiển thị dialog loading. False sẽ không hiển thị.

> **timeoutMillisecond:** Thời gian timeout load ad phản hồi.  mặc định là 18_000 milisec.

> **ignoreTimeBetweenAd:** Thời gian tối thiểu giữa 2 lần show ad .True sẽ không bị ràng buộc bởi thời gian 2 lần show ad cùng **Key cached**. False sẽ chịu ảnh hưởng bởi timebetween trong thư viện.

> **adCallback :**  Callback lại trạng thái ad .

```kotlin
    AdmobInter.loadAndShow(
        space: String,
        lifecycle: Lifecycle?,
        adCallback: AdCallback?,
        autoShowLoading: Boolean = true,
        timeoutMillisecond: Long = 18_000L,
        ignoreTimeBetweenAd: Boolean = false,
    )
```

## **Lấy trạng thái**

Lấy trạng thái của ad hiện tại được chứa trong mapCached

> **space:** Đây là tên của ad trong file config cần hiển thị .

```kotlin
	AdmobInter.getStatusBySpace(space: String): AdStatus?
```

## **Huỷ bỏ**

Huỷ bỏ một ad và xoá ad đó ra khỏi map cached

> **space:** Đây là tên của ad trong file config cần hiển thị .

```kotlin
	AdmobInter.destroyAdBySpace(space: String)
```

## **Thời gian giữa các lần hiển thị 2 ad chung cached key**

Thời gian tối thiểu giữa  2 lần hiển thị ad chung cached key. **Cached key** ở đây có thể là space hoặc id  ad tuỳ thuộc vào option bạn cấu hình. Giá trị này áp dụng cho toàn bộ lớp.

> **timeBetweenMillisecond:** Giá trị  thời gian để lần gọi tiếp theo hàm show sẽ load và hiển thị ad mới.

```kotlin
	AdmobInter.setTimeBetween(timeBetweenMillisecond: Long): AdmobInter
	AdmobInter.getTimeBetween(): Long
```
## **Cấu hình key trong mapCached**

**Cached key** ở đây có thể là space hoặc id  ad tuỳ thuộc vào option bạn cấu hình. Giá trị này áp dụng cho toàn bộ lớp.

Đối với các ad inter mà bạn có thể muốn tắt bật ở nhiều vị trí. Bạn có thể cần nhắc cache theo id ad. và tách nhiều space . Vẫn đảm bảo show chung 1 space nhưng có nhiều space để bạn tắt.

> **value:** True sẽ là cached theo space. False sẽ cached theo id.

> **space:** Trả về cached key theo space name.

```kotlin
	AdmobInter.setCachedBySpace(value: Boolean): AdmobInter
	AdmobInter.getKeyCached(space: String): String
```

## **Cấu hình dialog loading**

Hỗ trợ cấu hình dialog bao gồm cả layout và các giá trị thuộc tính của dialog. Giá trị này áp dụng cho toàn bộ lớp.

> **resLayout:** Một layout chứa design cho dialog loading .

> **configurator:** Một interface ghi đè lại các cấu hình dialog mà bạn muốn hiển thị.

```kotlin
    AdmobInter.setDialogConfigurator(
        @LayoutRes resLayout: Int?,
        configurator: DialogLoadingConfigurator?
    )
```

## **Thời gian tối thiểu dialog hiện trước khi show ad**

Vì ad bạn có thể đã preload hoặc ad có thể hiện luôn nhưng bạn vẫn muốn hiển thị dialog. Do vậy rất có thể dialog hiện và ẩn nhanh có thể gây trải nghiệm xấu. Đây là thời gian tối thiểu hiện dialog trước khi show ad. Giá trị này áp dụng cho toàn bộ lớp.

> **value:** Giá trị  thời gian milisec tối thiểu hiện dialog. Giá trị mặc định là 2_000.

```kotlin
    AdmobInter.setMinTimeShowDialog(value: Long): AdmobInter
```
