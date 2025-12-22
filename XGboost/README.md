## 🧠 Công nghệ & Thư viện sử dụng

### 🔹 Ngôn ngữ lập trình
- **Python 3.9+**

### 🔹 Thư viện chính
- **NumPy** – xử lý toán học và mảng số
- **Pandas** – xử lý dữ liệu dạng bảng
- **Scikit-learn** – chia tập dữ liệu, đánh giá mô hình
- **XGBoost** – mô hình học máy chính dùng để huấn luyện và dự đoán
- **Matplotlib & Seaborn** – trực quan hóa kết quả
- 
### XGBoost (Extreme Gradient Boosting)
Dự án sử dụng **XGBoost Classifier**, một thuật toán boosting mạnh mẽ với các ưu điểm:
- Hiệu quả cao với dữ liệu bảng (tabular data)
- Giảm overfitting tốt
- Huấn luyện nhanh và chính xác
- Phù hợp cho bài toán phân loại nhiều lớp (Home – Draw – Away)

### 🔹 Feature Engineering
- Lịch sử 5 trận gần nhất (win/draw rate, goals, shots)
- Lịch sử đối đầu giữa 2 đội
- **Elo Rating** (đánh giá sức mạnh đội bóng)
- Tier đội bóng (đội mạnh/yếu)

### 🔹 Visualization (phục vụ báo cáo)
- `matplotlib`
- `seaborn`

---

## 📊 Feature sử dụng

### 1️⃣ Lịch sử 5 trận gần nhất
- HomeWinRate5, AwayWinRate5  
- HomeDrawRate5, AwayDrawRate5  
- HomeAvgGoals5, AwayAvgGoals5  
- HomeAvgGoalsConceded5, AwayAvgGoalsConceded5  
- HomeHomeWinRate5, AwayAwayWinRate5  
- HomeAvgShotOnTarget5, AwayAvgShotOnTarget5  
- HomeAvgShotsConceded5, AwayAvgShotsConceded5  

### 2️⃣ Lịch sử đối đầu giữa 2 đội
- Head2Head_HomeWin  
- Head2Head_Draw  
- Head2Head_AwayWin  

### 3️⃣ Chỉ số sức mạnh
- EloHome
- EloAway
- EloDiff

---

## 🧪 Đánh giá mô hình
- Accuracy
- Precision
- Recall
- F1-score
- Confusion Matrix

