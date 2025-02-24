# 🏆 Cuộc Thi Toán Mô Hình 2023 - Vòng 1  

## 📌 Giới thiệu  
Báo cáo này trình bày mô hình tối ưu hóa lịch làm việc của nhân viên y tế tại bệnh viện, tập trung vào các mục tiêu:  
- **Phân công công việc công bằng** giữa các nhân viên.  
- **Đảm bảo đa dạng khoa** trong mỗi ca trực.  
- **Tối ưu hóa điểm thâm niên** để tăng hiệu quả làm việc.  
- **Cải thiện mô hình ban đầu** bằng thuật toán **Simulated Annealing**.  

---

## 🏗 Bố cục báo cáo  

### 1️⃣ **Thông tin về bài toán**  
- Xây dựng **thuật toán tối ưu hóa** nhằm **cân bằng phân công ca trực** cho bác sĩ và điều dưỡng.  
- Hướng đến **sự công bằng** và **duy trì chất lượng dịch vụ y tế**.  
- Nếu phân công không hợp lý, có thể gây ra:  
  - **Tăng tỷ lệ sai sót y khoa**.  
  - **Tăng mệt mỏi**, ảnh hưởng sức khỏe nhân viên.  
  - **Giảm chất lượng chăm sóc bệnh nhân**.  

---

### 2️⃣ **Ý tưởng giải pháp**  
Mục tiêu chính của mô hình:  
- **Phân phối công việc công bằng**:  
  - Số ngày trực của từng nhân viên gần với mức trung bình.  
- **Đảm bảo đa dạng khoa** trong mỗi ca trực.  
- **Đảm bảo cân bằng điểm thâm niên**, giúp nhân viên mới học hỏi kinh nghiệm.  

---

### 3️⃣ **Phương pháp tiếp cận bài toán**  
- **Hard Constraints** (ràng buộc cứng):  
  - Mỗi ca trực phải có đúng **1 bác sĩ Cộng I, 1 bác sĩ Cộng II, 2 điều dưỡng**.  
- **Soft Constraints** (ràng buộc mềm):  
  - Xoay vòng nhân sự hợp lý để tránh quá tải hoặc quá ít công việc.  
  - Mỗi ca trực nên có **đa dạng khoa** và **đa dạng về điểm thâm niên**.  

---

### 4️⃣ **Thang đo hiệu quả của mô hình**  
Hàm mất mát được tính theo công thức:  

$$
f(x) = \alpha_1 \sum_{i=1}^{n} (A_i - \mu_K)^2 + \alpha_2 \sum_{i=1}^{m} (4-K_i)^2 + 
\alpha_3 \sum_{i=1}^{m} (\mu_{\text{đtnbsI}} + \mu_{\text{đtnbsII}} + 2\mu_{\text{đtndd}} - 
\text{đtnbsI} - \text{đtnbsII} - \text{đtnddI} - \text{đtnddII})^2
$$

Các biến số:  
- $n$: Tổng số nhân viên.  
- $m$: Tổng số ca trực cần sắp xếp.  
- $A_i$: Số ca trực được giao cho nhân viên $i$.  
- $\mu_K$: Trung bình số ca trực của tất cả nhân viên.  
- $K_i$: Số khoa có bác sĩ trực trong ca thứ $i$.  

---

### 5️⃣ **Cải tiến mô hình với Simulated Annealing**  
Thuật toán **Simulated Annealing** được sử dụng để **tối ưu hóa phân công công việc**, giảm giá trị của hàm mất mát.  
- **Simulated Annealing giúp thoát khỏi cực trị địa phương**, tìm kiếm lời giải tối ưu.  
- Công thức xác suất chấp nhận lời giải kém hơn:  

$$
P(E_{\text{sau}} - E_{\text{trước}}) = e^{-\frac{E_{\text{sau}} - E_{\text{trước}}}{T}}
$$

- **Kết quả tối ưu:**  
  - Hàm mất mát giảm từ **884.05** xuống **501.61249**.  
  - Thời gian thực thi: **~82 giây với 62 ca trực** và **10,000 lần lặp**.  

---

### 6️⃣ **Bảng kết quả phân công ca trực**  
- **Số ngày làm việc của bác sĩ và điều dưỡng phù hợp với ràng buộc mềm**.  
- **Mỗi ca trực có từ 2-4 khoa tham gia**, giúp đảm bảo **chất lượng chăm sóc đa khoa**.  
- **Mức thâm niên trong các ca trực được cân bằng**, giúp nhân viên mới học hỏi từ đồng nghiệp.  

---

### 7️⃣ **Tính tổng quát và khả thi của giải pháp**  
- **Thích ứng khi có thay đổi về nhân sự hoặc số lượng ca trực**.  
- **Dễ dàng bổ sung thêm ràng buộc mềm**, chỉ cần sửa hàm mất mát mà không phải viết lại thuật toán.  
- **Có thể tinh chỉnh các tham số** $\alpha_1, \alpha_2, \alpha_3$ để phản ánh yêu cầu thực tế.  

⏳ **Thời gian thực thi**: Với **62 ca trực**, chạy **10,000 lần lặp**, **hoàn thành trong ~82 giây**.  

---

## 📂 **Các tệp tin quan trọng**  
- 📁 **`LossFunction.ipynb`** - Phân tích hàm mất mát.  
- 📁 **`InitialModel.ipynb`** - Mô hình khởi tạo phân công ngẫu nhiên.  
- 📁 **`ImproveModel.ipynb`** - Mô hình tối ưu hóa với **Simulated Annealing**.  
- 📁 **`best_schedule_sa_improved_analytics.csv`** - Kết quả lịch phân công tối ưu.  

---

## 📚 **Tài liệu tham khảo**  
1. **Lập lịch làm việc & tối ưu hóa nhân sự**: [P. De Bruecker et al., 2015](https://doi.org/fake-link)  
2. **Simulated Annealing trong thực tế**: [YouTube Video](https://youtu.be/P_cgr7Y56b4?si=OETKVJaq2o9ZW7RD)  
3. **Tác động của lịch trực không hợp lý đến chất lượng bệnh viện**: [Medely Research](https://medely.com/blog/impact-of-staffing-shortages-on-patient-care/)  

---

## 🎉 **Lời cảm ơn**  
Thay mặt nhóm **Sparkle**, chúng tôi xin gửi lời cảm ơn đến **BTC Cuộc Thi Toán Mô Hình 2023** đã tạo ra một sân chơi bổ ích. Cuộc thi giúp chúng tôi ứng dụng toán học vào thực tế, phát triển kỹ năng lập mô hình và tối ưu hóa.  

😊 **Mọi góp ý, xin gửi về nhóm Sparkle! 🚀**  
