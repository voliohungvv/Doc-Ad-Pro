# AdmobOpenResume

##  [Doc Admob](https://developers.google.com/admob/android/app-open?hl=vi)

Với định dạng ad này quảng cáo load trước sẽ bị hết giá trị sau 4 tiếng  do vậy . Ad sau 1 tiếng kể từ khi load mà chưa được hiển thị sẽ rơi vào trạng thái **Error**

## **Hỗ trợ các định dạng**

- open_app_resume

## **Hiển thị**

Hàm hiển thị một ad inter **Đã có trạng thái loaded** lên toàn màn hình

> **space:** Đây là tên của ad trong file config cần hiển thị .

> **lifecycle:** lifecycle này sẽ giúp hiển thị ad khi activity/fragment quay trở lại resume, tránh show dưới background. Đối số này có thể null nhưng bạn sẽ phải chấp nhận ad có thể failed to show nếu app in background.

> **autoShowLoading** : True sẽ hỗ trở hiển thị dialog loading. False sẽ không hiển thị

> **ignoreTimeBetweenAd:** Thời gian tối thiểu giữa 2 lần show ad .True sẽ không bị ràng buộc bởi thời gian 2 lần show ad cùng **Key cached**. False sẽ chịu ảnh hưởng bởi timebetween trong thư viện.

> **adCallback :**  Callback lại trạng thái ad .

```kotlin
    AdmobOpenResume.show(
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

> **timeoutMillisecond:** Thời gian timeout load ad phản hồi.  mặc định là 20_000

> **adCallback :**  Callback lại trạng thái ad .
```kotlin
	AdmobOpenResume.load(
        space: String,
        adCallback: AdCallback? = null,
        timeoutMillisecond: Long = 20_000L,
    )
```

## **load và hiển thị**

Hàm sẽ bắt đầu load một ad và  hiển thị luôn lên toàn màn hình

> **space:** Đây là tên của ad trong file config cần hiển thị .

> **lifecycle:** lifecycle này sẽ giúp hiển thị ad khi activity/fragment quay trở lại resume, tránh show dưới background. Đối số này có thể null nhưng bạn sẽ phải chấp nhận ad có thể failed to show nếu app in background.

> **autoShowLoading** : True sẽ hỗ trở hiển thị dialog loading. False sẽ không hiển thị.

> **timeoutMillisecond:** Thời gian timeout load ad phản hồi.  mặc định là 20_000

> **ignoreTimeBetweenAd:** Thời gian tối thiểu giữa 2 lần show ad .True sẽ không bị ràng buộc bởi thời gian 2 lần show ad cùng **Key cached**. False sẽ chịu ảnh hưởng bởi timebetween trong thư viện.

> **adCallback :**  Callback lại trạng thái ad .

```kotlin
    AdmobOpenResume.loadAndShow(
        space: String,
        lifecycle: Lifecycle?,
        adCallback: AdCallback?,
        autoShowLoading: Boolean = true,
        timeoutMillisecond: Long = 20_000L,
        ignoreTimeBetweenAd: Boolean = false,
    )
```

## **Lấy trạng thái**

Lấy trạng thái của ad hiện tại được chứa trong mapCached

> **space:** Đây là tên của ad trong file config cần hiển thị .

```kotlin
	AdmobOpenResume.getStatusBySpace(space: String): AdStatus?
```

## **Huỷ bỏ**

Huỷ bỏ một ad và xoá ad đó ra khỏi map cached

> **space:** Đây là tên của ad trong file config cần hiển thị .

```kotlin
	AdmobOpenResume.destroyAdBySpace(space: String)
```

## **Thời gian giữa các lần hiển thị 2 ad chung cached key**

Thời gian tối thiểu giữa  2 lần hiển thị ad chung cached key. **Cached key** ở đây có thể là space hoặc id  ad tuỳ thuộc vào option bạn cấu hình

> **timeBetweenMillisecond:** Giá trị  thời gian để lần gọi tiếp theo hàm show sẽ load và hiển thị ad mới mặc định là 15_000.

```kotlin
    AdmobOpenResume.setTimeBetween(timeBetweenMillisecond: Long): AdmobOpenResume
    AdmobOpenResume.getTimeBetween(): Long
