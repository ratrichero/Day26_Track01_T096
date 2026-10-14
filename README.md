# BÁO CÁO THỰC HÀNH LAB: THIẾT KẾ & ÁP DỤNG SẢN PHẨM AI (AI ADOPTION)
## DAY 26 – TRACK 01 | NHÓM: T096
**Dự án:** PricePolicy AI Agent – Nền tảng Định giá & Bảo chứng Chính sách Bán hàng Bất động sản VLandFuture  

---

### 1. Bảng Thành viên & Đóng góp Phản biện chéo

| Họ tên | MSSV | Phần phụ trách | Góp ý đã đưa cho nhóm bạn |
| :--- | :---: | :--- | :--- |
| **Tạ Việt Cường** | **2A202602560** | Khóa phạm vi sản phẩm; Chẩn đoán nguyên nhân gốc (Gartner-Lite, Mollick, ADKAR); Tái thiết kế quy trình AS-IS / TO-BE; Lập lộ trình Gate 30–60–90 ngày; Xây dựng Dashboard hành động v1 & v2; Soạn thảo Memo quyết định. | **Phản biện Nhóm 05 (Trợ lý Tra cứu Vận hành CSKH):** Chỉ số *"Số lượt câu hỏi tra cứu"* chỉ là vanity metric dễ gây thiên lệch. Đề xuất nhóm bạn chuyển đổi sang *"Tỷ lệ tra cứu có trích nguồn giải quyết dứt điểm vấn đề của khách hàng mà không cần leo thang (First Contact Resolution without Escalation)"* và bổ sung cơ chế kiểm soát văn bản chính sách hết hạn (Time-sensitive Policy Deprecation). |

---

### 2. Phạm vi Sản phẩm (Scope)
* **1 Sản phẩm AI cụ thể:** **PricePolicy AI Agent** – Nền tảng AI hỗ trợ ra quyết định định giá thương mại, phát hiện xung đột điều khoản và bảo chứng chính sách bán hàng bất động sản.
* **1 Nhóm người dùng chính:** **Nhân viên Kinh doanh Tuyến đầu (Sales Executive)** tại các sàn phân phối và sự kiện mở bán tập trung (kèm vai trò liên đới: Quản lý Bán hàng - Sales Manager).
* **3 Quy trình nghiệp vụ cốt lõi:**
  1. *Quy trình tra cứu chính sách theo ngày giao dịch & xác định điều kiện ưu đãi (Time-Travel Policy & Eligibility Verification).*
  2. *Quy trình mô phỏng song song 3 kịch bản thanh toán & đề xuất phương án tối ưu dòng tiền (Scenario Simulation & Cashflow Optimization).*
  3. *Quy trình thẩm định, đóng gói hồ sơ & phê duyệt báo giá thương mại (HITL Gate & Immutable Audit Snapshot).*

---

### 3. Nguyên nhân Gốc (Root Cause Diagnosis)
* **Nguyên nhân gốc 1 (Độ tin cậy & Tâm lý người dùng - Khung ADKAR & Gartner-Lite):** Sales ngại sử dụng và không dám tin kết quả của AI vì hệ thống ban đầu thiếu cơ chế trích dẫn căn cứ điều khoản hai chiều (Why/Why-not), dẫn tới nỗi sợ bị đền tiền hoặc trừ hoa hồng cá nhân nếu AI tính nhầm chiết khấu phức tạp.  
  *(Căn cứ & Bằng chứng: Phỏng vấn sâu 15 sales tuyến đầu cho thấy 13/15 người khẳng định sợ bị trừ hoa hồng nên thà dùng file Excel tự lập; Log hệ thống tháng đầu ghi nhận 85% tài khoản bỏ xó sau đúng 1 lần đăng nhập training).*
* **Nguyên nhân gốc 2 (Quy trình & Phân định trách nhiệm - Khung Mollick & Gartner-Lite):** Quy trình vận hành chưa cưỡng chế việc sử dụng AI, Quản lý bán hàng vẫn chấp nhận duyệt giá "niềm tin" qua ảnh chụp Zalo gửi riêng lẻ, đồng thời tổ chức thiếu vai trò Data Owner phụ trách tính cập nhật của các phụ lục chính sách khẩn cấp.  
  *(Căn cứ & Bằng chứng: 78% báo giá phát hành vẫn được lập thủ công; doanh nghiệp ghi nhận thất thoát 3.8% tổng doanh thu mỗi đợt mở bán do cộng dồn ưu đãi cấm; đối chiếu bài học thành công từ case Morgan Stanley về việc trích dẫn nguồn kiểm chứng bắt buộc).*

---

### 4. Cách làm Mới (TO-BE Workflow & 3 Thay đổi Bắt buộc)
* **Nguồn kiểm chứng (Verifiable Citations):** Tích hợp bắt buộc tính năng Dual Explainability: tự động trích dẫn chính xác Số văn bản/Điều/Khoản áp dụng cho các ưu đãi hợp lệ (Why), đồng thời chỉ rõ lý do loại trừ đối với các ưu đãi bị xung đột hoặc không thỏa mãn (Why-not).
* **Người chịu trách nhiệm (Clear Ownership):** Phân chia rành mạch theo Mollick: Sales chịu trách nhiệm xác thực thông tin đầu vào của khách; Sales Manager giữ quyền quyết định cuối cùng trên cổng phê duyệt HITL (Cờ Xanh/Vàng/Đỏ); Chuyên viên Chính sách (Policy Admin) chịu trách nhiệm pháp lý cho dữ liệu văn bản nguồn.
* **Cách xử lý khi AI không chắc chắn (Safe Abstention):** Kích hoạt cơ chế Dừng an toàn (Safe Abstention): khi phát hiện văn bản chính sách mâu thuẫn hoặc thiếu dữ liệu xác minh, AI tuyệt đối không đoán mò con số mà tự động ngắt tính toán, gán Cờ Đỏ và chuyển thẳng sang luồng thẩm định ngoại lệ cho Quản lý xử lý.

