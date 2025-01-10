# Bắt đầu

<span style="color: red;">Đây là hướng dẫn phiên bản từ 1.2.0 trở lên</span>.

<span style="color: gray;">Nếu bạn nâng cấp từ các bản 1.1.x lên thì cần thay json file config, callback. Các hàm khác vẫn giữ nguyên param</span>.

📌**Bước 1: Implement thư viện (xem ver mới nhất ở đầu page)**
```
implementation 'com.android.fullhd.adssdk:AdsPro:x.x.x'
```

```grovy
maven{
    url = "........"
    allowInsecureProtocol = true   
}
```

📌**Bước 2:  Tạo file cấu hình ad tĩnh dưới app trong thư mục app/src/main/assets/config.json**

- Hỗ trợ 2 định dạng json format v4 và v3 khuyến khích chọn V4 cho các app mới.

Format kiểu mới V4:
```json
{
  "versionNameDisable": "dev_2.0.0",
  "listAds": {
    "open_app_splash": [
      {
        "spaceName": "ADMOB_Open_Splash",
        "ids": [
          "ca-app-pub-3940256099942544/9257395921",
          "ca-app-pub-3940256099942544/9257395921",
          "ca-app-pub-3940256099942544/9257395921"
        ],
        "status": true
      },
      {
        "spaceName": "ADMOB_Open_Splash2",
        "ids": [
          "ca-app-pub-3940256099942544/9257395921",
          "ca-app-pub-3940256099942544/9257395921",
          "ca-app-pub-3940256099942544/9257395921"
        ],
        "status": true
      }
    ],
    "open_app_resume": [
      {
        "spaceName": "ADMOB_Open_Resume",
        "ids": [
          "ca-app-pub-3940256099942544/9257395921"
        ],
        "status": true
      }
    ],
    "interstitial": [
      {
        "spaceName": "ADMOB_Inter",
        "ids": [
          "ca-app-pub-3940256099942544/1033173712"
        ],
        "status": true
      }
    ],
    "interstitial_splash": [
      {
        "spaceName": "ADMOB_Inter_Splash",
        "ids": [
          "ca-app-pub-3940256099942544/1033173712"
        ],
        "status": true
      }
    ],
    "banner_300x250": [
      {
        "spaceName": "ADMOB_Banner_320x250",
        "ids": [
          "ca-app-pub-3940256099942544/6300978111"
        ],
        "status": true
      }
    ],
    "banner_adaptive": [
      {
        "spaceName": "ADMOB_Banner_Adaptive",
        "ids": [
          "ca-app-pub-8541569573502186/3727064079"
        ],
        "status": true
      }
    ],
    "banner_collapsible_bottom": [
      {
        "spaceName": "ADMOB_Banner_Collapsible_Bottom",
        "ids": [
          "ca-app-pub-3940256099942544/2014213617"
        ],
        "status": true
      }
    ],
    "banner_collapsible_top": [
      {
        "spaceName": "ADMOB_Banner_Collapsible_Top",
        "ids": [
          "ca-app-pub-3940256099942544/2014213617"
        ],
        "status": true
      }
    ],
    "native": [
      {
        "spaceName": "ADMOB_Native",
        "ids": [
          "ca-app-pub-3940256099942544/2247696110"
        ],
        "status": true
      }
    ],
    "native_collapsible": [
      {
        "spaceName": "ADMOB_Native_collapsible",
        "ids": [
          "ca-app-pub-3940256099942544/2247696110"
        ],
        "status": true
      }
    ],
    "reward_interstitial": [
      {
        "spaceName": "ADMOB_Rewarded_Inter",
        "ids": [
          "ca-app-pub-3940256099942544/5354046379"
        ],
        "status": true
      },
      {
        "spaceName": "ADMOB_Rewarded_Inter2",
        "ids": [
          "ca-app-pub-3940256099942544/5354046379"
        ],
        "status": true
      }
    ],
    "reward": [
      {
        "spaceName": "ADMOB_Rewarded",
        "ids": [
          "ca-app-pub-3940256099942544/5224354915",
          "ca-app-pub-3940256099942544/5224354917",
          "ca-app-pub-3940256099942544/5224354916"
        ],
        "status": true
      },
      {
        "spaceName": "ADMOB_Rewarded2",
        "ids": [
          "ca-app-pub-3940256099942544/5224354915",
          "ca-app-pub-3940256099942544/5224354917",
          "ca-app-pub-3940256099942544/5224354916"
        ],
        "status": true
      }
    ]
  }
}



```

