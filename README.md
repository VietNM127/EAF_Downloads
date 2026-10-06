# DIY EAF Downloads

Trang tải firmware, ASCOM driver và hướng dẫn sử dụng cho DIY EAF.

## Tải xuống

- [ASCOM Driver 1.29.5](./DIY-EAF-ASCOM-Setup-1.29.5.exe)
- [Hướng dẫn sử dụng tiếng Việt](./USER_GUIDE_VI.md)

## Firmware hiện tại

- [Firmware AutoFocus 1.3.7 OTA payload](./AutoFocus-1.3.7-ota.bin)
- [Firmware AutoFocus 1.3.7 merged image](./AutoFocus-1.3.7-merged.bin)

Firmware `1.3.7` cải tiến núm điều khiển HBX/EC16: xoay liên tục nối dài hành trình đang chạy; xoay chậm dùng tốc độ thấp, xoay nhanh nhiều nấc tăng dần đến mức `Fastest`, theo `Top-speed delay` đã cấu hình. Bản này giữ nội suy MicroPlyer và điều chỉnh dòng bằng VREF của TMC2208.

Box cũ không có cổng 3,5 mm tự mặc định tắt HBX khi cập nhật, người dùng không cần cấu hình. Box có cổng được nhà sản xuất bật sẵn; OTA giữ nguyên cờ này. Cảm biến nhiệt DS18B20 chưa được hỗ trợ trong bản này.

## Firmware cũ

- [Firmware AutoFocus 1.2.10 OTA payload](./AutoFocus-1.2.10-ota.bin)
- [Firmware AutoFocus 1.2.10 merged image](./AutoFocus-1.2.10-merged.bin)

Ghi chú:

- File `*-ota.bin` là application binary dùng cho Serial OTA.
- File `*-merged.bin` là ảnh flash đầy đủ 4 MB, dùng cho flash thủ công hoặc recovery.
- Người dùng cập nhật firmware qua nút `Firmware Update...` trong Setup; driver tự tải bản mới từ manifest, không cần chọn file `.bin` thủ công.
- Nút này cập nhật firmware của box. ASCOM driver vẫn được cài bằng file `.exe` riêng.

## Cài đặt

Vui lòng đọc hướng dẫn sử dụng trước khi cập nhật firmware hoặc cài đặt driver.
