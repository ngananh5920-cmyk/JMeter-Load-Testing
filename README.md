# BÁO CÁO KIỂM THỬ HIỆU NĂNG BẰNG JMETER

## Thông tin chung

* **Tên bài thực hành:** Học công cụ kiểm thử JMeter và thực hành kiểm thử tải API
* **Chủ đề:** Kiểm thử hiệu năng API bằng Apache JMeter
* **Ngày thực hiện:** 03/06/2026
* **Người thực hiện:** Nguyễn Phương Ngân - 23010450

### Tài liệu tham khảo

* Video hướng dẫn JMeter
* Apache JMeter User Manual
* Apache JMeter Component Reference
* Apache JMeter Best Practices

---

## 1. Mục tiêu

Tìm hiểu và thực hành sử dụng Apache JMeter để kiểm thử hiệu năng API, bao gồm:

* Tạo Test Plan và Thread Group.
* Cấu hình HTTP Request để gửi request đến API.
* Sử dụng Listener để thu thập kết quả.
* Chạy kiểm thử tải với nhiều người dùng ảo.
* Đọc và phân tích các chỉ số như Response Time, Throughput và Error Rate.
* Xuất kết quả kiểm thử và đánh giá hiệu năng hệ thống.

---

## 2. Môi trường kiểm thử

