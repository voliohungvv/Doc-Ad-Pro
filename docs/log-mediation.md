# Thay đổi các version
Đối với version 1.2.11 trở đi đang sử dụng admob 23.2.0 mọi logic sẽ tương ứng với version 1.3.1 trở đi sử dụng admob 24.0.0


## Version 1.2.6 -> 1.2.xx đang sử dụng admob 23.2.0
- Sử dụng mediation sau
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


## Version 1.3.1 -> 1.3.xx đang sử dụng admob 24.0.0
- Sử dụng mediation sau
```gradle

    api 'com.google.ads.mediation:facebook:6.17.0.0'
    api('com.facebook.android:facebook-android-sdk:latest.release') {
        exclude group: 'com.google.zxing'
    }
    api("com.unity3d.ads:unity-ads:4.13.2")//
    api("com.google.ads.mediation:unity:4.13.2.0")//
    api 'com.google.ads.mediation:applovin:13.1.0.1'///
    api 'com.google.ads.mediation:vungle:7.4.3.1'///
    api 'com.google.ads.mediation:pangle:6.5.0.5.0'///
    api 'com.google.ads.mediation:mintegral:16.9.51.0'///
    api 'com.google.ads.mediation:ironsource:8.7.0.1' ///

```