Format kiểu cũ V3:
```json
{
  "versionNameDisable": "dev_2.0.0",
  "listAds": [
    {
      "spaceName": "ADMOB_Open_Resume",
      "adsType": "open_app_resume",
      "ids": [
        "ca-app-pub-3940256099942544/9257395921"
      ],
      "status": true
    },
    {
      "spaceName": "ADMOB_Open_Splash",
      "adsType": "open_app_splash",
      "ids": [
        "ca-app-pub-3940256099942544/9257395921"
      ],
      "status": true
    },
    {
      "spaceName": "ADMOB_Inter",
      "adsType": "interstitial",
      "ids": [
        "ca-app-pub-3940256099942544/1033173712"
      ],
      "status": true
    },
    {
      "spaceName": "ADMOB_Inter_Splash",
      "adsType": "interstitial_splash",
      "ids": [
        "ca-app-pub-3940256099942544/1033173715",
        "ca-app-pub-3940256099942544/1033173714",
        "ca-app-pub-3940256099942544/1033173712"
      ],
      "status": true
    },
    {
      "spaceName": "ADMOB_Banner_320x250",
      "adsType": "banner_300x250",
      "ids": [
        "ca-app-pub-3940256099942544/6300978113",
        "ca-app-pub-3940256099942544/6300978111",
        "ca-app-pub-3940256099942544/6300978112"
      ],
      "status": true
    },
    {
      "spaceName": "ADMOB_Banner_Adaptive",
      "adsType": "banner_adaptive",
      "ids": [
        "ca-app-pub-8541569573502186/3727064079",
        "ca-app-pub-3940256099942544/6300978111",
        "ca-app-pub-3940256099942544/6300978112"
      ],
      "status": true
    },
    {
      "spaceName": "ADMOB_Banner_Collapsible_Bottom",
      "adsType": "banner_collapsible_bottom",
      "ids": [
        "ca-app-pub-3940256099942544/2014213611",
        "ca-app-pub-3940256099942544/2014213612",
        "ca-app-pub-3940256099942544/2014213617"
      ],
      "status": true
    },
    {
      "spaceName": "ADMOB_Banner_Collapsible_Top",
      "adsType": "banner_collapsible_top",
      "ids": [
        "ca-app-pub-3940256099942544/2014213611",
        "ca-app-pub-3940256099942544/2014213612",
        "ca-app-pub-3940256099942544/2014213617"
      ],
      "status": true
    },
    {
      "spaceName": "ADMOB_Native",
      "adsType": "native",
      "ids": [
        "ca-app-pub-3940256099942544/2247696112",
        "ca-app-pub-3940256099942544/2247696110",
        "ca-app-pub-3940256099942544/2247696111"
      ],
      "status": true
    },
    {
      "spaceName": "ADMOB_Native_collapsible",
      "adsType": "native_collapsible",
      "ids": [
        "ca-app-pub-3940256099942544/2247696110",
        "ca-app-pub-3940256099942544/2247696112",
        "ca-app-pub-3940256099942544/2247696113"
      ],
      "status": true
    },
    {
      "spaceName": "ADMOB_Rewarded_Inter",
      "adsType": "reward_interstitial",
      "ids": [
        "ca-app-pub-3940256099942544/5354046379"
      ],
      "status": true
    },
    {
      "spaceName": "ADMOB_Rewarded",
      "adsType": "reward",
      "ids": [
        "ca-app-pub-3940256099942544/5224354915",
        "ca-app-pub-3940256099942544/5224354917",
        "ca-app-pub-3940256099942544/5224354916"
      ],
      "status": true
    }
  ]
}

```

📌**Bước 3:  Init AdSDK**

