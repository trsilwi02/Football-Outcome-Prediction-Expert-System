# ⚽ Dự đoán Kết quả Bóng đá Premier League sử dụng KNN

## 📋 Mô tả
Dự án này sử dụng thuật toán **K-Nearest Neighbors (KNN)** để dự đoán kết quả trận đấu Premier League dựa trên các chỉ số thống kê và phong độ của hai đội. Mô hình được tối ưu hóa thông qua **Grid Search** và **Time-Series Cross-Validation** để đảm bảo tính chính xác và khả năng tổng quát hóa.

## 🎯 Mục tiêu
- Dự đoán kết quả trận đấu: **Home Win (1)**, **Draw (0)**, hoặc **Away Win (2)**.
- Phân tích ảnh hưởng của các yếu tố: phong độ, thống kê ghi bàn, cú sút, lịch sử đối đầu.
- Tìm ra cấu hình tham số tối ưu cho mô hình KNN.

---

## 📊 Dữ liệu
### 🔹 Nguồn dữ liệu
- **File**: `epl_24-25.csv` (Dữ liệu gốc từ Premier League).
- **Nội dung**: Dữ liệu trận đấu Premier League mùa giải 2023-2024 và 2024-2025.
- **Số lượng**: Khoảng 730 trận đấu.

### 🔹 Các cột dữ liệu chính
- `MatchDate`: Ngày thi đấu.
- `HomeTeam`, `AwayTeam`: Tên hai đội thi đấu.
- `FullTimeResult`: Kết quả thực tế (H/D/A).
- `HomeShotsOnTarget`, `AwayShotsOnTarget`: Chỉ số sút trúng đích.

---

## 🧠 Features Engineering
Mô hình sử dụng **16 features** quan trọng đã được chuẩn hóa bằng **StandardScaler**:

### 1️⃣ Phong độ & Bàn thắng (Rolling 5 matches)
- `HomeWinRate5, AwayWinRate5`: Tỷ lệ thắng hiện tại.
- `HomeDrawRate5, AwayDrawRate5`: Tỷ lệ hòa hiện tại.
- `HomeAvgGoals5, AwayAvgGoals5`: Hiệu suất ghi bàn trung bình.
- `HomeAvgGoalsConceded5, AwayAvgGoalsConceded5`: Khả năng phòng ngự (bàn thua).

### 2️⃣ Chỉ số tấn công (Rolling 5 matches)
- `HomeAvgShotOnTarget5, AwayAvgShotOnTarget5`: Khả năng dứt điểm chính xác.
- `HomeAvgShotsConceded5, AwayAvgShotsConceded5`: Khả năng hạn chế đối phương dứt điểm.
- `HomeHomeWinRate5, AwayAwayWinRate5`: Chỉ số sức mạnh khi đá đúng sở trường sân nhà/khách.

### 3️⃣ Lịch sử đối đầu & Sân bãi
- `Head2Head_HomeWinRate5, Head2Head_DrawRate5, Head2Head_AwayWinRate5`: Tỷ lệ thắng/hòa/thua trong 5 lần chạm trán gần nhất giữa 2 đội.

> ⚠️ **Xử lý Data Leakage**: Sử dụng kỹ thuật `.shift(1)` để đảm bảo mô hình chỉ học từ dữ liệu của các trận đấu đã diễn ra trước đó.

---

## 🔍 Phương pháp đánh giá
- **Tiền xử lý**: Sử dụng `StandardScaler` để đưa các đặc trưng về cùng một quy mô.
- **Phân chia dữ liệu**: Sử dụng `TimeSeriesSplit` (3 folds) để giữ đúng trình tự thời gian.
- **Tối ưu hóa**: `GridSearchCV` để quét qua các giá trị K và Distance Metrics.

## 🧪 Đánh giá mô hình
Mô hình hiển thị kết quả trực quan qua:
- **Accuracy Score**: Độ chính xác tổng thể trên tập Test.
- **Classification Report**: Chi tiết Precision, Recall, F1-score cho từng lớp (0, 1, 2).
- **Confusion Matrix**: Biểu đồ Heatmap (Seaborn) thể hiện sự nhầm lẫn giữa các dự đoán.

---

## 📈 Kết quả tốt nhất
Dựa trên kết quả chạy thực tế từ Grid Search:
- 🔹 **K (n_neighbors)** = 19
- 🔹 **Metric** = chebyshev
- 🔹 **Weights** = distance
- 🔹 **CV Accuracy** = 0.5046 (~50.5%)
