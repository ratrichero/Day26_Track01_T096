# MEMO QUYẾT ĐỊNH ÁP DỤNG SẢN PHẨM AI
**Dự án:** PricePolicy AI Agent – Nền tảng Định giá & Bảo chứng Chính sách Bán hàng Bất động sản VLandFuture  
**Nhóm thực hiện:** Nhóm T096  
**Người phụ trách chính:** Tạ Việt Cường (MSSV: 2A202602560)  
**Ngày lập memo:** 14/10/2026  
**Trạng thái quyết định:** **SỬA (RESTRUCTURE WORKFLOW & TRUST ARCHITECTURE TRƯỚC KHI MỞ RỘNG)**

---

## 1. Vấn đề và Nguyên nhân gốc

### 1.1 Hiện trạng quan sát & Vấn đề thực tế (Problem Statement)
Hệ thống **PricePolicy AI Agent** đã được triển khai (Deployment) và cấp tài khoản cho 120 nhân viên kinh doanh (Sales Executive) cùng 15 Quản lý bán hàng (Sales Manager) tại sàn phân phối VLandFuture. Tuy nhiên, sau 4 tuần đi vào hoạt động, tỷ lệ sử dụng thực tế (Adoption) vô cùng thấp:
* **78% nhân viên kinh doanh** vẫn tự lập bảng tính Excel cá nhân trôi nổi bên ngoài, tự tính nhẩm chiết khấu và chụp ảnh màn hình gửi qua Zalo để xin Quản lý phê duyệt.
* **Thời gian trung bình** để hoàn tất một lượt lập và duyệt giá mất tới 25 phút/giao dịch; quản lý rơi vào tình trạng "duyệt niềm tin" qua ảnh Zalo do không thể kiểm tra lại hàng chục công thức phức tạp trong giờ mở bán cao điểm.
* Doanh nghiệp ghi nhận thất thoát **3.8% tổng doanh thu** mỗi đợt mở bán do tình trạng sales áp dụng chồng chéo các chính sách ưu đãi cấm kết hợp, dùng phụ lục đã hết hiệu lực, hoặc hứa hẹn chiết khấu vượt khung.

### 1.2 Phân biệt Triệu chứng và Nguyên nhân gốc
* **Triệu chứng quan sát được:** *"Nhân viên ít sử dụng AI Agent, số lượt đăng nhập thấp, vẫn dùng Excel thủ công."*
* **Nguyên nhân gốc 1 (Độ tin cậy & Kiến trúc sản phẩm):** Hệ thống AI ban đầu chỉ đưa ra con số báo giá tổng mà thiếu cơ chế **Trích xuất nguồn gốc điều khoản hai chiều (Dual Explainability - Why & Why-not)**. Sales lo sợ nếu AI hiểu sai văn bản chính sách nhiều tầng sẽ dẫn tới tính nhầm giá, gây tranh chấp pháp lý và bản thân bị khấu trừ tiền hoa hồng cá nhân.
* **Nguyên nhân gốc 2 (Quy trình & Phân định trách nhiệm):** Quy trình nghiệp vụ chưa tích hợp bắt buộc công cụ AI vào mắt xích phê duyệt chính thức. Quản lý bán hàng vẫn chấp nhận duyệt hồ sơ qua Zalo; chưa có quy định bắt buộc gắn mã định danh Snapshot bất biến (SHA-256) vào hồ sơ đặt cọc kế toán.

---

## 2. Framework đã dùng và Bằng chứng thực tế

Quá trình chẩn đoán được thực hiện chuẩn xác thông qua 3 framework chuyên sâu:

