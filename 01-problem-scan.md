# Problem Scan & Quick Assessment — Vin Smart Future (Healthcare Edition)

> **File nộp bài cá nhân (Phase 1 & Phase 2 theo hướng dẫn README.md)**
> * **Người thực hiện:** **Đặng Quốc Cường**
> * **Vai trò:** AI Product Engineer tại Vin Smart Future
> * **Đơn vị trọng tâm:** Vinmec Healthcare System (kết hợp các công ty thành viên Vingroup)
> * **Nhánh Git cá nhân:** `cuong`

---

# 🔍 Phase 1 — SCAN: Bảng quét cơ hội (Sử dụng 4 Lenses)

Quét qua các hoạt động vận hành thực tế tại các công ty thành viên Vingroup nhằm tìm kiếm các điểm nghẽn (bottlenecks) có thể tối ưu bằng AI:

| # | Công ty thành viên | Lens | Mô tả ngắn bài toán / Điểm nghẽn vận hành |
|---|-------------------|------|------------------------------------------|
| **1** | **Vinmec** | **Tốn thời gian** | **AI-First Prescription Drafter:** Bác sĩ mất 12–15 phút/ca gõ thủ công từng mã thuốc và tính liều theo eGFR cho ca bệnh mạn tính. AI chủ động phân tích Big Data để soạn sẵn đơn thuốc tối ưu ngay khi có chẩn đoán. |
| **2** | **Vinmec** | **AI có thể tốt hơn** | **Tóm tắt hồ sơ xuất viện (Discharge Summary):** Bác sĩ mất 25–30 phút/bệnh nhân để đọc lại toàn bộ ghi chú lâm sàng, xét nghiệm và tự viết bản tóm tắt xuất viện bằng tay. |
| **3** | **Vinmec** | **Lặp lại** | **Mã hóa bệnh án ICD-10 tự động:** Chuyên viên bảo hiểm y tế đọc hồ sơ bệnh án để dò tìm và gán thủ công hàng trăm mã bệnh/thủ thuật ICD-10 phục vụ thanh quyết toán BHYT. |
| **4** | **VinFast** | **Lặp lại** | **Đối chiếu hóa đơn trạm sạc:** So khớp dữ liệu sạc điện hằng tuần từ hàng nghìn trụ sạc đối tác công cộng với hóa đơn thực tế gửi về hệ thống tài chính ERP. |
| **5** | **Xanh SM** | **Tốn thời gian** | **Điều phối viên xử lý sự cố hết pin thực địa:** Tài xế taxi điện báo cạn pin, điều phối viên mất 15 phút tra cứu GPS, tìm trạm sạc trống và soạn tin chỉ dẫn thủ công. |
| **6** | **Vinhomes** | **Pain từ người khác** | **Phân loại & Định tuyến phản ánh cư dân:** Khiếu nại (mất nước, hỏng đèn, tiếng ồn) gửi qua App Vinhomes Resident được nhân viên CSKH đọc và chuyển tiếp thủ công, mất 12–24h xử lý. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

Chọn lọc Top 3 bài toán tiềm năng nhất từ danh sách SCAN và hoàn thiện 3 thẻ bài toán:

---

