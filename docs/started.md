# Bắt đầu

**Bước 1: Implement thư viện (xem ver mới nhất ở đầu page)**
```
implementation 'com.android.fullhd.adssdk:AdsPro:1.0.0'
```

```grovy
maven{
    url = "http://repo.volio.vn/repository/maven-s3/"
    allowInsecureProtocol = true   
}
```

**Bước 2:  Tạo file cấu hình ad tĩnh dưới app trong thư mục app/src/main/assets/config.json**
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

**Bước 3:  Init AdSDK**

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
📌 **Bước 4:  Triển khai CMP trước khi load các ad khác**

```kotlin
    AdsSDK.showCMP(activity: AppCompatActivity, isTesting: Boolean = false, onDone: () -> Unit)
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

**Tham khảo [Example](https://gitlab.volio.vn/govo-tech/hd/Ads-Pro/-/tree/develop/app/src/main/java/com/android/fullhd/hd_ad) nếu có quyền :)**