
# Remote Layout Native
  
📌  Cấu hình Bật Remote Layout Native
Mặc định tính năng này bị tắt.
Để bật/tắt tính năng trong code :
```kotlin  
 DynamicLayoutHelper.setActiveRemoteLayout(true)
```
Hoặc bật/tắt qua remote config :
```kotlin  
 AdsSDK.loadAdsFromRemoteConfig(
				keyEnableRemoteLayoutNative = "enableRemoteLayoutNative")
```
##  Cách  remote config layout Native thường : ##

**Bước 1** . Key remote config chính là nameSpace trong file config Ads: 

- Vd: Muốn remote layout cho Admob_Native_Language thì cần tạo key remote config có tên là "Admob_Native_Language" 

**Bước 2** . Patse nội dung file XML lên Default value -> save.

##  Cách  remote config layout Native Collapsible: ##

**Bước 1** . Key remote config chính là nameSpace trong file config Ads + Endfix.

- A. đối với layout nhỏ Endfix =  "_collapse" 
    - vd : Admob_Collapsible_Native  -> Admob_Collapsible_Native_collapse

- B. đối với layout to/sổ lên Endfix =  "_expand" 
    - vd : Admob_Collapsible_Native  -> Admob_Collapsible_Native_expand

**Bước 2** . Patse nội dung file XML lên Default value


## Lưu ý  

📌 **Phải set cứng Height cho root view. Không support databinding**

📌 Layout Xml có thể referent đến tất cả các resource đã có sẵn trong app như @dimen / @drawable/ @color => **Chỉ có thể dùng các resource có sẵn này để viết layout mới.**


📌  **Luôn luôn test/preview layout trước khi đưa lên remote :**

- 1 . Copy layout xml sang thư mục **@raw**

- 2 . Sử dụng phương thức **previewForTesting()** để xem trước Layout.

```kotlin  
 DynamicLayoutHelper.previewForTesting(viewGroup: ViewGroup, @RawRes rawXml: Int)
```
 
## Supported Views & Attributes

This module supports inflating and applying attributes for several common Android views.  
Below is the list of supported view types and their attributes.

----------

### View

-   `layout_width`, `layout_height`
    
-   `background`: `@drawable/…`, `@color/…`, `#hex`
    
-   `backgroundTint`: `@color/…`, `#hex`
    
-   `alpha`
    
-   `margin`
    
-   `padding`
    

----------

### TextView

-   `style`
    
-   `fontFamily`: `@font/…`
    
-   `textColor`: `@color/…`, `#hex`
    
-   `lines`: `Int`
    
-   `maxLines`: `Int`
    
-   `ellipsize`: `end`, `start`, `middle`
    
-   `gravity`
    
-   `textSize`: `@dimen/…`, `sp`, `dp`, `px`
    
-   `text`: `@string/…`
    
-   `hint`: `@string/…`
    
-   `lineSpacingExtra`
    
-   `lineSpacingMultiplier`
    
-   `letterSpacing`
    
-   `includeFontPadding`
    

----------

### FrameLayout

-   `layout_gravity`
    

----------

### CardView

-   `cardBackgroundColor`: `@color/…`, `#hex`
    
-   `cardCornerRadius`: `@dimen/…`, `dp`, `px`
    
-   `cardElevation`: `@dimen/…`, `dp`, `px`
    

----------

### MaterialCardView

-   `cardBackgroundColor`: `@color/…`, `#hex`
    
-   `cardCornerRadius`: `@dimen/…`, `dp`, `px`
    
-   `cardElevation`: `@dimen/…`, `dp`, `px`
    
-   `strokeWidth`: `@dimen/…`, `dp`, `px`
    
-   `strokeColor`: `@color/…`, `#hex`
    

----------

### LinearLayout

-   `orientation`
    
-   `weightSum`
    
-   `layout_gravity`
    
-   `layout_weight`
    

----------

### ConstraintLayout

-   `layout_constraintDimensionRatio`
    
-   `layout_constraintWidth_percent`
    
-   `layout_constraintHeight_percent`
    
-   `layout_constraintHorizontal_bias`
    
-   `layout_constraintVertical_bias`
    
-   **Basic constraints**:
    
    -   `layout_constraintTop_toTopOf`
        
    -   `layout_constraintTop_toBottomOf`
        
    -   `layout_constraintBottom_toTopOf`
        
    -   `layout_constraintBottom_toBottomOf`
        
    -   `layout_constraintStart_toStartOf`
        
    -   `layout_constraintStart_toEndOf`
        
    -   `layout_constraintEnd_toStartOf`
        
    -   `layout_constraintEnd_toEndOf`
        

----------

### ImageView

-   `src`: `@drawable/…`
    
-   `scaleType`
    

----------

