# Bắt đầu
**Bước 1:  Tạo file cấu hình ad tĩnh dưới app trong thư mục app/src/main/assets/config.json**
```json
{
  "versionNameDisable": "dev_2.0.0",
  "listAds": [
    {
      "spaceName": "ADMOB_Open_Resume",
      "adsType": "open_app_resume",
      "id": "ca-app-pub-3940256099942544/9257395921",
      "status": true
    },
    {
      "spaceName": "ADMOB_Open_Splash",
      "adsType": "open_app_splash",
      "id": "ca-app-pub-3940256099942544/9257395921",
      "status": true
    },
    {
      "spaceName": "ADMOB_Inter",
      "adsType": "interstitial",
      "id": "ca-app-pub-3940256099942544/1033173712",
      "status": true
    },
    {
      "spaceName": "ADMOB_Inter_Splash",
      "adsType": "interstitial_splash",
      "id": "ca-app-pub-3940256099942544/1033173712",
      "status": true
    },
    {
      "spaceName": "ADMOB_Banner_320x250",
      "adsType": "banner_300x250",
      "id": "ca-app-pub-3940256099942544/6300978111",
      "status": true
    },
    {
      "spaceName": "ADMOB_Banner_Adaptive",
      "adsType": "banner_adaptive",
      "id": "ca-app-pub-8541569573502186/3727064079",
      "status": true
    },

    {
      "spaceName": "ADMOB_Banner_Collapsible_Bottom",
      "adsType": "banner_collapsible_bottom",
      "id": "ca-app-pub-3940256099942544/2014213617",
      "status": true
    },
    {
      "spaceName": "ADMOB_Banner_Collapsible_Top",
      "adsType": "banner_collapsible_top",
      "id": "ca-app-pub-3940256099942544/2014213617",
      "status": true
    },

    {
      "spaceName": "ADMOB_Native",
      "adsType": "native",
      "id": "ca-app-pub-3940256099942544/2247696110",
      "status": true
    },
    {
      "spaceName": "ADMOB_Rewarded_Inter",
      "adsType": "reward_interstitial",
      "id": "ca-app-pub-3940256099942544/5354046379",
      "status": true
    },

    {
      "spaceName": "ADMOB_Rewarded",
      "adsType": "reward",
      "id": "ca-app-pub-3940256099942544/5224354917",
      "status": true
    }
  ]
}

```

**Bước 2:  Init AdSDK**

```kotlin
    AdsSDK.init(
        application = this,
        pathAssetConfigAds = "config.json",
        isDebug = BuildConfig.DEBUG
    )
        .setLogging(BuildConfig.DEBUG) 
        .setIgnoreAdResume(MainActivityBanner1::class.java)
        .registerAdCallback(adsCallback)
        .setTimeForceLoadNewBanner(10_000)
        .setTimeForceLoadNewNative(10_000)
        .enableAppsflyer("key")// cần cấu hình thư viện IAP nếu crash
        .enableTiktokEvent(false)
        .autoShowDebugView(BuildConfig.DEBUG, false) // show debug view
```
📌 **Bước 3:  Triển khai CMP trước khi load các ad khác**

```kotlin
    AdsSDK.showCMP(activity: AppCompatActivity, isTesting: Boolean = false, onDone: () -> Unit)
```

📌 **Tham khảo file [AdUtils.kt](https://gitlab.volio.vn/govo-tech/hd/Ads-Pro/-/blob/develop/app/src/main/java/com/android/fullhd/hd_ad/ads/AdUtils.kt) một vài loại ad**


**Tham khảo [Example](https://gitlab.volio.vn/govo-tech/hd/Ads-Pro/-/tree/develop/app/src/main/java/com/android/fullhd/hd_ad)**