```
## **Cấu hình key trong mapCached**

**Cached key** ở đây có thể là space hoặc id  ad tuỳ thuộc vào option bạn cấu hình. Giá trị này áp dụng cho toàn bộ lớp

Đối với các ad inter mà bạn có thể muốn tắt bật ở nhiều vị trí. Bạn có thể cần nhắc cache theo id ad. và tách nhiều space . Vẫn đảm bảo show chung 1 space nhưng có nhiều space để bạn tắt

> **value:** True sẽ là cached theo space. False sẽ cached theo id.

> **space:** Trả về cached key theo space name.

```kotlin
	AdmobOpenResume.setCachedBySpace(value: Boolean): AdmobOpenResume
	AdmobOpenResume.getKeyCached(space: String): String
```

## **Cấu hình dialog loading**

Hỗ trợ cấu hình dialog bao gồm cả layout và các giá trị thuộc tính của dialog.
Mặc định đã có dialog hiển thị. Giá trị này áp dụng cho toàn bộ lớp

> **resLayout:** Một layout chứa design cho dialog loading .

> **configurator:** Một interface ghi đè lại các cấu hình dialog mà bạn muốn hiển thị.

```kotlin
	AdmobOpenResume.setDialogConfigurator(
        @LayoutRes resLayout: Int?,
        configurator: DialogLoadingConfigurator?
	)
```
## **Thời gian tối thiểu dialog hiện trước khi show ad**

Vì ad bạn có thể đã preload hoặc ad có thể hiện luôn nhưng bạn vẫn muốn hiển thị dialog. Do vậy rất có thể dialog hiện và ẩn nhanh có thể gây trải nghiệm xấu. Đây là thời gian tối thiểu hiện dialog trước khi show ad. Giá trị này áp dụng cho toàn bộ lớp

> **value:** Giá trị  thời gian milisec tối thiểu hiện dialog mặc định là 2_000.

```kotlin
	AdmobOpenResume.setMinTimeShowDialog(value: Long): AdmobInterSplash
```

## **Tự động load và show open ad resume**

**Hỗ trợ hàm load lần đầu để show tự động open ad resume. bạn phải gọi hàm này thì module ad sẽ tự động show và load các lần tiếp theo. Bạn lưu ý nên tránh load ở activity có intent LAUNCHER vì có thể sẽ miss mất CMP nếu bạn gọi CMP ở splash. Do vậy bạn nên gọi ở các fragment bên trong ví dụ có thể là homeFragment. Các hàm load này luôn check có ad loaded rồi sẽ không load nữa**

> **space:**  Đây là tên của ad auto show open ad

> **timeoutMillisecond:** Thời gian timeout load ad phản hồi.  mặc định là 20_000

> **adCallback :**  Callback lại trạng thái ad .


```kotlin
	AdmobOpenResume.loadAndAutoShowIfAvailable(
        space: String,
        adCallback: AdCallback? = null,
        timeoutMillisecond: Long = 20_000L
    )
```

## **Bật tắt tự động load sau khi đóng open ad resume tự động**

Nếu bạn muốn tối ưu thời gian load ad hoặc logic nào đó mà không muốn module tự động load next ad sau khi đóng ad  open tự động bạn có thể tắt.

> **value:**  True sẽ tự động load open ad sau khi đóng, false sẽ không tự load

```kotlin
	AdmobOpenResume.setAutoLoadNextAfterClose(value: Boolean): AdmobOpenResume
```

## **Cấu hình thời gian delay lần load tiếp theo của ad resume tự động**

Nếu bạn muốn tối ưu thời gian load ad bạn có thể để giá trị này. Đây là khoảng thời gian delay sau khi đóng open ad resume tự động để load tiếp

> **value:**  Giá trị delay trước khi load ad resume tự động tiếp theo

```kotlin
	AdmobOpenResume.setTimeDelayAutoPreloadNextAfterClose(value: Long): AdmobOpenResume
```

## **Tắt show open ad resume tự động.**

Tắt hoặcbật  open ad resume tự động cho đến khi đổi giá trị lại.

> **value:**  True bật hiện open ad resume , False tắt show open ad resume.

```kotlin
	AdmobOpenResume.setAutoShowOpenResume(value: Boolean): AdmobOpenResume
```


## **Tắt show open ad resume tự động trong lần kế tiếp.**

Tắt hoặc bật  open ad resume trong lần kế. Giá trị này chỉ có tác dụng trong lần kế tiếp và nó sẽ tự động trở lại false sau khi ngăn được 1 lần show kế tiếp

> **value:**  True bật hiện open ad resume trong lần kế tiếp, False tắt show open ad resume trong lần kế tiếp.

```kotlin
	AdmobOpenResume.preventPreventShowNextSession(value: Boolean): AdmobOpenResume
```
