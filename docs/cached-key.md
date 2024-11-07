# Cached key và cơ chế

Logic tất cả các ad sẽ được chưa trong các map cached theo một key cho trước để quản lí trạng thái vòng đời. Đối với thư viện này có 2 cơ chế cache theo 2 loại key là SpaceName và Id của Ad.

Với thư viện ad này một cached key sẽ lưu trữ object ad đó và sẽ đảm bảo load và show **nhiều lần** chỉ trên object đó trừ khi bạn sử dụng hàm **destroyAdBySpace** để loại bỏ ad ra khỏi map cached. Do vậy moi thông tin về space ad đó sẽ được lưu trữ từ khi app bắt đầu đến khi app bị kill

:pushpin: **Lưu ý**
- 2 quảng cáo có chung cached key thì bạn có thể dùng chung chúng trong mapCached
- Ở tầng ngoài bạn chỉ cần theo tác với spacename còn muốn chuyền đổi cần dùng hàm **setCachedBySpace**
- Nên xác định cấu hình cached trước khi bắt đầu load, show ad

:pushpin: **Cached theo space ( AdmobNative, AdmobBanner, AdmobOpenResume, AdmobOpenSplash )**

- Mặc định cached theo space và dùng chung space sẽ chính là dùng chung ad, có thể tách space  để load như một đối tượng ad mới.

:pushpin: **Cached theo ID ( AdmobInter, AdmobInterSplash, AdmobRewardInter, AdmobReward)**

- Mặc định cached theo ID và mục đích chính sẽ  chính là tách space của inter chung phục vụ mục đích bật tắt nhưng vẫn đảm bảo chỉ load và show chung 1 ID chung đó.

- Tuy là 2 spaceName khác nhau có chung ID và có cached theo ID. Nhưng bạn hiển thị log, floating debug view thư viện vẫn lọc chỉ các trạng thái của space đó chứ không phải là 2 space đó chung id sẽ chung các các callback và log.

- Đối với các ad full screen có hỗ trở hàm thay đổi giữa cached theo space hoặc cached theo ID. Tuỳ bạn sử dụng

```kotlin
    fun setCachedBySpace(value: Boolean): AdmobInter // true cached space, false cached theo id
```