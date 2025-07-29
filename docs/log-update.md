# Thay đổi các version
- Các thay đổi update qua các version sẽ hiện ở đây từ mới nhất đến thấp nhất. chỉ ghi lại log của các phiển bản chính. 
- Đối với các phiên bản hỗ trợ ktx dưới 1.8, và các phiêu bản mới 1.3.x. Không có ghi log lại mà dựa vào tên version chính.
- Đối với version 1.2.11 đang sử dụng admob 23.2.0 mọi logic sẽ tương ứng với version 1.3.1 sử dụng admob 24.0.0
- Ví dụ phiên bản **1.0.9-ktx-support-below-1.8** thì tương ứng logic với bản **1.0.9** chính
-  [Xem version mới nhất](#version-raw)

## Version 1.2.16 | 1.3.6
- [Update] - add AppsFlyer onConversionDataSuccess Listener (add default listener) -> tracking utm-source


## Version 1.2.14, 1.2.15 | 1.3.4. 1.3.5
- [Update] - add small ad loading native collapsible

## Version 1.2.13 | 1.3.3
- [Update] - Fix native meta click 

## Version 1.2.12 | 1.3.2
- [Update] - Xoá log và tối ưu lại login , debug

## Version 1.2.11 | 1.3.1
- [Update] - Thêm loading navite collapsible ở dạng kích thước expand. **autoShowLoadingLarge: Boolean = false**
- [Update] - Thêm debug view riêng của đội HDTeam một vài các tính năng hay dùng khác **{Trigger button, iap inspector, ad inspector, app setting ..}**
- [Fix]- Sửa lỗi khi adview đã vào trạng thái loading thì show mà không check premium nữa. -> Sửa bằng việc thêm logic check **{permium, network, remote config}** trước khi show.
```kotlin
    fun show(
        space: String,
        adContainer: ViewGroup,
        lifecycle: Lifecycle?,
        @LayoutRes layoutRes: Int,
        @LayoutRes collapsibleLayoutRes: Int = R.layout.hd_ad_native_ads_large_collap_demo,
        @LayoutRes layoutLoadingRes: Int? = null,
        forceLoadNewAdIfShowed: Boolean = false,
        blurMediaImage: Boolean = false,
        isFakeClose: Boolean = false,
        autoShowLoadingLarge: Boolean = false, // update
        adCallback: AdCallback? = null,
    )
```

## Version 1.2.9 | 1.2.10
- [Update] - Nâng cấp GDPR experiment lên phiên bản com.google.android.ump:user-messaging-platform:3.2.0
- Vì CD/CD lỗi cached version lên phiển bản 1.2.10 và phiên bản 1.2.9 là giống nhau. 

## Version 1.2.8
- [Update]Mở ra một số các hàm để tracking ad V3 dựa vào 2 hàm **Admob{Type}.getMapAdLoader()** và **Admob{Type}.getKeyCached(space: String)** để truy cập sâu các thuộc
tính của lớp AdLoader<T>
- [Update] Sửa validate json thrown ra dễ hiểu hơn. Khi file json ad sai

```kotlin
    Admob{Type}.getMapAdLoader() // cung cấp map cached theo idCached ( chú ý ad full màn đang cached theo id, adview cached theo space)
    Admob{Type}.getKeyCached(space: String) // dùng hàm này để lấy key cached dùng cho hàm trên truyền vào là space
    GDPRUtils.canShowAd // true  là user bấm consent, false là user bấm do not consent
    GDPRUtils.isGDPR(applicationContext: Context)// true là trong danh sách cần xin consent, false không trong danh sách consent
```

## Version 1.2.7
- Thêm logic control CTR native collapsible . Dùng biến isFakeClose: nếu true click ad, false sẽ hoạt động bình thường.
```kotlin

    AdmobNativeCollapsible.show(
        space: String,
        adContainer: ViewGroup,
        lifecycle: Lifecycle?,
        @LayoutRes layoutRes: Int,
        @LayoutRes collapsibleLayoutRes: Int = R.layout.hd_ad_native_ads_large_collap_demo,
        @LayoutRes layoutLoadingRes: Int? = null,
        forceLoadNewAdIfShowed: Boolean = false,
        blurMediaImage: Boolean = false,
        isFakeClose: Boolean  = false,
        adCallback: AdCallback? = null,
    )
```

## Version 1.2.6
- Để tối ưu appstart time một vài đội yêu cầu lazy init AdsSDK trong activity do vậy . Sửa logic isAutoRegisterActivityAndProcess biến này chịu trách nhiệm
tự động đăng kí activity ứng dụng để show ad full màn hình. Nếu bạn Lazy AdsSDK.init thì bản phải tự đăng kí 2 hàm dưới trong application để tránh lỗi không có activity show ad.
- Đăng kí registerProcessLifeOwner và registerActivityLifecycle trong application và lazy AdsSDK.init

- [Lỗi liên quan] Nếu bạn AdsSDK.init sau khi activity chính của bạn khởi động mà không đăng kí registerProcessLifeOwner và registerActivityLifecycle từ sớm. Sẽ không có acitivty nào được lưu lại và hỗ trợ show ad full màn hình. Ở versio cũ hơn sẽ không xuất hiện callback
- [Sửa] Tách registerProcessLifeOwner và registerActivityLifecycle chủ động đăng kí. Thêm callback onAdOff nếu không có activity tránh kẹt logic chuyển màn.
```kotlin
    AdsSDK.init(
        application: Application,
        pathAssetConfigAds: String,
        isDebug: Boolean = false,
        isAutoRegisterActivityAndProcess: Boolean = true,
        onSuccess: () -> Unit = {}
    ):


    AdsSDK.registerProcessLifeOwner()  \\ đăng kí process để show appresume
    AdsSDK.registerActivityLifecycle(application: Application) \\ đăng kí activity để show add full màn hình

    \\ nếu không thể đăng kí hoặc lí do bất khả kháng hãy cẩn trọng sử dụng thêm và xoá acitity chính của bạn thông qua hàm này
    AdsSDK.addCurrentToListActivityInProcess(activity: Activity) 
    AdsSDK.getCurrentListActivityInProcess(): MutableSet<Activity>
    AdsSDK.removeActivityInProcess(activity: Activity)
}
```
## Version 1.2.5
- [Update] đưa Firebase.initialize(application) vào trong background.
- [Lỗi] Sửa lỗi popup windown not attach to windown tại collapsible native. Khi chuyển màn quá nhanh hoặc có thể xảy ra khi dùng dialogBottomSheetFragment
- [Lí do] Bởi vì viewGroup đang chưa được attachToWindow nên popupWindow.showAsDropDown(viewGroup,...) đang bị lỗi
- [Sửa] Kiểm tra view attachToWindow & inflatter xong trước khi show
```
    Fatal Exception: java.lang.IllegalArgumentException
    View=android.widget.PopupWindow$PopupDecorView{a7f95b1 V.E...... R.....I. 0,0-0,0} not attached to window manager
    android.view.WindowManagerGlobal.findViewLocked (WindowManagerGlobal.java:576)
    android.view.WindowManagerGlobal.updateViewLayout (WindowManagerGlobal.java:465)
    android.view.WindowManagerImpl.updateViewLayout (WindowManagerImpl.java:170)
    android.widget.PopupWindow.update (PopupWindow.java:2230)
    android.widget.PopupWindow.update (PopupWindow.java:2351)
    android.widget.PopupWindow.alignToAnchor (PopupWindow.java:2521)
    android.widget.PopupWindow.-$$Nest$malignToAnchor
    android.widget.PopupWindow$1.onViewAttachedToWindow (PopupWindow.java:245)
    android.view.View.dispatchAttachedToWindow (View.java:22080)
```

## Version 1.2.4
- [Update] Mở publish hàm fun dismissCollapsible(space: String) chủ động đóng collapsible native
```kotlin
    fun dismissCollapsible(space: String): PopupWindow? 
```

## Version 1.2.3
- [Update] Thêm blur media image ở native sử dụng bằng biến **blurMediaImage: Boolean**
Tạo blurmedia đằng sau . phải thêm một  ImageView vào có id = iv_blur vào sau ad_media. có kích thước tương ứng
```kotlin
    fun show(
        space: String,
        adContainer: ViewGroup,
        lifecycle: Lifecycle?,
        @LayoutRes layoutRes: Int,
        @LayoutRes collapsibleLayoutRes: Int = R.layout.hd_ad_native_ads_large_collap_demo,
        @LayoutRes layoutLoadingRes: Int? = null,
        forceLoadNewAdIfShowed: Boolean = false,
        blurMediaImage: Boolean = false,
        adCallback: AdCallback? = null,
    )

```

## Version 1.2.2
- [Update] Thêm hàm tắt các ad full màn hình. Hoặc activity

```kotlin

//Lấy toàn bộ activity còn sống trong process dành cho bạn tự xử lí
fun AdsSDK.getCurrentListActivityInProcess(): MutableSet<Activity> {
}

// finish toàn bộ activit trong process. Vì không phân biệt được các mediation có các ad activiy nào
// do vậy bạn cần truyền vào Activity của chính bạn. VD MainActivity vào except để loại trừ bị finish.
fun AdsSDK.destroyAllActivityInProcess(vararg except: Class<*>){
}

```

## Version 1.2.1 
- [Lỗi] missing ads inter lần thứ 2 sau khi tắt mạng liên tục ( tần suất xảy ra thấp . chỉ khi chuyền màn liên tục). 
- [Lí do] bởi vì callback onAdDismiss gọi chậm hơn hàm load nên ad đã bị gắn thành null tại callback onAdShowFullScreenContent.
- [Sửa] Sửa thành chỉ khi ad đã show thì mới gắn lại ad = null khi show full onAdShowFullScreenContent

- [Update] Sửa init appsflyer dưới background giảm thiểu tình trạng ARN. 
- fun enableAppsflyer(appsflyerId: String, initInBackgroundThread: Boolean = true): AdsSDK

- [Update] <span style="color: red;">Loại bỏ mọi thư viện ad mediation giảm thiểu size app. Từ bây giờ cần gắn mediation cần implement ở tầng app</span>.
- Dưới dây là các version tương thích với bản 1.2.1
- [Chú ý]: Vì không còn mediation nên nếu bị ad full màn hình đè (ad resume). Thì phải thêm class vào  hàm dưới cho module ads check
```kotlin

fun setClazzAdFullScreenOfMediation(vararg clazz: Class<*>)

fun clearSetClazzAdFullScreenOfMediation() 
```

```gradle

   api 'com.google.ads.mediation:facebook:6.17.0.0'
   api 'com.google.ads.mediation:adcolony:4.8.0.2'
   api 'com.google.ads.mediation:applovin:12.5.0.1'
   api 'com.google.ads.mediation:vungle:7.4.0.0'
   api 'com.google.ads.mediation:pangle:6.0.0.8.0'
   api 'com.google.ads.mediation:mintegral:16.7.81.0'
   api('com.facebook.android:facebook-android-sdk:latest.release') {
       exclude group: 'com.google.zxing'
   }
   api("com.unity3d.ads:unity-ads:4.9.2")
   api("com.google.ads.mediation:unity:4.9.2.0")

```

## Version 1.2.0 (Big update)
- Sửa thư viện hỗ trợ high floor. 
- Hỗ trợ 2 định dạng json format. V3 kiểu cũ, V4 kiểu mới
- Thay đổi hàm callback


- <span style="color: red;">Thêm trường id:</span> Đây là id được thao tác trong list id của adsModel. <span style="color: red;">Một vài logic phải chú ý</span> ví dụ như hàm onStartLoading sẽ phải là id đứng đầu. Nhưng thư viện có thể load failed các id đầu và callback về các id thành công phía sau dẫn tới ID loading và ID onLoaded khác nhau.


- callback mới: 
```kotlin 
override fun onAdImpression(adsModel: AdModel, id: String) {
            super.onAdImpression(adsModel, id)
            Log.e(TAG, "onAdImpression: ${adsModel.spaceName} _ ${adsModel.id} |")
        }
```

- callback cũ: 
```kotlin 
override fun onAdImpression(adsModel: AdModel) {
            super.onAdImpression(adsModel)
            Log.e(TAG, "onAdImpression: ${adsModel.spaceName} _ ${id} |")
        }
```

## Version 1.1.1
-  Hạ cấp appfly về bản cũ trước đó : Sửa lỗi sau 
```
No virtual method sendAdRevenue(Landroid/content/Context;Ljava/util/Map;)V in class Lcom/appsflyer/AppsFlyerLib; or its super classes (declaration of 'com.appsflyer.AppsFlyerLib' appears in /data/app/~~SWEPUGEQbTMBNVW8AaHpZw==/

```

## Version 1.1.0
-  Thêm record exception vào các hàm của appflyer . Thử fix lỗi crash sau

```
 Fatal Exception: java.lang.IllegalArgumentException: key [und_aaland] in alias:language contains unsupported fields combination.
       at android.icu.util.ULocale$AliasReplacer.loadAliasData(ULocale.java:1294)
       at android.icu.util.ULocale$AliasReplacer.replace(ULocale.java:1184)
       at android.icu.util.ULocale.canonicalize(ULocale.java:1680)
       at android.icu.util.ULocale.createCanonical(ULocale.java:443)
       at android.icu.impl.CalendarUtil.getCalendarType(CalendarUtil.java:52)
       at android.icu.util.Calendar.getCalendarTypeForLocale(Calendar.java:1716)
       at android.icu.util.Calendar.createInstance(Calendar.java:1731)
       at android.icu.util.Calendar.getInstanceInternal(Calendar.java:1701)
       at android.icu.util.Calendar.getInstance(Calendar.java:1656)
       at libcore.icu.LocaleData.initializeCalendarData(LocaleData.java:252)
       at libcore.icu.LocaleData.initLocaleData(LocaleData.java:217)
       at libcore.icu.LocaleData.get(LocaleData.java:195)
       at java.util.Calendar.setWeekCountData(Calendar.java:3387)
       at java.util.Calendar.<init>(Calendar.java:1612)
       at java.util.GregorianCalendar.<init>(GregorianCalendar.java:627)
       at java.util.Calendar.createCalendar(Calendar.java:1684)
       at java.util.Calendar.getInstance(Calendar.java:1652)
       at java.text.SimpleDateFormat.initializeCalendar(SimpleDateFormat.java:758)
       at java.text.SimpleDateFormat.<init>(SimpleDateFormat.java:702)
       at com.appsflyer.internal.AFb1rSDK.valueOf(SourceFile:61)
       at com.appsflyer.internal.AFb1tSDK.AFInAppEventParameterName(:57)
       at com.appsflyer.internal.AFa1dSDK$AFa1xSDK.AFInAppEventType(SourceFile:2575)
       at com.appsflyer.internal.AFd1tSDK$1.run(:221)
       at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1137)
       at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:637)
       at java.lang.Thread.run(Thread.java:1012)

```

## Version 1.0.9
-  Prevent ad banner adaptive destroy when lifecycle desstroy. Chỉ áp dụng destroy với ad native khi gắn lifecycler.

## Version 1.0.8
-  Fix ad banner destroy when refresh. Fix một vài trường hợp ad banner khi tự reload lại sẽ bị đen.

## Version 1.0.7
- Sửa validate version name khi build cho phép load ad thật . Chỉ bao gồm số và dấu . + thêm độ dài version name chỉ gồm 5,6 kí tự.

## Version 1.0.6
- Fix callback ad native trong trường hợp ad natvie, banner  load trước (preload) và show sau sẽ không gọi callback onAdClick.

## Version 1.0.5
-  Nâng version google-play-ads từ 22.3.0 -> 23.2.0

## Version 1.0.4
-  Sửa lỗi ad inter load trước không có callback adOnPaidValue.

## Version 1.0.3
-  Thêm định dạng native collapsible

## Version 1.0.2
-  Fix lỗi ad colapsible crash khi tự động destroy tại  **override fun onDestroy(owner: LifecycleOwner)** xảy ra khi (load ở 1 activity và show ở một activity khác).
-  Add Unity ad mediation.


## Version 1.0.1
-  Fix lỗi ad native và ad banner load thừa trên dialog gây giảm show rate.
-  Fix lỗi timeout CMP tự động chuyển khi hết thời gian -> Chỉ timeout khi form CMP chưa hiện. Nếu hiện rồi thì huỷ timeout

## Version Raw
Các version dưới đang sắp xếp theo dạng thô và cách nhau bằng dấu cách " ". Phiên bản mới nhất là sau chữ <span style="color: red;">com.android.fullhd.adssdk AdsPro</span>.
<iframe src="https://repo.volio.vn/repository/maven-s3/com/android/fullhd/adssdk/AdsPro/maven-metadata.xml" width="100%" height="100px"></iframe>

