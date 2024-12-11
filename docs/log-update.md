# Thay đổi các version
- Các thay đổi update qua các version sẽ hiện ở đây từ mới nhất đến thấp nhất.

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
