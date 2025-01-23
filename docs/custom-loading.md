# Custom loading

## Loading AdView

Với định dạng các loại ad view như AdNative, AdBanner thì các view loading sẽ được truyền dưới dạng reslayout, Nếu null sẽ sử dụng layout loading mặc định của thư viện. Áp dụng này sẽ có tác dụng với mỗi lần gọi hàm


📌 **Hàm mẫu**

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

## Loading Ad Full Screen

Với định dạng các loại ad full screen như AdInter, AdReward thì các view loading sẽ là dialog. Bạn có thể ghi đè layout mặc định hoặc thậm chí là truyền cả layout mà bạn muốn và cấu hình dialog hiển thị. Áp dụng sẽ tác động lên toàn bộ lớp Ad đó.


📌 **Hàm mẫu**

```kotlin
    AdmobInter.setDialogConfigurator(
            resLayout = R.layout.layout_dialog_loading_inter_custom, 
            configurator =  object : DialogLoadingConfigurator {
            override val themeId: Int
                get() = android.R.style.Theme_Translucent_NoTitleBar_Fullscreen

            override fun onCreate(view: View?, dialog: Dialog) {
                view?.findViewById<TextView>(R.id.tvLoading)?.text = "Loading..."
            }

            override fun onShow(view: View?, dialog: Dialog) {
                dialog.apply {
                    window?.setLayout(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT)
                    window?.setBackgroundDrawableResource(android.R.color.transparent)
                    setCanceledOnTouchOutside(false)
                }
            }

    })
```