[Vui lòng bấm đây vào đọc kĩ "setTimeForceLoadNewNative(10_000)" dùng không thì bỏ qua](https://voliohungvv.github.io/Doc-Ad-Pro/ad/admob-native/#thoi-gian-giua-cac-lan-load-moi) 


[Vui lòng bấm đây vào đọc về ý nghĩa của các hàm callback](https://voliohungvv.github.io/Doc-Ad-Pro/ad/adsdk/#ang-ki-callback-tong-lang-nghe-moi-ad) 



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
        .loadAdsFromRemoteConfig(keyConfigAds = "ADMOB_V3", keyTimeBetweenAdInter = "timeBetweenMillisecond")
       // .setTimeForceLoadNewBanner(10_000) 
       // .setTimeForceLoadNewNative(10_000)

```

```kotlin

private  val TAG = "WiFiMapApplication"
private val adCallback = object : AdCallback {
        override fun onAdStartLoading(adsModel: AdModel, id: String) {
            super.onAdStartLoading(adsModel,id)
            Log.e(TAG, "onAdStartLoading: ${adsModel}")
        }

        override fun onAdClicked(adsModel: AdModel, id: String) {
            super.onAdClicked(adsModel,id)
            Log.e(TAG, "onAdClicked: ${adsModel}")
            toastDebug("click : ${adsModel.type} \n ${id.takeLast(4)}")

        }

        override fun onAdClosed(adsModel: AdModel, id: String) {
            super.onAdClosed(adsModel,id)
            Log.e(TAG, "onAdClosed: ${adsModel}")
        }

        override fun onAdDismissedFullScreenContent(adsModel: AdModel, id: String) {
            super.onAdDismissedFullScreenContent(adsModel,id)
            Log.e(TAG, "onAdDismissedFullScreenContent: ${adsModel}")
        }

        override fun onAdShowedFullScreenContent(adsModel: AdModel, id: String) {
            super.onAdShowedFullScreenContent(adsModel, id)
            Log.e(TAG, "onAdShowedFullScreenContent: ${adsModel}")
        }

        override fun onAdFailedToShowFullScreenContent(
            adsModel: AdModel,
            id: String,
            error: AdSDKError?
        ) {
            super.onAdFailedToShowFullScreenContent(adsModel, id,error)
            Log.e(TAG, "onAdFailedToShowFullScreenContent: ${adsModel} - ${error.toString()}")

        }

        override fun onAdFailedToLoad(adsModel: AdModel, id: String, error: AdSDKError?) {
            super.onAdFailedToLoad(adsModel,id, error)
            Log.e(TAG, "onAdFailedToLoad: ${adsModel} -  ${error.toString()}")
        }

        override fun onAdImpression(adsModel: AdModel, id: String) {
            super.onAdImpression(adsModel, id)
            Log.e(TAG, "onAdImpression: ${adsModel}")
        }

        override fun onAdLoaded(adsModel: AdModel, id: String) {
            super.onAdLoaded(adsModel, id)
            Log.e(TAG, "onAdLoaded: $adsModel")
            toastDebug("loaded : ${adsModel.type} \n ${id.takeLast(4)}")
        }

        override fun onAdOpened(adsModel: AdModel, id: String) {
            super.onAdOpened(adsModel, id)
            Log.e(TAG, "onAdOpened: ${adsModel}")
        }

        override fun onAdSwipeGestureClicked(adsModel: AdModel, id: String) {
            super.onAdSwipeGestureClicked(adsModel, id)
            Log.e(TAG, "onAdSwipeGestureClicked: ${adsModel}")
        }

        override fun onAdPaidValueListener(adsModel: AdModel, id: String, bundle: Bundle) {
            super.onAdPaidValueListener(adsModel, id, bundle)
            Log.e(TAG, "onAdPaidValueListener: ")
        }

        override fun onAdOff(adsModel: AdModel, id: String, error: AdSDKError?) {
            Log.e(TAG, "onAdOffxx: ${adsModel} -  ${error.toString()} ")
        }

    }

    private fun toastDebug(text: CharSequence) {
        if (BuildConfig.DEBUG) {
            Toast.makeText(this@WiFiMapApplication, text, Toast.LENGTH_SHORT).show()
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

```kotlin
private const val TAG = "AdUtils"

fun configLoadingAdFullScreen() {
    AdmobInter.setDialogConfigurator(
        resLayout = R.layout.layout_dialog_loading_inter_custom,
        configurator = object : DialogLoadingConfigurator {
            override val themeId: Int
                get() = android.R.style.Theme_Translucent_NoTitleBar_Fullscreen

            override fun onCreate(view: View?, dialog: Dialog) {
                view?.findViewById<TextView>(R.id.tvLoading)?.text = "Loading..."
            }

            override fun onShow(view: View?, dialog: Dialog) {
                dialog.apply {
                    window?.setLayout(
                        ViewGroup.LayoutParams.MATCH_PARENT,
                        ViewGroup.LayoutParams.MATCH_PARENT
                    )
                    window?.setBackgroundDrawableResource(android.R.color.transparent)
                    setCanceledOnTouchOutside(false)
                }
            }

        })
}

fun BaseFragment<*, *>.showBannerAdaptive(
    space: String,
    adContainer: ViewGroup,
    loadNew: Boolean = true
) {
    AdmobBanner.show(
        space = space,
        adContainer = adContainer,
        layoutLoadingRes = R.layout.layout_loading_ad_view_common,
        forceLoadNewAdIfShowed = loadNew,
        lifecycle = null,
        adCallback = object : AdCallback {
            override fun onAdPaidValueListener(adsModel: AdModel, id: String, bundle: Bundle) {
                Tracking.logPairValueBanner(screenName, bundle)
            }

            override fun onAdOff(adsModel: AdModel, id: String, error: AdSDKError?) {
                adContainer.gone(true)
            }

        })
}


fun BaseActivity<*>.showBannerAdaptive(
    space: String,
    adContainer: ViewGroup,
    loadNew: Boolean = true
) {
    AdmobBanner.show(
        space = space,
        adContainer = adContainer,
        layoutLoadingRes = R.layout.layout_loading_ad_view_common,
        forceLoadNewAdIfShowed = loadNew,
        lifecycle = null,
        adCallback = object : AdCallback {
            override fun onAdPaidValueListener(adsModel: AdModel, id: String, bundle: Bundle) {
                Tracking.logPairValueBanner(screenName, bundle)
            }

            override fun onAdOff(adsModel: AdModel, id: String, error: AdSDKError?) {
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
            override fun onAdPaidValueListener(adsModel: AdModel, id: String, bundle: Bundle) {
                Tracking.logPairValueBanner(screenName, bundle)
            }

            override fun onAdOff(adsModel: AdModel, id: String, error: AdSDKError?) {
                adContainer.gone(true)
            }

        })
}


fun BaseFragment<*, *>.showNativeCollapsible(
    space: String,
    adContainer: ViewGroup,
    @LayoutRes layoutRes: Int = R.layout.layout_native_80,
    @LayoutRes collapsibleLayoutRes: Int = R.layout.layout_ads_native_collapsible
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
            override fun onAdPaidValueListener(adsModel: AdModel, id: String, bundle: Bundle) {
                Tracking.logPairValueBanner(screenName, bundle)
            }

            override fun onAdOff(adsModel: AdModel, id: String, error: AdSDKError?) {
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
            override fun onAdPaidValueListener(adsModel: AdModel, id: String, bundle: Bundle) {
                Tracking.logPairValueNative(screenName, bundle)
            }

            override fun onAdOff(adsModel: AdModel, id: String, error: AdSDKError?) {
                adContainer.gone(true)
            }

        })
}


fun BaseActivity<*>.showNative(
    space: String,
    adContainer: ViewGroup,
    @LayoutRes layout: Int,
    loadNew: Boolean = false,
    onClickAd: () -> Unit = {}
) {
    AdmobNative.show(
        space = space,
        adContainer = adContainer,
        layoutRes = layout,
        forceLoadNewAdIfShowed = loadNew,
        layoutLoadingRes = R.layout.layout_loading_ad_view_common,
        adCallback = object : AdCallback {
            override fun onAdPaidValueListener(adsModel: AdModel, id: String, bundle: Bundle) {
                Tracking.logPairValueNative(screenName, bundle)
            }

            override fun onAdOff(adsModel: AdModel, id: String, error: AdSDKError?) {
                adContainer.gone(true)
            }

            override fun onAdClicked(adsModel: AdModel, id: String) {
                super.onAdClicked(adsModel, id)
                onClickAd.invoke()
            }
        })
}


fun BaseDialog<*>.showNative(
    space: String,
    screenName: String,
    adContainer: ViewGroup,
    @LayoutRes layout: Int,
    loadNew: Boolean = false
) {
    Log.e(TAG, "showNative: ${AdsSDK.getStatusBySpace(space)}")
    AdmobNative.show(
        space = space,
        adContainer = adContainer,
        layoutRes = layout,
        forceLoadNewAdIfShowed = loadNew,
        layoutLoadingRes = R.layout.layout_loading_ad_view_common,
        adCallback = object : AdCallback {
            override fun onAdPaidValueListener(adsModel: AdModel, id: String, bundle: Bundle) {
                Tracking.logPairValueNative(screenName, bundle)
            }

            override fun onAdOff(adsModel: AdModel, id: String, error: AdSDKError?) {
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

    if (BaseConstants.disableFirstClickInter) {
        nextAction.invoke()
        BaseConstants.disableFirstClickInter = false
        return
    }

    val status = AdsSDK.getStatusBySpace(space)
    if (status == AdStatus.LOADED) {
        AdmobInter.show(
            space,
            autoShowLoading = false,
            lifecycle = lifecycle,
            adCallback = object : AdCallback {

                override fun onAdPaidValueListener(adsModel: AdModel, id: String, bundle: Bundle) {
                    super.onAdPaidValueListener(adsModel, id, bundle)
                    Tracking.logPairValueInter(curScreen, nextScreen, bundle)
                }

                override fun onAdFailedToShowFullScreenContent(
                    adsModel: AdModel,
                    id: String,
                    error: AdSDKError?
                ) {
                    super.onAdFailedToShowFullScreenContent(adsModel, id, error)
                    nextAction.invoke()
                }

                override fun onAdFailedToLoad(adsModel: AdModel, id: String, error: AdSDKError?) {
                    super.onAdFailedToLoad(adsModel, id, error)
                    nextAction.invoke()
                }

                override fun onAdOff(adsModel: AdModel, id: String, error: AdSDKError?) {
                    super.onAdOff(adsModel, id, error)
                    nextAction.invoke()
                }

                override fun onAdShowedFullScreenContent(adsModel: AdModel, id: String) {
                    super.onAdShowedFullScreenContent(adsModel, id)
                    delayHandler(200) {
                        nextAction.invoke()
                    }
                }

                override fun onAdDismissedFullScreenContent(adsModel: AdModel, id: String) {
                    super.onAdDismissedFullScreenContent(adsModel, id)
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

            override fun onAdPaidValueListener(adsModel: AdModel, id: String, bundle: Bundle) {
                super.onAdPaidValueListener(adsModel, id, bundle)
                Tracking.logPairValueInter(curScreen, nextScreen, bundle)
            }

            override fun onAdFailedToShowFullScreenContent(
                adsModel: AdModel,
                id: String,
                error: AdSDKError?
            ) {
                super.onAdFailedToShowFullScreenContent(adsModel, id, error)
                nextAction.invoke()
            }

            override fun onAdFailedToLoad(adsModel: AdModel, id: String, error: AdSDKError?) {
                super.onAdFailedToLoad(adsModel, id, error)
                nextAction.invoke()
            }

            override fun onAdOff(adsModel: AdModel, id: String, error: AdSDKError?) {
                super.onAdOff(adsModel, id, error)
                nextAction.invoke()
                Log.e(TAG, "onAdOff  ${adsModel.spaceName}")
            }

            override fun onAdDismissedFullScreenContent(adsModel: AdModel, id: String) {
                super.onAdDismissedFullScreenContent(adsModel, id)
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

            override fun onAdPaidValueListener(adsModel: AdModel, id: String, bundle: Bundle) {
                super.onAdPaidValueListener(adsModel, id, bundle)
                Tracking.logPairValueInter(curScreen, nextScreen, bundle)
            }

            override fun onAdFailedToShowFullScreenContent(
                adsModel: AdModel,
                id: String,
                error: AdSDKError?
            ) {
                super.onAdFailedToShowFullScreenContent(adsModel, id, error)
                nextAction.invoke()
            }

            override fun onAdFailedToLoad(adsModel: AdModel, id: String, error: AdSDKError?) {
                super.onAdFailedToLoad(adsModel, id, error)
                nextAction.invoke()
            }

            override fun onAdOff(adsModel: AdModel, id: String, error: AdSDKError?) {
                super.onAdOff(adsModel, id, error)
                nextAction.invoke()
            }

            override fun onAdDismissedFullScreenContent(adsModel: AdModel, id: String) {
                super.onAdDismissedFullScreenContent(adsModel, id)
                nextAction.invoke()
            }
        })
}

fun BaseActivity<*>.autoShowAdResume(space: String) {
    AdmobOpenResume.setTimeDelayAutoPreloadNextAfterClose(5_000)
    AdmobOpenResume.loadAndAutoShowIfAvailable(space, object : AdCallback {
        override fun onAdPaidValueListener(adModel: AdModel, id: String, bundle: Bundle) {
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