# Kiểm thử hiệu năng Website bằng Apache JMeter

## 1. Giới thiệu

Trong bài thực hành này, công cụ **Apache JMeter** được sử dụng để kiểm thử hiệu năng của một website.
Mục tiêu là mô phỏng nhiều người dùng truy cập đồng thời vào website và đo lường các chỉ số hiệu năng như:

* Thời gian phản hồi (Response Time)
* Số lượng request xử lý (Throughput)
* Tỷ lệ lỗi (Error Rate)

Website được sử dụng để kiểm thử:

```
https://en.wikipedia.org
```

---

# 2. Công cụ sử dụng

* Apache JMeter 5.6.3
* Java JDK
* Hệ điều hành: Windows

---

# 3. Cấu hình Test Plan

Trong JMeter, Test Plan được xây dựng với cấu trúc gồm:

```
HTTP Request Defaults
Thread Group 1 – Basic Load
Thread Group 2 – Heavy Load
Thread Group 3 – Custom Scenario
```

## HTTP Request Defaults

Cấu hình URL cơ sở của website:

```
Protocol: https
Server Name: en.wikipedia.org
```

Nhờ đó các HTTP Request chỉ cần khai báo **Path**.

---

# 4. Các kịch bản kiểm thử

## Thread Group 1 – Basic Load

Mục tiêu: kiểm thử tải cơ bản khi người dùng truy cập trang chủ.

Cấu hình:

```
Number of Users: 10
Ramp-up Period: 10 seconds
Loop Count: 5
```

Request thực hiện:

```
GET /
```

Kịch bản này mô phỏng nhiều người dùng truy cập trang chủ của website.

---

## Thread Group 2 – Heavy Load

Mục tiêu: kiểm thử khi có nhiều người dùng truy cập đồng thời.

Cấu hình:

```
Number of Users: 50
Ramp-up Period: 30 seconds
Loop Count: 1
```

Requests:

```
GET /
GET /wiki/Artificial_intelligence
```

Kịch bản này mô phỏng tải lớn khi nhiều người dùng truy cập website cùng lúc.

---

## Thread Group 3 – Custom Scenario

Mục tiêu: mô phỏng hành vi người dùng truy cập các bài viết khác nhau.

Cấu hình:

```
Number of Users: 20
Ramp-up Period: 10 seconds
Duration: 60 seconds
```

Requests:

```
GET /wiki/Python_(programming_language)
GET /wiki/Machine_learning
```

Kịch bản này mô phỏng người dùng đọc các bài viết về Python và Machine Learning.

---

# 5. Listeners sử dụng

Để thu thập và phân tích kết quả kiểm thử, các Listener sau được sử dụng:

```
Summary Report
View Results Tree
```

Trong đó:

**Summary Report** dùng để hiển thị các chỉ số hiệu năng như:

* Số lượng request
* Thời gian phản hồi trung bình
* Thời gian phản hồi tối thiểu / tối đa
* Throughput
* Tỷ lệ lỗi

**View Results Tree** dùng để kiểm tra chi tiết request và response.


# 6. Phân tích kết quả

Từ kết quả kiểm thử có thể rút ra một số nhận xét:

* Hệ thống xử lý thành công **40 request** từ **20 người dùng**.
* **Tỷ lệ lỗi bằng 0%**, cho thấy tất cả request đều được server xử lý thành công.
* Trang **Python** có thời gian phản hồi trung bình cao hơn so với trang **Machine Learning**.
* Sự khác biệt này có thể do kích thước nội dung trang Python lớn hơn hoặc có nhiều tài nguyên hơn.

---

# 7. Kết luận

Qua quá trình kiểm thử hiệu năng bằng Apache JMeter có thể kết luận rằng:

* Website có thể xử lý nhiều người dùng truy cập đồng thời mà không xảy ra lỗi.
* Thời gian phản hồi trung bình của các request đều dưới **1 giây**.
* Hệ thống hoạt động ổn định trong kịch bản kiểm thử đã thực hiện.

Bài thực hành giúp hiểu rõ hơn về cách:

* Thiết lập Test Plan trong JMeter
* Mô phỏng tải người dùng
* Thu thập và phân tích kết quả kiểm thử hiệu năng