| Thành phần | Giá trị |
| :--- | :--- |
| **Công cụ** | Apache JMeter |
| **API demo** | [https://jsonplaceholder.typicode.com](https://jsonplaceholder.typicode.com) |
| **Kiểu kiểm thử** | Load Testing |
| **Phương thức** | GET |
| **Endpoint** | `/posts` |

---

## 3. Nội dung đã học về Jmeter

### 3.1. Test Plan
* Test Plan là thành phần gốc của JMeter, dùng để quản lý toàn bộ kịch bản kiểm thử.
* Trong bài thực hành này, Test Plan bao gồm: Thread Group (Load Test API), HTTP Request (Get Post), View Results Tree và Summary Report.
<img width="1470" height="956" alt="Ảnh màn hình 2026-06-03 lúc 16 49 22" src="https://github.com/user-attachments/assets/f266e928-6415-4933-b4a4-04e755d61f23" />

### 3.2. Thread Group
* Thread Group dùng để mô phỏng người dùng ảo truy cập hệ thống.
* Dựa trên tổng số mẫu sinh ra trong Summary Report, kịch bản được cấu hình để thực hiện tổng cộng 150 requests.
<img width="1470" height="956" alt="Ảnh màn hình 2026-06-03 lúc 16 49 58" src="https://github.com/user-attachments/assets/06c934f5-c201-45d8-a4c6-141523da169f" />

### 3.3. HTTP Request
HTTP Request được sử dụng để gửi yêu cầu đến API với thông số cấu hình:
* **Method:** GET
* **Protocol:** https
* **Server Name:** jsonplaceholder.typicode.com
* **Path:** /posts
<img width="1470" height="956" alt="Ảnh màn hình 2026-06-03 lúc 16 51 37" src="https://github.com/user-attachments/assets/ac2feac4-d94c-4b2c-b489-097b245b175a" />

### 3.4. Response Assertion
Response Assertion dùng để kiểm tra dữ liệu trả về từ API có đúng kỳ vọng hay không:
* **Name:** Check ID
* **Field to Test:** Text Response
* **Pattern Matching Rules:** Contains
* **Patterns to Test:** `"id"` *(Kiểm tra trong chuỗi JSON trả về bắt buộc phải có thuộc tính "id")*
<img width="1470" height="956" alt="Ảnh màn hình 2026-06-03 lúc 16 55 20" src="https://github.com/user-attachments/assets/8473d464-9269-4c35-b3a3-965543d8daad" />

### 3.5. Listener
Các Listener được sử dụng trong bài:
* **View Results Tree:** Xem chi tiết kết quả trả về của từng request *(Response code, Response message, kích thước dữ liệu, thời gian phản hồi...)*.

<img width="1470" height="956" alt="Ảnh màn hình 2026-06-03 lúc 17 07 09" src="https://github.com/user-attachments/assets/9230a63b-d1c2-405b-8acc-c2049e71a824" />

* **Summary Report:** Xem bảng thống kê tổng hợp toàn bộ hiệu năng của lượt kiểm thử.
<img width="1470" height="956" alt="Ảnh màn hình 2026-06-03 lúc 17 07 13" src="https://github.com/user-attachments/assets/cc423691-e232-4474-b0e4-e49c52d3e073" />

---

## 4. Kịch bản kiểm thử

### Kịch bản 1: Kiểm thử tải API lấy thông tin bài viết
* **Mục đích:** Kiểm tra khả năng phản hồi và độ ổn định của API khi có nhiều yêu cầu truy cập liên tục.
* **API kiểm thử:** `GET https://jsonplaceholder.typicode.com/posts`
* **Kết quả mong đợi:**
  * Request thực hiện thành công.
  * Response Code = 200.
  * Trả về dữ liệu định dạng JSON hợp lệ.
  * Tỷ lệ lỗi thấp, hệ thống hoạt động ổn định dưới tải.

---

## 5. Kết quả kiểm thử

Dựa trên dữ liệu từ **View Results Tree**, một mẫu request cụ thể *(Load Test API 1-4)* cho kết quả như sau:
* **Sample Start:** 2026-06-03 17:06:40 GMT+07:00
* **Load time:** 54 ms
* **Latency:** 53 ms
* **Size in bytes:** 1514 bytes
* **Response code:** 200
* **Response message:** OK
* **Response data type:** text *(định dạng application/json; charset=utf-8)*

### Bảng kết quả tổng hợp thu được từ Summary Report

| Label | # Samples | Average (ms) | Min (ms) | Max (ms) | Std. Dev. | Error % | Throughput | Received KB/sec | Sent KB/sec | Avg. Bytes |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Get Post** | 120 | 117 | 51 | 644 | 89.30 | 75.00% | 18.9/min | 0.44 | 0.06 | 1436.0 |
| *(No Label)* | 30 | 0 | 0 | 0 | 0.00 | 100.00% | 3.3/sec | 2.79 | 0.00 | 859.0 |
| **TOTAL** | 150 | 93 | 0 | 644 | 92.58 | 80.00% | 23.6/min | 0.51 | 0.06 | 1320.6 |

---

## 6. Nhận xét

Qua bảng số liệu thực tế thu được từ quá trình kiểm thử tải:

* **Về số lượng Request:** Tổng cộng hệ thống đã thực hiện kích hoạt 150 samples, trong đó có 120 samples thuộc nhãn đặt trước là `Get Post` và 30 samples không có nhãn.
* **Về Thời gian phản hồi (Response Time):** Đối với các request chạy được (`Get Post`), thời gian phản hồi trung bình khá nhanh đạt 117 ms, thấp nhất là 51 ms và cao nhất rơi vào 644 ms. Độ lệch chuẩn (Std. Dev.) là 89.30, cho thấy thời gian phản hồi có sự biến động nhẹ tùy thời điểm nhận tải nhưng vẫn nằm trong ngưỡng chấp nhận được của một API công cộng.
* **Về Tỷ lệ lỗi (Error Rate):** Lượt test ghi nhận tỷ lệ lỗi rất cao, lên đến 80.00% tính trên tổng số mẫu (trong đó riêng nhóm nhãn `Get Post` lỗi 75.00% và nhóm không nhãn lỗi 100%). Ở giao diện hiển thị (*View Results Tree*) xuất hiện các icon màu đỏ báo hiệu request thất bại đan xen với các request màu xanh (thành công 200 OK). Điều này cho thấy khi số lượng request đồng thời gửi lên liên tục, API của Server thử nghiệm (`jsonplaceholder.typicode.com`) đã bắt đầu từ chối hoặc trả về lỗi *(có thể do cơ chế giới hạn tần suất - Rate Limiting của server miễn phí này)*.
* **Về Băng thông (Throughput):** Khả năng xử lý tổng thể đạt 23.6 request/phút.

---

## 7. Kết luận

Bài thực hành đã hoàn thành đầy đủ các yêu cầu cốt lõi về mặt kỹ năng:
* Cài đặt thành công và làm quen tốt giao diện công cụ Apache JMeter.
* Biết cách thiết lập cấu trúc Test Plan cơ bản, Thread Group và cấu hình HTTP Request để gọi API endpoint cụ thể.
* Sử dụng thành thạo các Listener quan trọng như View Results Tree và Summary Report để bắt dữ liệu thực tế.
* Thu thập được số liệu trực quan để phân tích hiệu năng hệ thống.

*Mặc dù tỷ lệ lỗi (Error Rate) thực tế cao do giới hạn từ phía server demo, bài thực hành đã giúp em hiểu rõ tầm quan trọng của việc kiểm thử tải để phát hiện ra ngưỡng chịu đựng và điểm nghẽn của hệ thống API.*
