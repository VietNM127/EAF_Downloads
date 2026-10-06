# DIY EAF Downloads

Trang tải firmware, ASCOM driver và hướng dẫn sử dụng cho DIY EAF.

## Tải xuống

- [ASCOM Driver 1.29.5](./DIY-EAF-ASCOM-Setup-1.29.5.exe)
- [Hướng dẫn sử dụng tiếng Việt](./USER_GUIDE_VI.md)

## Firmware hiện tại

- [Firmware AutoFocus 1.3.15 OTA payload](./AutoFocus-1.3.15-ota.bin)
- [Firmware AutoFocus 1.3.15 merged image](./AutoFocus-1.3.15-merged.bin)

Firmware `1.3.15` hoàn thiện điều khiển núm xoay HBX/EC16:

- Chỉnh từng nấc riêng lẻ: motor đi `100 UI step/nấc` ở tốc độ `Normal`, rồi dừng. Quãng đi không đổi khi chọn microstep `1/8`, `1/16` hoặc `1/32`.
- Có nấc tiếp theo cùng chiều trong vòng `0,5 giây`: chuyển sang quay liên tục, bắt đầu ở `Slowest`. Xoay nhanh nhiều nấc sẽ tăng dần đến `Fastest`.
- Mỗi `10` nấc nhanh sau nấc đầu tăng một mức; khoảng `40` nấc nhanh sau nấc đầu đạt `Fastest`. Với cùng nhịp xoay, thời gian tăng tốc dài gấp đôi bản `1.3.13`. Tốc độ tối đa vẫn dùng đúng `Top-speed delay` đã cấu hình.
- Khi quay liên tục, giữ tốc độ qua nhịp nghỉ lấy lại tay dưới `1,5 giây`. Hết `1,5 giây` không có tín hiệu xoay thì motor dừng và lần xoay sau bắt đầu bằng nấc chỉnh tinh.

Lưu ý: trong chế độ quay liên tục, motor có thể quay thêm tối đa `1,5 giây` sau khi ngừng xoay núm. Luôn quan sát cơ cấu và tránh chạm giới hạn cơ khí. Muốn trở lại chỉnh từng nấc, chờ motor dừng rồi xoay các nấc cách nhau hơn `0,5 giây`.

Bản này giữ hệ tọa độ `3200 UI step/vòng motor`, nội suy MicroPlyer và điều chỉnh dòng bằng VREF của TMC2208. HBX không thay đổi Speed đã lưu trong Setup và không can thiệp khi host đang di chuyển, calibration hoặc OTA.

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
