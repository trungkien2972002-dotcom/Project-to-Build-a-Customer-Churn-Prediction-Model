# Project-to-Build-a-Customer-Churn-Prediction-Model
# 📊 Banking Customer Churn Prediction Project

## 1. Tổng Quan Dự Án (Project Overview)
Dự án tập trung vào việc phân tích dữ liệu và xây dựng mô hình dự báo **tỷ lệ khách hàng rời bỏ dịch vụ (Churn)** tại một tổ chức ngân hàng. Việc giữ chân khách hàng cũ luôn mang lại hiệu quả chi phí cao hơn so với việc tìm kiếm khách hàng mới. Thông qua dự án này, chúng ta sẽ khai phá các mô hình hành vi, nhân khẩu học và các chỉ số tài chính để xác định sớm những khách hàng có nguy cơ rời đi, từ đó đề xuất các chiến lược tối ưu hóa trải nghiệm và giữ chân khách hàng (Customer Retention Strategies).

---

## 2. Tập Dữ Liệu & Các Đặc Trưng (Dataset & Features)
Tập dữ liệu chứa thông tin của **10,000 khách hàng** với 14 thuộc tính cốt lõi:

### Biến Mục Tiêu (Target Variable):
*   `Exited`: Khách hàng đã rời bỏ ngân hàng hay chưa (1: Đã rời đi, 0: Ở lại).

### Các Biến Độc Lập (Features):
*   **Thông tin định danh:** `RowNumber`, `CustomerId`, `Surname` (Thường được loại bỏ khi huấn luyện mô hình).
*   **Nhân khẩu học (Demographics):** 
    *   `Geography`: Quốc gia cư trú (Pháp, Đức, Tây Ban Nha).
    *   `Gender`: Giới tính (Nam, Nữ).
    *   `Age`: Tuổi của khách hàng.
*   **Hành vi & Sản phẩm (Behavioral):**
    *   `Tenure`: Số năm khách hàng đã gắn bó với ngân hàng.
    *   `NumOfProducts`: Số lượng sản phẩm tài chính khách hàng đang sử dụng.
    *   `HasCrCard`: Khách hàng có thẻ tín dụng hay không (1: Có, 0: Không).
    *   `IsActiveMember`: Khách hàng có hoạt động tích cực không (1: Có, 0: Không).
*   **Chỉ số tài chính (Financials):**
    *   `CreditScore`: Điểm tín dụng của khách hàng.
    *   `Balance`: Số dư tài khoản hiện tại.
    *   `EstimatedSalary`: Thu nhập ước tính của khách hàng.

---

## 3. Các Bước Triển Khai (Workflow)

### Bước 1: Phân tích Khám phá Dữ liệu (Advanced EDA)
*   Phân tích phân phối đơn biến, tập trung vào sự mất cân bằng của biến mục tiêu `Exited` (~20% Churn).
*   Phân tích lưỡng biến (Bivariate) để tìm mối tương quan giữa Nhân khẩu học/Tài chính với hành vi rời đi.
*   Phân tích đa biến (Multivariate) và trực quan hóa phân khúc sâu (ví dụ: Hành vi nhóm tuổi lớn tuổi có số dư cao tại thị trường Đức).

### Bước 2: Tiền xử lý & Kỹ nghệ Đặc trưng (Preprocessing & Feature Engineering)
*   Xử lý giá trị khuyết thiếu (nếu có) và chuẩn hóa dữ liệu số (`StandardScaler` / `MinMaxScaler`).
*   Mã hóa các biến danh mục (`One-Hot Encoding` cho `Geography`, `Gender`).
*   Xây dựng các đặc trưng phái sinh hiệu quả (ví dụ: Tỷ lệ số dư trên thu nhập `Balance_to_Salary_Ratio`).
*   Xử lý mất cân bằng dữ liệu bằng các kỹ thuật như **SMOTE** hoặc điều chỉnh trọng số giai cấp (`class_weight`).

### Bước 3: Huấn luyện & Đánh giá Mô hình (Modeling & Evaluation)
*   Thử nghiệm nhiều thuật toán phân lớp khác nhau: Logistic Regression, Random Forest, Gradient Boosting (XGBoost, LightGBM).
*   Tối ưu hóa siêu tham số (Hyperparameter Tuning) sử dụng `GridSearchCV` hoặc `RandomizedSearchCV`.
*   **Số liệu đánh giá (Metrics):** Do tập dữ liệu mất cân bằng, dự án ưu tiên tối ưu hóa **F1-Score** và **AUC-ROC** thay vì chỉ dựa vào Accuracy (Độ chính xác tổng thể).

---
