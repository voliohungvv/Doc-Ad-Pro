## AdmobNative

##  [Doc Admob](https://developers.google.com/admob/android/native?hl=vi)

## **Hỗ trợ các định dạng**

- native

## **Hiển thị**

Hàm hiển thị một ad native ad lên một view cho trước

> **space:** Đây là tên của ad trong file config cần hiển thị .

> **adContainer :** ViewGroup chứa ad .

> **layoutRes** : Một reslayout chứa design của ad native theo ý muốn.

> **layoutLoadingRes :** Một reslayout chứa view loading, null sẽ hiển thị layout loading mặc định.

> **forceLoadNewAdIfShowed**: Nếu true sẽ load ad mới  vào lần hiển thị tiếp theo mỗi khi ad trước hiển thị thành công, false sẽ hiển thị lại lại ad cũ và sẽ không load mới ad.

> **adCallback :**  Callback lại trạng thái ad .

```kotlin
    AdmobNative.show(
        space: String,
        adContainer: ViewGroup,
        @LayoutRes layoutRes: Int,
        @LayoutRes layoutLoadingRes: Int? = null,
        forceLoadNewAdIfShowed: Boolean = false,
        adCallback: AdCallback? = null,
    )
```

## **Load trước**

Load trước ad để hiển thị ad nhanh hơn.

> **space:** Đây là tên của ad trong file config cần hiển thị .

> **forceLoadNew:** True thì sẽ  load mới ads bất kể ad mang trạng thái nào. False sẽ chỉ load mới khi ad hết hạn  hoặc ad mang trạng thái lỗi , không load đè lại khi đang có ad sẵn kể cả là đã show.

```kotlin
    AdmobNative.load(
        space: String,  
        forceLoadNew: Boolean = false,  
        adCallback: AdCallback? = null
    )
```
## **Lấy trạng thái**

Lấy trạng thái của ad hiện tại được chứa trong mapCached

> **space:** Đây là tên của ad trong file config cần hiển thị .

```kotlin
	AdmobNative.getStatusBySpace(space: String): AdStatus?
```

## **Huỷ bỏ**

Huỷ bỏ một ad và xoá ad đó ra khỏi map cached

> **space:** Đây là tên của ad trong file config cần hiển thị .

```kotlin
	AdmobNative.destroyAdBySpace(space: String)
```

## **Thời gian giữa các lần load mới**

Đối với hàm show sẽ hiển thị lại các ad cũ trước đó (nếu giá trị **forceLoadNewAdIfShowed ** = false). Nhưng thời gian hiển thị tiếp so với lần Ad Impression gần nhất  mà vượt quá giá trị này thì hàm show sẽ load mới ad.

> **value:** Giá trị  thời gian để lần gọi tiếp theo hàm show sẽ load và hiển thị ad mới.

```kotlin
	AdsSDK.setTimeForceLoadNewNative(millisecond: Long): AdsSDK
```