### 2.1 Gartner-Lite (Đánh giá mức độ sẵn sàng của tổ chức)
* **Direction (Hướng đi - ĐẠT):** Mục tiêu số hóa công tác định giá thương mại, triệt tiêu thất thoát 2%–6% biên lợi nhuận ròng và rút ngắn chu kỳ chốt cọc là hoàn toàn đúng đắn và có sự cam kết từ Ban Giám đốc.
* **Readiness (Mức sẵn sàng - THIẾU):** Dữ liệu văn bản chính sách bán hàng chưa có người chịu trách nhiệm cập nhật tập trung (Data/Policy Owner). Khi có phụ lục sửa đổi khẩn cấp, tài liệu đưa lên hệ thống bị trễ 2–3 ngày, gây ra tình trạng bất đồng bộ dữ liệu.
* **Absorption (Khả năng hấp thụ - THIẾU):** Chưa có quy trình bàn giao (handoff) rõ ràng giữa Sales và Quản lý trên hệ thống; thiếu vòng lặp phản hồi (feedback loop) để đội ngũ AI tiếp nhận và tinh chỉnh khi phát hiện lỗi suy luận điều khoản loại trừ.

### 2.2 Mollick – Jagged Frontier (Phân chia công việc Người – AI)
Hệ thống ban đầu mắc lỗi gộp chung vai trò hoặc để AI can thiệp vào vùng quyết định nhạy cảm. Cần phân định lại 3 vùng ranh giới:
1. **Người giữ quyền (Human Mandate):** Quản lý Bán hàng giữ thẩm quyền phê duyệt cuối cùng (Approve / Reject / Exception) đối với các giao dịch có rủi ro; Sales chịu trách nhiệm xác thực thông tin đầu vào của khách hàng.
2. **AI hỗ trợ, Người kiểm tra (Centaurs/Cyborgs):** AI thực hiện tra cứu chính sách theo ngày hiệu lực (Time-Travel), phát hiện mâu thuẫn điều khoản 3 cấp độ, tính toán số học tất định 100% (Deterministic Math Engine), sinh bảng so sánh 3 phương án và giải trình lý do Why/Why-not. Sales kiểm chứng nguồn trước khi tư vấn khách.
3. **AI tự động (Safe Automation):** Chỉ tự động đóng gói dữ liệu và băm mã SHA-256 tạo Snapshot bất biến đối với các báo giá không có rủi ro (Cờ Xanh). Khi gặp điều khoản mờ mịt, AI phải kích hoạt **Dừng an toàn (Safe Abstention)** thay vì đoán mò.

### 2.3 ADKAR (Chẩn đoán điểm nghẽn hành vi người dùng)
* **Awareness (Nhận thức):** Sales nhận thức được công ty có tool AI mới nhưng chưa hiểu rõ phạm vi trách nhiệm.
* **Desire (ĐIỂM NGHẼN CHÍNH):** Sales **ngại dùng và không dám tin** vào kết quả của AI vì không thấy trích dẫn căn cứ phụ lục cụ thể. Nỗi sợ bị trừ tiền hoa hồng áp đảo mong muốn thử nghiệm công nghệ. Việc tổ chức đào tạo tính năng không giải quyết được điểm nghẽn này nếu không giải quyết được độ tin cậy.
* **Knowledge & Ability (Kiến thức & Kỹ năng):** Sales chưa được hướng dẫn kỹ năng đối chiếu căn cứ Why/Why-not và quy trình gửi duyệt 1-click.
* **Reinforcement (Củng cố):** Chưa có chế tài ngăn chặn kênh duyệt Zalo phi chính thức; chưa đưa chỉ số báo giá qua AI vào tiêu chí đánh giá KPI sàn.

### 2.4 Căn cứ & Bằng chứng thực tế thu thập được
1. **Dữ liệu Log tác vụ hệ thống (Telemetry Log):** Trong tháng đầu, 85% tài khoản sales chỉ đăng nhập đúng 1 lần trong buổi training rồi bỏ xó.
2. **Phỏng vấn sâu 15 Sales Executive tuyến đầu:** 13/15 người khẳng định: *"Em không dám mang con số AI gợi ý ra chốt với khách mua nhà 5–10 tỷ vì nếu sai chính sách chiết khấu thì tháng đó em bị trừ sạch hoa hồng. Dùng file Excel tự chế dù chậm nhưng em tự kiểm soát được công thức."*
3. **Bài học thực chứng quốc tế:**
   * *Morgan Stanley Case:* Nền tảng AI tư vấn quản lý tài sản chỉ đạt mức áp dụng 98% khi và chỉ khi mọi khuyến nghị tài chính đều đi kèm trích dẫn văn bản quy chuẩn (Verifiable Citations) và có chuyên gia con người chịu trách nhiệm.

