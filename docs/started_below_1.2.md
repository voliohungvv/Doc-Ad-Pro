# Bắt đầu

<span style="color: red;">Đây là hướng dẫn bản cuối (1.1.1) hỗ trợ dạng json format cũ bên dưới (không hỗ trợ nâng cấp trong tương lai). Trên bản 1.2.0 vui lòng đọc triển khai. [Cập nhật version](started_above_1.2.md)</span>.

📌**Bước 1: Implement thư viện (xem ver mới nhất ở đầu page)**
```
implementation 'com.android.fullhd.adssdk:AdsPro:1.1.1' 
```

```grovy
maven{
    url = "........"
    allowInsecureProtocol = true   
}
```

📌**Bước 2:  Tạo file cấu hình ad tĩnh dưới app trong thư mục app/src/main/assets/config.json**
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
      "spaceName": "ADMOB_Native_collapsible",
      "adsType": "native_collapsible",
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

📌**Bước 3:  Init AdSDK**

[Vui lòng bấm vào đọc kĩ "setTimeForceLoadNewNative(10_000)" dùng không thì bỏ qua](https://voliohungvv.github.io/Doc-Ad-Pro/ad/admob-native/#thoi-gian-giua-cac-lan-load-moi) 

```kotlin
    AdsSDK.init(
        application = this,
        pathAssetConfigAds = "config.json",
        isDebug = BuildConfig.DEBUG
    )
        .setLogging(BuildConfig.DEBUG) 
        .setIgnoreAdResume(SplashActivity::class.java) // set các fragment,  activiy không show open ad
        .registerAdCallback(adsCallback)
        .enableAppsflyer("key")// cần cấu hình thư viện IAP nếu crash
        .enableTiktokEvent(false)
        .autoShowDebugView(false, false) // show debug view chỉ nên bật khi test ad
        .loadAdsFromRemoteConfig(keyConfigAds = "ADMOB_V3", keyTimeBetweenAdInter = "timeBetweenMillisecond")
       // .setTimeForceLoadNewBanner(10_000) 
       // .setTimeForceLoadNewNative(10_000)

```

```kotlin
private  val TAG = "LOG_ADS"
private val adCallback = object : AdCallback {
        override fun onAdStartLoading(adsModel: AdModel) {
            super.onAdStartLoading(adsModel)
            Log.e(TAG, "onAdStartLoading: ${adsModel}")
        }

        override fun onAdClicked(adsModel: AdModel) {
            super.onAdClicked(adsModel)
            Log.e(TAG, "onAdClicked: ${adsModel}")
            toastDebug("click : ${adsModel.type} \n ${adsModel.id.takeLast(4)}")

        }

        override fun onAdClosed(adsModel: AdModel) {
            super.onAdClosed(adsModel)
            Log.e(TAG, "onAdClosed: ${adsModel}")
        }

        override fun onAdDismissedFullScreenContent(adsModel: AdModel) {
            super.onAdDismissedFullScreenContent(adsModel)
            Log.e(TAG, "onAdDismissedFullScreenContent: ${adsModel}")
        }

        override fun onAdShowedFullScreenContent(adsModel: AdModel) {
            super.onAdShowedFullScreenContent(adsModel)
            Log.e(TAG, "onAdShowedFullScreenContent: ${adsModel}")
        }

        override fun onAdFailedToShowFullScreenContent(
            adsModel: AdModel,
            error: AdSDKError?
        ) {
            super.onAdFailedToShowFullScreenContent(adsModel, error)
            Log.e(TAG, "onAdFailedToShowFullScreenContent: ${adsModel} - ${error.toString()}")
        }

        override fun onAdFailedToLoad(adsModel: AdModel, error: AdSDKError?) {
            super.onAdFailedToLoad(adsModel, error)
            Log.e(TAG, "onAdFailedToLoad: ${adsModel} -  ${error.toString()}")
        }

        override fun onAdImpression(adsModel: AdModel) {
            super.onAdImpression(adsModel)
            Log.e(TAG, "onAdImpression: ${adsModel}")
        }

        override fun onAdLoaded(adsModel: AdModel) {
            super.onAdLoaded(adsModel)
            Log.e(TAG, "onAdLoaded: $adsModel")
            toastDebug("loaded : ${adsModel.type} \n ${adsModel.id.takeLast(4)}")
        }
        

        override fun onAdPaidValueListener(adsModel: AdModel, bundle: Bundle) {
            super.onAdPaidValueListener(adsModel, bundle)
            Log.e(TAG, "onAdPaidValueListener: ${adsModel.spaceName}")
        }

        override fun onAdOff(adsModel: AdModel, error: AdSDKError?) {
            Log.e(TAG, "onAdOff: ${adsModel} -  ${error.toString()} ")
        }

    }

    private fun toastDebug(text: CharSequence) {
        if (BuildConfig.DEBUG) {
            Toast.makeText(this, text, Toast.LENGTH_SHORT).show()
        }
    }

```

📌 **Bước 4:  Triển khai CMP trước khi load các ad khác thường trước khi show ad splash**

```kotlin
    showCMP(activity: AppCompatActivity, isTesting: Boolean = false,timeoutMillis: Long = 10_000L, onDone: () -> Unit)
```

📌 **Bước 5:  Triển khai logic update version nếu cần sử dụng thường ở màn splash**

```kotlin
    AdsSDK.checkShowAppUpdate() // hàm bất đồng bộ chỉ cần gọi 
```

📌 **Bước 6:  Thêm ad ID ở trong thẻ  </application>**

```xml
     <meta-data
            android:name="com.google.android.gms.ads.APPLICATION_ID"
            android:value="ca-app-pub-................." />  
```

📌 **Tham khảo dưới đây một vài loại ad**

```
  fun BaseFragment<*, *>.showBannerAdaptive(space: String, adContainer: ViewGroup, loadNew: Boolean = true) {
    AdmobBanner.show(
        space = space,
        adContainer = adContainer,
        layoutLoadingRes = R.layout.layout_loading_ad_view_common,
        forceLoadNewAdIfShowed = loadNew,
        lifecycle = null,
        adCallback = object : AdCallback {
            override fun onAdPaidValueListener(adsModel: AdModel, bundle: Bundle) {
                Tracking.logPairValueBanner(screenName, bundle)
            }

            override fun onAdOff(adsModel: AdModel, error: AdSDKError?) {
                adContainer.gone(true)
            }

        })
}


fun BaseActivity<*>.showBannerAdaptive(space: String, adContainer: ViewGroup, loadNew: Boolean = true) {
    AdmobBanner.show(
        space = space,
        adContainer = adContainer,
        layoutLoadingRes = R.layout.layout_loading_ad_view_common,
        forceLoadNewAdIfShowed = loadNew,
        lifecycle = null,
        adCallback = object : AdCallback {
            override fun onAdPaidValueListener(adsModel: AdModel, bundle: Bundle) {
                Tracking.logPairValueBanner(screenName, bundle)
            }

            override fun onAdOff(adsModel: AdModel, error: AdSDKError?) {
                adContainer.gone(true)
            }

        })
}


fun BaseFragment<*, *>.showBannerCollapsible(
    space: String,
    adContainer: ViewGroup,
) {
    AdmobBanner.show(
        space = space,
        adContainer = adContainer,
        layoutLoadingRes = R.layout.layout_loading_ad_view_common,
        forceLoadNewAdIfShowed = true,
        lifecycle = viewLifecycleOwner.lifecycle,
        adCallback = object : AdCallback {
            override fun onAdPaidValueListener(adsModel: AdModel, bundle: Bundle) {
                Tracking.logPairValueBanner(screenName, bundle)
            }

            override fun onAdOff(adsModel: AdModel, error: AdSDKError?) {
                adContainer.gone(true)
            }

        })
}

fun BaseFragment<*, *>.showNative(
    space: String,
    adContainer: ViewGroup,
    @LayoutRes layout: Int,
    loadNew: Boolean = false
) {

    AdmobNative.show(
        space = space,
        adContainer = adContainer,
        layoutRes = layout,
        forceLoadNewAdIfShowed = loadNew,
        layoutLoadingRes = R.layout.layout_loading_ad_view_common,
        adCallback = object : AdCallback {
            override fun onAdPaidValueListener(adsModel: AdModel, bundle: Bundle) {
                Tracking.logPairValueNative(screenName, bundle)
            }

            override fun onAdOff(adsModel: AdModel, error: AdSDKError?) {
                adContainer.gone(true)
            }

        })
}

fun BaseFragment<*, *>.showNativeCollapsible(
    space: String,
    adContainer: ViewGroup,
    @LayoutRes layoutRes: Int ,
    @LayoutRes collapsibleLayoutRes: Int 
) {
    AdmobNativeCollapsible.show(
        space = space,
        adContainer = adContainer,
        layoutLoadingRes = R.layout.layout_loading_ad_view_common,
        forceLoadNewAdIfShowed = true,
        layoutRes = layoutRes,
        collapsibleLayoutRes = collapsibleLayoutRes,
        lifecycle = viewLifecycleOwner.lifecycle,
        adCallback = object : AdCallback {
            override fun onAdPaidValueListener(adsModel: AdModel, bundle: Bundle) {
                Tracking.logPairValueBanner(screenName, bundle)
            }

            override fun onAdOff(adsModel: AdModel, error: AdSDKError?) {
                adContainer.gone(true)
            }

        })
}

fun BaseActivity<*>.showNative(
    space: String,
    adContainer: ViewGroup,
    @LayoutRes layout: Int,
    loadNew: Boolean = false
) {
    AdmobNative.show(
        space = space,
        adContainer = adContainer,
        layoutRes = layout,
        forceLoadNewAdIfShowed = loadNew,
        layoutLoadingRes = R.layout.layout_loading_ad_view_common,
        adCallback = object : AdCallback {
            override fun onAdPaidValueListener(adsModel: AdModel, bundle: Bundle) {
                Tracking.logPairValueNative(screenName, bundle)
            }

            override fun onAdOff(adsModel: AdModel, error: AdSDKError?) {
                adContainer.gone(true)
            }
        })
}


fun BaseFragment<*, *>.showInterNextAction(
    space: String = "ADMOB_Interstitial_Gerneral",
    curScreen: String = screenName,
    nextScreen: String = "",
    nextAction: () -> Unit
) {
    val status = AdsSDK.getStatusBySpace(space)
    if (status == AdStatus.LOADED) {
        AdmobInter.show(
            space,
            autoShowLoading = false,
            lifecycle = lifecycle,
            adCallback = object : AdCallback {

                override fun onAdPaidValueListener(adsModel: AdModel, bundle: Bundle) {
                    super.onAdPaidValueListener(adsModel, bundle)
                    Tracking.logPairValueInter(curScreen, nextScreen, bundle)
                }

                override fun onAdFailedToShowFullScreenContent(
                    adsModel: AdModel,
                    error: AdSDKError?
                ) {
                    super.onAdFailedToShowFullScreenContent(adsModel, error)
                    nextAction.invoke()
                }

                override fun onAdFailedToLoad(adsModel: AdModel, error: AdSDKError?) {
                    super.onAdFailedToLoad(adsModel, error)
                    nextAction.invoke()
                }

                override fun onAdOff(adsModel: AdModel, error: AdSDKError?) {
                    super.onAdOff(adsModel, error)
                    nextAction.invoke()
                }

                override fun onAdShowedFullScreenContent(adsModel: AdModel) {
                    super.onAdShowedFullScreenContent(adsModel)
                    delayHandler(200) {
                        nextAction.invoke()
                    }
                }

                override fun onAdDismissedFullScreenContent(adsModel: AdModel) {
                    super.onAdDismissedFullScreenContent(adsModel)
                    val timeRemote = AdmobInter.getTimeBetween()
                    val timeLoadAds = 4_000L
                    val timeDelay = (timeRemote - timeLoadAds).coerceAtLeast(timeLoadAds)
                    delayHandler(timeDelay) {
                        AdmobInter.load(space)
                    }
                }
            })
    } else {
        nextAction.invoke()
        if (AdsSDK.shouldLoadAdFullScreenIfMissing(space)) {
            AdmobInter.load(space)
        }
    }
}


fun BaseActivity<*>.showInterSplashAction(
    space: String,
    curScreen: String = screenName,
    nextScreen: String = "",
    nextAction: () -> Unit
) {

    AdmobInterSplash.loadAndShow(
        space = space,
        lifecycle = lifecycle,
        adCallback = object : AdCallback {

            override fun onAdPaidValueListener(adsModel: AdModel, bundle: Bundle) {
                super.onAdPaidValueListener(adsModel, bundle)
                Tracking.logPairValueInter(curScreen, nextScreen, bundle)
            }

            override fun onAdFailedToShowFullScreenContent(
                adsModel: AdModel,
                error: AdSDKError?
            ) {
                super.onAdFailedToShowFullScreenContent(adsModel, error)
                nextAction.invoke()
            }

            override fun onAdFailedToLoad(adsModel: AdModel, error: AdSDKError?) {
                super.onAdFailedToLoad(adsModel, error)
                nextAction.invoke()
            }

            override fun onAdOff(adsModel: AdModel, error: AdSDKError?) {
                super.onAdOff(adsModel, error)
                nextAction.invoke()
                Log.e(TAG, "onAdOff  ${adsModel.spaceName}")
            }

            override fun onAdDismissedFullScreenContent(adsModel: AdModel) {
                super.onAdDismissedFullScreenContent(adsModel)
                nextAction.invoke()
            }
        })
}


fun BaseActivity<*>.showOpenSplashAction(
    space: String,
    curScreen: String = screenName,
    nextScreen: String = "",
    nextAction: () -> Unit
) {

    AdmobOpenSplash.loadAndShow(
        space = space,
        lifecycle = lifecycle,
        adCallback = object : AdCallback {

            override fun onAdPaidValueListener(adsModel: AdModel, bundle: Bundle) {
                super.onAdPaidValueListener(adsModel, bundle)
                Tracking.logPairValueInter(curScreen, nextScreen, bundle)
            }

            override fun onAdFailedToShowFullScreenContent(
                adsModel: AdModel,
                error: AdSDKError?
            ) {
                super.onAdFailedToShowFullScreenContent(adsModel, error)
                nextAction.invoke()
            }

            override fun onAdFailedToLoad(adsModel: AdModel, error: AdSDKError?) {
                super.onAdFailedToLoad(adsModel, error)
                nextAction.invoke()
            }

            override fun onAdOff(adsModel: AdModel, error: AdSDKError?) {
                super.onAdOff(adsModel, error)
                nextAction.invoke()
            }

            override fun onAdDismissedFullScreenContent(adsModel: AdModel) {
                super.onAdDismissedFullScreenContent(adsModel)
                nextAction.invoke()
            }
        })
}

// chỉ cần gọi duy nhất ở 1 lần trong app không cần preload hay gì khác nữa cả
fun BaseActivity<*>.autoShowAdResume(space: String) {
    AdmobOpenResume.loadAndAutoShowIfAvailable(space, object : AdCallback {
        override fun onAdPaidValueListener(adModel: AdModel, bundle: Bundle) {
            Tracking.logPairValueOpen(
                ScreenTracking.currentScreen,
                ScreenTracking.currentScreen,
                bundle
            )
        }
    })
}

```

<!-- **Tham khảo [Example](https://gitlab.volio.vn/govo-tech/hd/Ads-Pro/-/tree/develop/app/src/main/java/com/android/fullhd/hd_ad) nếu có quyền :)** -->