# Dự án Healthy Brain Network (HBN)

## Vấn đề cần giải quyết
Dự án này tập trung vào việc dự đoán mức độ nghiện Internet ở trẻ em và thanh thiếu niên bằng cách sử dụng dữ liệu từ Healthy Brain Network (HBN). Bộ dữ liệu này bao gồm các thông tin đa dạng như nhân khẩu học, đặc điểm thể chất và hoạt động, cho phép phân tích và dự đoán toàn diện.

## Thành viên nhóm
- **Phan Nguyễn An Hưng-22028098**  
- **Nguyễn Quốc Đạt-22028236-INT3405E_55**  
- **Võ Tá Thành-22028050**  


## Các bước thực hiện dự án

### 1. **Mô tả bộ dữ liệu**
Bộ dữ liệu HBN bao gồm dữ liệu thu thập từ khoảng 5.000 trẻ em và thanh thiếu niên từ 5-22 tuổi. Các loại dữ liệu chính:
- **Dữ liệu dạng bảng (CSV)**: Được thu thập bằng cách đo đạc trực tiếp.
- **Dữ liệu Actigraphy (Parquet)**: Một số đối tượng sẽ được đeo một thiết bị đo đạc để đo đạc các thông số trong vòng 30 ngày.

### 2. **Tiền xử lý và xây dựng đặc trưng**
- **Dữ liệu chuỗi thời gian:** Xử lý dữ liệu time series.
- **Giảm chiều dữ liệu:** Áp dụng AutoEncoder (dùng PyTorch) để nén dữ liệu time series.
- **Chọn lọc đặc trưng:** Kết hợp dữ liệu time series đã giảm chiều với dữ liệu dạng bảng, loại bỏ các đặc trưng dạng object, tạo ra các đặc trưng mới từ đặc trưng cũ. 

### 3. **Thiết kế và huấn luyện mô hình**

#### 3.1 Quy trình từ hồi quy đến phân loại
- **Bước 1:** Huấn luyện các mô hình hồi quy để dự đoán kết quả liên tục.
- **Bước 2:** Làm tròn kết quả dự đoán và tinh chỉnh bằng mô hình phân loại.

#### 3.2 Lựa chọn mô hình
1. **LGBMRegressor**
2. **XGBRegressor**
3. **CatBoostRegressor**
4. **XGBClassifier**

#### 3.3 Tích hợp mô hình
- Xây dựng mô hình VotingRegressor gồm LGBM, XGB và CatBoost.
- Tích hợp mô hình XGBClassifier để tinh chỉnh dự đoán từ hồi quy.

### 4. **Đánh giá và kiểm thử**
- Đánh giá mô hình bằng chỉ số Weighted Cohen’s Kappa.
- So sánh kết quả trên tập huấn luyện và kiểm tra để đảm bảo độ tin cậy của mô hình.

### 5. **Kết quả**
- Điểm submit: 0.413