---

## 3. Ít nhất 2 Thay đổi Cụ thể sau Kiểm tra chéo (Peer Review)

Trong phiên phản biện chéo với **Nhóm 05 (Chuyên đề Trợ lý Tra cứu Vận hành CSKH)**, nhóm T096 đã tiếp thu và thực hiện 2 thay đổi mang tính cốt lõi từ bản v1 sang bản v2:

| Hạng mục | Bản ban đầu (v1) | Bản hoàn thiện (v2 - Sau phản biện) | Giá trị mang lại |
| :--- | :--- | :--- | :--- |
| **Thay đổi 1: Chuyển đổi Chỉ số Tầng 1 (Usage)** | Đo lường bằng *"Số lượt đăng nhập hệ thống hàng ngày (Daily Logins)"* với mục tiêu $\ge 100$ lượt/ngày. | Thay thế bằng **"Tỷ lệ giao dịch báo giá hoàn tất đủ luồng kiểm chứng trên AI Agent (Validated Quote Rate)"** với mục tiêu $\ge 85\%$ giao dịch cọc thực tế. | Loại bỏ vanity metric vô nghĩa (đăng nhập điểm danh nhưng không dùng); gắn chặt việc đo lường vào quy trình nghiệp vụ tạo ra giá trị thực. |
| **Thay đổi 2: Bổ sung Chỉ số Tầng 4 (Quality & Reliability)** | Chỉ đo *"Tỷ lệ làm lại báo giá (Rework Rate) do sai sót tính toán"* chung chung. | Bổ sung thêm chỉ số **"Tỷ lệ kích hoạt Dừng an toàn chuẩn xác khi chính sách xung đột hoặc mập mờ (Safe Abstention Recall)"** với mục tiêu 100%. | Đảm bảo nguyên tắc an toàn doanh nghiệp: AI không đoán mò con số tài chính khi gặp văn bản mập mờ; chủ động ngắt tính toán và chuyển hồ sơ Cờ Đỏ cho Quản lý thẩm định ngoại lệ. |
| **Thay đổi bổ sung: Cột Hành động khi chỉ số xấu** | Các hành động ở bản v1 mang tính chung chung: *"Gửi email nhắc nhở", "Tổ chức thêm lớp đào tạo"*. | Chuẩn hóa hành động gắn liền với quyền kiểm soát quy trình: **Khóa quyền xuất phiếu thu cọc trên ERP nếu thiếu mã Snapshot ID từ AI**; tự động leo thang (escalate) SLA khi quản lý chậm duyệt. | Thiết lập cơ chế thực thi mang tính cưỡng chế quy trình (Hard Gate), triệt tiêu thói quen vận hành tùy tiện qua Zalo. |

---

## 4. Quyết định Hành động

> ### **QUYẾT ĐỊNH CHÍNH THỨC: SỬA (FIX & RESTRUCTURE WORKFLOW)**
> **Không tiếp tục mở rộng quy mô (Rollout)** khi chưa kiện toàn kiến trúc tin cậy.  
> **Không dừng dự án (Kill)** vì giá trị tiềm năng bảo toàn biên lợi nhuận (2%–6%) và rút ngắn chu kỳ bán hàng là cực kỳ lớn.  
> **Hành động bắt buộc:** Tiến hành **Sửa đổi toàn diện quy trình làm việc (TO-BE Workflow), bổ sung cơ chế bảo chứng trích nguồn Why/Why-not, và khóa chặt cổng phê duyệt HITL** trong phạm vi 1 dự án thí điểm trước khi nhân rộng.

---

## 5. Lý do, Bước tiếp theo và Phân công Trách nhiệm (Owners)

