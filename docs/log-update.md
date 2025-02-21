# Thay đổi các version
- Các thay đổi update qua các version sẽ hiện ở đây từ mới nhất đến thấp nhất. chỉ ghi lại log của các phiển bản chính. 
- Đối với các phiên bản hỗ trợ ktx dưới 1.8. Không có ghi log lại mà dựa vào tên version chính.
Ví dụ phiên bản **1.0.9-ktx-support-below-1.8** thì tương ứng logic với bản **1.0.9** chính
-  [Xem version mới nhất](#version-raw)

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

