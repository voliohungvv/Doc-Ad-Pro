# Cấu hình để load được ad thật 

:pushpin: **Để hiển thị được ad thật thì ứng dụng phải thoả mãi 2 điều kiện là isDebug = false và tên version phải hợp lệ  val regex = "^[0-9.]+$".toRegex()**

```kotlin
    AdsSDK.init(
        application: Application,
        pathAssetConfigAds: String,
        isDebug: Boolean = false // biến này mang giá trị false
    ): AdsSDK   
```


```Groovy
defaultConfig {
    applicationId "com.android.volio.adssdk"
    minSdk 24
    targetSdk 34
    versionCode 1
    versionName "1.0.0" // tên version này chỉ chứa chữ số và dấu "." . Không quan tâm thứ tự
    testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
}

```