### 5.1 Lý do đưa ra quyết định
* Vấn đề cốt lõi không nằm ở thuật toán AI (AI nhận diện ngữ cảnh và máy tính số học tất định đã được kiểm chuẩn chính xác), mà nằm ở **sự đứt gãy niềm tin của người dùng (Desire bottleneck)** và **sự thiếu vắng quy tắc kiểm soát bắt buộc trong quy trình vận hành**.
* Việc "Sửa" tập trung vào việc trao quyền kiểm chứng cho Sales và cung cấp công cụ thẩm định rủi ro siêu tốc cho Quản lý sẽ tháo gỡ điểm nghẽn một cách triệt để mà không tốn kém chi phí mua sắm công cụ mới.

### 5.2 Lộ trình Thực thi & Các Cổng Quyết định (Gate 30–60–90 Ngày)

```
[0 - 30 Ngày: CHUẨN HÓA DỮ LIỆU & BASELINE]
├── Khóa phạm vi thí điểm: Dự án Zenith Park (40 Sales, 2 Quản lý).
├── Bổ nhiệm Policy Data Owner; thiết lập lịch cập nhật phụ lục trong 4 giờ.
├── Đo lường Baseline chính xác từ log hệ thống và đối soát ERP.
└── GATE 1: Dữ liệu chính sách số hóa 100% + Baseline xác lập đầy đủ.
        │
        ▼
[31 - 60 Ngày: BẢO CHỨNG ĐỘ TIN CẬY & THÍ ĐIỂM HẸP]
├── Bật tính năng Dual Explainability (Bắt buộc trích dẫn Why & Why-not).
├── Triển khai cổng duyệt HITL (Cờ Xanh/Vàng/Đỏ); CHẶN hoàn toàn việc duyệt qua Zalo.
├── Thiết lập quy trình QA mẫu 10% báo giá ngẫu nhiên mỗi tuần.
└── GATE 2: Tỷ lệ trích nguồn đạt 100%, Rework Rate < 5%, Thời gian duyệt < 60s.
        │
        ▼
[61 - 90 Ngày: MỞ RỘNG TOÀN DIỆN & THỂ CHẾ HÓA]
├── Mở rộng cho toàn bộ 120 sales và 15 quản lý tại tất cả các dự án.
├── Tích hợp API khóa quyền xuất phiếu thu cọc trên ERP nếu thiếu mã Snapshot SHA-256.
├── Đánh giá hiệu quả bảo toàn biên lợi nhuận và tốc độ chốt cọc.
└── GATE 3: Validated Quote Rate ≥ 85%, Thất thoát biên lợi nhuận = 0%.
```

### 5.3 Phân công Trách nhiệm (Owners)

| Vai trò | Người chịu trách nhiệm | Trọng tâm công việc |
| :--- | :--- | :--- |
| **Project Lead & AI Strategist** | **Tạ Việt Cường (Nhóm T096)** | Giám sát toàn diện lộ trình 30–60–90 ngày; theo dõi Dashboard 5 tầng; điều phối kiểm tra chéo các mốc Gate. |
| **Policy Data Owner** | **Chuyên viên Quản trị Chính sách (Policy Admin)** | Chuẩn hóa dữ liệu chính sách bán hàng; chịu trách nhiệm pháp lý cho văn bản số hóa; giải quyết xung đột điều khoản trong 24h. |
| **Sales Operations Lead** | **Giám đốc Sàn giao dịch & Sales Managers** | Triệt tiêu kênh duyệt Zalo; cưỡng chế quy trình duyệt qua cổng HITL; kèm cặp sales kiểm chứng nguồn tại sàn. |
| **Technical & AI Architect** | **Lead Solution Architect** | Đảm bảo công cụ toán học Deterministic Engine chính xác 100%; hoàn thiện cơ chế Dừng an toàn (Safe Abstention); lưu vết Snapshot SHA-256. |
| **Business Sponsor** | **Giám đốc Tài chính (CFO) & Giám đốc Khối Bán hàng** | Giám sát chỉ số thất thoát biên lợi nhuận; ký ban hành quy chế bắt buộc sử dụng PricePolicy AI Agent trong toàn hệ thống. |