### 📇 QUICK PROBLEM CARD #1 (LỰA CHỌN ƯU TIÊN SỐ 1 ĐỂ DEEP-DIVE)

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu): AI chủ động khai thác Lịch sử Dùng thuốc  │
│ Cá nhân kết hợp Big Data để khởi tạo sẵn đơn thuốc mẫu tối   │
│ ưu cho người khám, đồng thời ghi nhận phản hồi để tự học.    │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [x] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Bác sĩ ngoại trú/nội trú (mất 12-15    │
│ phút gõ phím), Bệnh nhân (chờ đợi mệt mỏi tại phòng khám).  │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Khám, nhập ICD-10 ──> 2. Nhớ/tra phác đồ đa bệnh lý    │
│   ──> 3. Gõ tìm 5-8 thuốc ──> 4. Rà soát eGFR & dị ứng      │
│   ──> 5. In đơn và ký tay (không có vòng lặp tự học)        │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 & 4 (⏱ 12 phút/ca)  │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2, 3 và 4        │
│ (Dual-RAG: Truy xuất lịch sử cá nhân + Big Data soạn đơn)   │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│   1. Giảm thời gian kê đơn từ 15 min ──> dưới 2 min/ca.     │
│   2. Tỷ lệ bác sĩ chấp thuận đơn gợi ý: >= 80% ban đầu.     │
│   3. Tỷ lệ chấp thuận tăng lên >= 90% sau 3 tháng tự học.   │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [ ] LLM  [x] Agent │
└─────────────────────────────────────────────────────────────┘
```

---

### 📇 QUICK PROBLEM CARD #2

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu): Tự động trích xuất thông tin lâm sàng và  │
│ cận lâm sàng từ EHR để soạn thảo bản tóm tắt xuất viện.     │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [x] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Bác sĩ điều trị nội trú (quá tải hồ sơ)│
│ Bệnh nhân (khó hiểu các thuật ngữ y khoa phức tạp).         │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Mở hồ sơ bệnh án EHR ──> 2. Đọc diễn tiến điều trị     │
│   ──> 3. Gõ tay bản tóm tắt ──> 4. In và nộp lưu trữ        │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ 25 phút/ca)  │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 và 3           │
│ (Đọc dữ liệu EHR -> Trích xuất -> Sinh bản tóm tắt nháp)    │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│   1. Giảm thời gian soạn hồ sơ từ 25 min ──> dưới 5 min.    │
│   2. 95% bệnh nhân hiểu rõ hướng dẫn dùng thuốc tại nhà.    │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

---

### 📇 QUICK PROBLEM CARD #3

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu): Hỗ trợ điều phối viên Xanh SM xử lý sự    │
│ cố xe taxi điện hết pin giữa đường và chỉ dẫn trạm sạc trống│
│ Công ty thành viên: [ ] VinFast  [x] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Tài xế Xanh SM (chờ đợi), Điều phối    │
│ viên tổng đài (quá tải vào giờ cao điểm).                   │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Nhận cuộc gọi báo pin ──> 2. Tra cứu định vị GPS xe    │
│   ──> 3. Tra cứu trạm sạc trống ──> 4. Soạn SMS chỉ đường   │
│   ──> 5. Điều xe sạc pin lưu động (nếu cạn kiệt pin)        │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 & 4 (⏱ 10 phút/ca)  │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3 và 4           │
│ (Tự động hóa pull dữ liệu trạm sạc -> Soạn draft tin nhắn)  │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│   1. Giảm thời gian xử lý sự cố từ 15 min ──> dưới 3 min.   │
│   2. Tỷ lệ điều xe đúng trạm sạc khả dụng đạt 98%.          │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

---

# 🗳️ Quyết định lựa chọn của tôi & Nhóm:

**Lựa chọn cuối cùng:** **Card #1 — Vinmec ClinicalRx: AI-First Self-Improving Prescription Drafter.**

### Lý do lựa chọn và loại bỏ các thẻ khác:
* **So với Card #2 (Vinmec Discharge Summary):** Card #2 chỉ giải quyết khâu hành chính sau xuất viện (hậu kỳ), không giải phóng được áp lực thời gian tại phòng khám. Trong khi đó, Card #1 trực tiếp tác động vào khâu khám chữa bệnh thực địa (*Point-of-Care*), giúp tăng thời gian bác sĩ tương tác với bệnh nhân và nâng cao doanh thu/năng suất phòng khám.
* **So với Card #3 (Xanh SM Sự cố sạc pin):** Card #1 có chiều sâu về công nghệ cao hơn vượt trội nhờ cơ chế **Agentic Loop with Human Feedback (Vòng lặp tự học hỏi)**. Bác sĩ không chỉ duyệt đơn mà còn đóng vai trò huấn luyện viên giúp Agent tự tiến hóa sau mỗi lần từ chối/sửa thuốc.
