# Hướng dẫn sử dụng Viet DIY Focuser

Tài liệu này dành cho người dùng cuối. Nếu chỉ dùng focuser với NINA/ASCOM, bạn không cần quan tâm phần build driver hay code firmware.

Phiên bản khuyến nghị:

- Firmware: `1.2.7`
- Driver ASCOM: `1.23.0`
- Tên thiết bị trong ASCOM Chooser: `Viet DIY Focuser`

## 1. Cài đặt

### 1.1. Cài ASCOM Platform

Cài ASCOM Platform trước nếu máy chưa có.

### 1.2. Cài driver Viet DIY Focuser

Chạy file cài:

```text
DIY-EAF-ASCOM-Setup-1.23.0.exe
```

Sau khi cài xong, trong ASCOM Chooser sẽ có thiết bị:

```text
Viet DIY Focuser
```

## 2. Kết nối với NINA

1. Cắm dây USB từ máy tính vào EAF.
2. Mở NINA.
3. Vào phần Equipment / Focuser.
4. Chọn driver:

```text
Viet DIY Focuser
```

5. Bấm nút cấu hình / Setup.

## 3. Màn hình Setup

Các mục chính:

- `COM port`: chọn cổng COM của EAF.
- `Auto-detect DIY EAF`: tự tìm thiết bị nếu không biết COM.
- `Maximum position`: hành trình tối đa của focuser theo đơn vị UI step.
- `Speed`: tốc độ chạy focuser.
- `Motor tuning (advanced)`: tùy chỉnh motor nâng cao.
- `Reverse logical direction`: đảo chiều logic nếu chiều trong NINA bị ngược.
- `Hold motor when idle (25%)`: giữ motor sau khi dừng bằng 25% dòng chạy.
- `Set current position`: đặt vị trí hiện tại thành một giá trị logic.
- `Calibrate Maximum Travel`: đo hành trình tối đa.
- `Manual Control`: điều khiển tay để focus thô.
- `Save & Apply`: lưu và áp dụng cấu hình.

Nếu không thay đổi cấu hình, bấm `Save & Apply` sẽ đóng nhanh và không ghi lại firmware.

## 4. Thiết lập lần đầu

Làm theo thứ tự này:

1. Xoay núm focus của kính về gần điểm trong cùng. (Mặc định : xoay cùng chiều kim đồng hồ)
2. Lắp EAF vào núm focus.
3. Mở Setup của `Viet DIY Focuser`.
4. Chọn đúng COM hoặc tick `Auto-detect DIY EAF`.
5. Ở `Set current position`, nhập:

```text
0
```

6. Bấm `Set Position`.

Lúc này vị trí hiện tại được coi là điểm zero.

## 5. Calibrate Maximum Travel

Chức năng này dùng để đo hành trình focus tối đa.

1. Bấm `Calibrate Maximum Travel`.
2. Đảm bảo focuser đang ở điểm zero hoặc gần zero.
3. Bấm `Set Zero`.
4. Giữ nút `Hold to Move Out`.
5. Quan sát cơ khí khi focuser chạy ra ngoài.
6. Nhả nút trước khi chạm hard stop.
7. Khi thấy giá trị `Current travel` phù hợp, bấm `Use Current as Maximum`.

Khuyến nghị: không nên lấy sát điểm kẹt cơ khí. Nên giảm nhẹ Maximum position để tránh motor đẩy tới hard stop.

Ví dụ:

- Nếu đo được 130000 step, có thể đặt Maximum position khoảng 128000.

## 6. Maximum position và UI step

Với cấu hình mặc định hiện tại:

```text
1 vòng motor / núm focus = 3200 UI step
```

Ví dụ:

| Hành trình focus | Maximum position gợi ý |
| --- | ---: |
| 10 vòng | 32000 |
| 20 vòng | 64000 |
| 40 vòng | 128000 |

Lưu ý: đây là giá trị cho direct-drive, tức motor nối trực tiếp với núm focus. Nếu dùng pulley, dây curoa hoặc hộp số thì số step mỗi vòng núm focus sẽ thay đổi.

## 7. Microsteps

Trong `Motor tuning (advanced)`, có thể chọn:

- `1/8`
- `1/16`
- `1/32`

Người dùng bình thường không cần chỉnh mục này thường xuyên.

Với firmware hiện tại, đổi microstep không làm thay đổi hệ tọa độ mà NINA nhìn thấy:

```text
Position vẫn giữ nguyên
Maximum position vẫn giữ nguyên
NINA vẫn dùng như cũ
```

Microstep chỉ làm motor chạy mịn hơn hoặc thô hơn ở bên trong.

Khuyến nghị:

- Dùng mặc định nếu focuser đã chạy ổn.
- Dùng `1/32` nếu muốn motor mịn hơn.
- Nếu motor yếu, kêu hoặc chạy không ổn, thử giảm về `1/16` hoặc tăng `Top-speed delay`.

