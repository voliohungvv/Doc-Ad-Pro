# Thay đổi các version
- Các thay đổi update qua các version sẽ hiện ở đây từ mới nhất đến thấp nhất.


## Version 1.0.2
-  Fix lỗi ad colapsible crash khi tự động destroy tại  **override fun onDestroy(owner: LifecycleOwner)** xảy ra khi (load ở 1 activity và show ở một activity khác).
-  Add Unity ad mediation.


## Version 1.0.1
-  Fix lỗi ad native và ad banner load thừa trên dialog gây giảm show rate.
-  Fix lỗi timeout CMP tự động chuyển khi hết thời gian -> Chỉ timeout khi form CMP chưa hiện. Nếu hiện rồi thì huỷ timeout
