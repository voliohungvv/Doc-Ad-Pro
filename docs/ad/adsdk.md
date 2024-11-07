# AdSDK

Một vài hàm thường dùng trong AdsSDK

## **Kiểm tra init** 

```kotlin
	AdsSDK.checkInit(): Boolean
```

## **Init module AdsSDK**

Hàm này chứa khởi tạo MobileAds.initialize bất đồng bộ và loadConfigAsset đồng bộ.

```kotlin
	AdsSDK.init(  
		  application: Application,  
		  pathAssetConfigAds: String,  
		  isDebug: Boolean = false  
	): AdsSDK
```

## **Load cấu hình từ text Json**

Load cấu hình và validate cấu hình thành công sẽ có trạng thái AdsSDK.adsSourceConfig = AdSourceConfig.Json .
>**overrideOldConfig** True sẽ ghi đè toàn bộ cấu hình hiện tại bằng cấu hình cũ. False sẽ merger listAds và lấy cả spaceName cũ và với.

```kotlin
	AdsSDK.loadAdsFromJson(jsonDataAds: String, overrideOldConfig: Boolean = true):AdsSDK
```

## **Load cấu hình từ path Asset File**

Load cấu hình và validate cấu hình thành công sẽ có trạng thái AdsSDK.adsSourceConfig = AdSourceConfig.Asset.

```kotlin
	AdsSDK.loadAdsFromAssetFile(pathAsset: String, overrideOldConfig: Boolean = true): AdsSDK
```

## **Load  Cấu hình từ  RemoteConfig**

Load cấu hình và validate cấu hình thành công sẽ có trạng thái AdsSDK.adsSourceConfig = AdSourceConfig.RemoteConfig.

```kotlin
	AdsSDK.loadAdsFromRemoteConfig(
		    keyConfigAds: String,
		    keyTimeBetweenAdInter: String = "",
		    overrideOldConfig: Boolean = true
	): AdsSDK
```


## **Gọi check update version**

Hàm này chạy bất đồng bộ và có thể hiện view update ở bất cứ đâu.

```kotlin
    AdsSDK.checkShowAppUpdate()
```

## **Gọi check showCMP**

Hàm này sẽ check consent form và trả về onDone dù user có đồng ý hay không . Có timeout là 5_000 milisec

```kotlin
	AdsSDK.showCMP(activity: AppCompatActivity, isTesting: Boolean = false, onDone: () -> Unit)
```

## **Thời gian reload banner**

Thời gian load mới banner từ lần impression gần nhất.

```kotlin
	AdsSDK.setTimeForceLoadNewBanner(millisecond: Long): AdsSDK
```

## **Thời gian reload native**

Thời gian load mới banner từ lần impression gần nhất.

```kotlin
	AdsSDK.setTimeForceLoadNewNative(millisecond: Long): AdsSDK
```

## **Loại bỏ check show ad full screen nâng cao**

Một vài trường hợp có thể xảy ra check show đè các ad  full screen quá mức xảy ra lỗi khi các loading liên tục. Bạn có thể tắt bằng cách truyền giá trị True để tắt code check show đè của thư viện. Lúc này bạn sẽ phải check đè ad resume bằng tay khi hiển thị loading dialog.

```kotlin
	AdsSDK.setDisableCheckShowOverrideAdvanceAdFullscreen(value: Boolean): AdsSDK
```

## **Loại bỏ các lớp không tự động show open app resume**

Có thể thêm Fragment, Activity tương ứng để loại bỏ show open app resume tự động

```kotlin
	AdsSDK.setIgnoreAdResume(vararg clazz: Class<*>): AdsSDK
```

## **Đăng kí callback tổng lắng nghe mọi ad**

Đăng kí mọi trạng thái , callback của ad trong sdk. **Callback này luôn gọi trước callback riêng lẻ của các hàm khác**

```kotlin
	AdsSDK.registerAdCallback(callback: AdCallback): AdsSDK
	AdsSDK.unregisterAdCallback(callback: AdCallback): AdsSDK
```

## **Lấy Client ID**

Lấy client ID của device hiện tại dành cho mục đính cấu hình máy test trên admob

```kotlin
	AdsSDK.getClientAdID(
	    context: Context,
	    onSuccess: (String?) -> Unit,
	    onFailed: (Throwable?) -> Unit
	)
```

## **Mở debug Menu Admob**

Mở debug menu của Admob. Menu này bao gồm các chức năng (Ad infomation, Open ad inspector ...)

```kotlin
	AdsSDK.openDebugMenu(context: Context, adUnitID: String)
```

## **Mở ad Inspector**

Mở Ad Inspector của Admob

```kotlin
	AdsSDK.openAdInspector(context: Context)
```

## **Thêm device test**

Thêm device test ad khi request

```kotlin
	AdsSDK.setTestDeviceID(testDeviceIds: List<String>)
```

## **Mở debug view của thư viện **

Mở Floatting button debug view service của thư viện. Giúp theo dõi các callback , trạng thái ad

```kotlin
	AdsSDK.showDebugView(context: Context) // hiện
	AdsSDK.hideDebugView(context: Context) // ẩn
```

## **Auto show debug view khi app chạy**

Tự động Mở Floatting button khi application resume

>**keepDebugViewWhenAppDestroy:** True thì thoát app debug view vẫn chạy như một service do vậy app sẽ không chết và debug các task service khác, False debug view sẽ tự động dừng khi không còn activity, task nào hoạt động

```kotlin
	AdsSDK.autoShowDebugView(value: Boolean, keepDebugViewWhenAppDestroy: Boolean): AdsSDK
```