## 8. Speed và Top-speed delay

### Speed

`Speed` là tốc độ sử dụng thông thường.

Khuyến nghị:

- `Slow` hoặc `Normal` cho focus tinh.
- `Fast` hoặc `Fastest` khi cần chạy nhanh.

### Top-speed delay

Mục này nằm trong `Motor tuning (advanced)`.

- Số nhỏ hơn: motor chạy nhanh hơn.
- Số lớn hơn: motor chạy chậm hơn, dễ ổn định hơn.

Giá trị khuyến nghị:

```text
500 - 1000 us
```

Nếu motor kêu, giật hoặc mất bước, hãy tăng giá trị này.

## 9. Manual Control

`Manual Control` dùng để focus thô nhanh hơn thao tác nút trong NINA.

Trong cửa sổ Manual Control:

- `Fast (Coarse)`: chạy nhanh để chỉnh thô.
- `Slow (Fine)`: chạy chậm để chỉnh tinh.
- `Hold to Move In`: giữ để chạy vào trong.
- `Hold to Move Out`: giữ để chạy ra ngoài.

Motor chỉ chạy khi giữ nút. Nhả nút để dừng.

Luôn quan sát focuser khi chạy tay. Không giữ nút đến khi cơ khí chạm hard stop.

## 10. Set current position

`Set current position` chỉ đổi giá trị vị trí logic. Nó không làm motor quay.

Dùng khi:

- muốn đặt vị trí hiện tại là zero;
- muốn đồng bộ lại vị trí sau khi tháo/lắp cơ khí;
- muốn xóa cảnh báo vị trí approximate sau khi đã xác nhận vị trí thật.

Ví dụ:

```text
Set current position = 0
```

rồi bấm:

```text
Set Position
```

thì vị trí hiện tại được coi là zero.

## 11. Hold motor when idle

Nếu bật:

```text
Hold motor when idle (25%)
```

motor sẽ được giữ nhẹ sau khi dừng, giúp tránh trượt vị trí.

Ưu điểm:

- giữ vị trí tốt hơn;
- hữu ích nếu tải focus có xu hướng tự trôi.

Nhược điểm:

- motor có thể hơi ấm;
- tiêu thụ dòng nhiều hơn.

Nếu cơ khí không bị trượt, có thể tắt.

## 12. Cảnh báo Approx position

Nếu mất nguồn khi motor đang chạy, firmware sẽ khôi phục vị trí gần nhất đã lưu và báo:

```text
Approx position
```

Điều này nghĩa là vị trí hiện tại có thể hơi lệch so với thực tế.

Bạn vẫn có thể dùng tiếp, nhưng nếu cảnh báo xuất hiện nhiều lần, nên:

1. Đưa focuser về một vị trí đã biết.
2. Dùng `Set Position`.
3. Hoặc chạy lại `Calibrate Maximum Travel`.

## 13. Lỗi thường gặp

### Không kết nối được

Kiểm tra:

- đúng COM port chưa;
- đã đóng Serial Monitor chưa;
- dây USB có ổn không;
- thiết bị có hiện trong Device Manager không;
- driver có đúng là `Viet DIY Focuser` không.

Nếu không biết COM, tick `Auto-detect DIY EAF`.

### Motor kêu nhưng không quay

Nguyên nhân có thể:

- nguồn không đủ;
- dòng motor quá thấp;
- tốc độ quá cao;
- cơ khí bị kẹt;

Thử:

- tăng `Top-speed delay`;
- giảm `Speed`;
- kiểm tra nguồn cấp;
- kiểm tra khớp nối cơ khí;

### Motor quay ngược

Tick:

```text
Reverse logical direction
```

sau đó bấm `Save & Apply`.

### Đổi microstep nhưng thấy NINA không đổi Maximum position

Đây là hành vi đúng.

Microstep chỉ đổi độ mịn motor bên trong firmware. NINA vẫn dùng cùng hệ tọa độ logic.

## 14. Gợi ý cấu hình ban đầu

Với NEMA17 direct-drive:

```text
Maximum position: 128000
Speed: Normal
Microsteps: 1/32
Top-speed delay: 500 - 1000 us
Hold motor when idle: tùy cơ khí
```

Nếu motor chạy quá nhanh:

```text
Tăng Top-speed delay
```

Nếu motor yếu hoặc kêu:

```text
Giảm Speed
Tăng Top-speed delay
Kiểm tra nguồn
```

## 15. Khi cần hỗ trợ

Khi báo lỗi, nên gửi kèm:

- phiên bản driver;
- phiên bản firmware;
- ảnh màn hình Setup;
- microstep đang dùng;
- top-speed delay;
- mô tả cơ khí: nối trực tiếp, pulley hay hộp số.