---

### 5. Bộ Chỉ số Ra Quyết định (Decision Metrics)

| Tầng | Phân loại | Tên chỉ số | Mốc đầu (Baseline) | Mục tiêu (Target) | Nguồn dữ liệu | Người phụ trách (Owner) | Hành động khi chỉ số xấu |
| :---: | :---: | :--- | :---: | :---: | :--- | :--- | :--- |
| **1** | **Workflow** | **Tỷ lệ giao dịch báo giá hoàn tất đủ luồng kiểm chứng trên AI Agent (Validated Quote Rate)** | 18% giao dịch cọc | $\ge 85\%$ giao dịch cọc | Đối soát chéo: Log Báo giá AI vs Mã cọc ERP | Giám đốc Sàn giao dịch & Sales Ops Lead | Khóa quyền xuất phiếu thu cọc trên ERP nếu hồ sơ thiếu mã Snapshot ID từ AI Agent. |
| **3** | **Workflow** | **Thời gian hoàn tất một lượt lập và phê duyệt báo giá (Time-to-Quote & Approval)** | 25 phút/báo giá | $\le 60$ giây (15s lập + 45s duyệt) | Log tác vụ hệ thống thời gian thực | Trưởng phòng Kinh doanh (Sales Manager) | Kích hoạt cảnh báo SLA: nếu quản lý không duyệt trong 3 phút, tự động leo thang sang Phó Giám đốc trực sàn. |
| **4** | **Product** | **Tỷ lệ kích hoạt Dừng an toàn chuẩn xác khi chính sách xung đột hoặc mập mờ (Safe Abstention Recall)** | 40% (AI đoán mò/lỗi chung chung) | **100%** ca xung đột/mập mờ được dừng an toàn | Log xung đột chính sách & Log ngoại lệ thẩm định | Lead AI Solution Architect & Policy Admin | Khóa tạm thời module chính sách của dự án đó; triệu tập Ban Chính sách ban hành đính chính trong 24 giờ. |
| **5** | **Product** | **Tỷ lệ thất thoát biên lợi nhuận do áp sai chính sách bán hàng** | Thất thoát 3.8% doanh thu | **Thất thoát = 0%** (Loại trừ 100% sai sót) | Báo cáo kiểm toán doanh thu & Snapshot Log (SHA-256) | Giám đốc Tài chính (CFO) & Giám đốc Khối Bán hàng | Kích hoạt Emergency Kill-switch, đình chỉ ngay quyền phê duyệt ngoại lệ của quản lý vi phạm. |

---

### 6. Quyết định Hành động & Cải tiến so với Bản v1
* **Quyết định chính thức:** **SỬA (FIX & RESTRUCTURE WORKFLOW)**.
* **Lý do (1 câu):** Không mở rộng tràn lan và không hủy bỏ công cụ, mà tập trung thiết kế lại workflow đưa AI vào đúng vị trí trợ lý có bảo chứng trích nguồn và cưỡng chế cổng duyệt tập trung HITL nhằm giải quyết triệt để điểm nghẽn niềm tin của nhân viên kinh doanh.
* **Hai thay đổi cốt lõi so với bản v1 (sau phản biện chéo):**
  1. *Thay đổi chỉ số Tầng 1:* Chuyển từ *"Số lượt đăng nhập hệ thống/ngày"* (vanity metric) sang *"Tỷ lệ giao dịch báo giá hoàn tất đủ luồng kiểm chứng trên AI Agent"* (gắn chặt với giá trị quy trình nghiệp vụ thực tế).
  2. *Bổ sung chỉ số Tầng 4:* Bổ sung chỉ số *"Tỷ lệ kích hoạt Dừng an toàn chuẩn xác khi chính sách xung đột hoặc mập mờ (Safe Abstention Recall) đạt 100%"* nhằm đảm bảo an toàn tuyệt đối, ngăn chặn hoàn toàn rủi ro AI ảo giác sinh số liệu sai lệch.

---

### 7. Cấu trúc Hồ sơ Repo

```text
Day26_Track01_T096/
├── README.md                          ← Báo cáo tổng hợp chuẩn 6 mục theo yêu cầu Lab
├── dashboard/
│   └── dashboard_hanh_dong_v2.xlsx    ← Bảng Dashboard 5 tầng hoàn thiện sau phản biện chéo
├── memo/
│   └── memo_quyet_dinh.md             ← Memo quyết định chi tiết 5 phần kèm lộ trình Gate 30-60-90
└── v1/
    └── dashboard_hanh_dong_v1.xlsx    ← Bảng Dashboard ban đầu trước phản biện để đối chiếu thay đổi
```
