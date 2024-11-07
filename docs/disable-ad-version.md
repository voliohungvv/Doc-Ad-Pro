# Cấu hình tắt ad theo version chỉ định

:pushpin: **Cấu hình thông qua biến versionNameDisable**

Tắt các version chỉ định thông qua versionNameDisable trong file config.

```xml
"versionNameDisable": "2.0.0" // tắt version 2.0.0

"versionNameDisable": "2.0.0-2.2.1"// tắt 2 version 2.0.0 và 2.2.1 có thể dùng kí tự - hoặc | hoặc ,  đều tương đương nhau nhưng chỉ dùng 1 kí tự

"versionNameDisable": "*" // tắt tất cả các version

```