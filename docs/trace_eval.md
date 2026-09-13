# 📊 BÁO CÁO THU HOẠCH NGHIỆM THU BÀI LAB 3 (BƯỚC 3 — SUBMISSION ARTIFACT)

> **Họ và Tên Học viên:** Phạm Quân 
> **Mã Sinh Viên / Mã Học viên:** 2A202602890  
> **Chủ đề Lựa chọn:** Trợ lý Học vụ & Tra cứu Lịch thi VinUni: Tra cứu điểm GPA, lịch thi và đặt lịch tư vấn học vụ với Cố vấn.  

---

## 1. BẢNG CHẤM ĐIỂM AGENTIC FIT SCORING MATRIX (ĐÁNH GIÁ CHỦ ĐỀ)

| Tiêu chí Đánh giá | Mức độ (1 - 5) | Giải trình chi tiết lý do chọn điểm |
| :--- | :---: | :--- |
| **1. Multi-step Reasoning** | **5/5** | Bài toán yêu cầu Agent thực hiện nhiều bước liên tiếp: xác định mục tiêu người dùng, truy vấn dữ liệu học vụ, suy luận dữ liệu điểm GPA/lịch thi, chọn hành động tiếp theo như đặt lịch tư vấn hoặc trả lời khuyến nghị. Đây là dạng bài toán đa bước chứ không chỉ sinh văn bản đơn thuần. |
| **2. Tool Interaction** | **5/5** | Hệ thống cần kết nối với các công cụ bên ngoài qua MCP như `academic_query` để tra cứu thông tin sinh viên, `schedule_appointment` để đặt lịch với cố vấn, và có thể kiểm tra lịch thi/điểm số. Việc dựa trên dữ liệu thực tế từ tool là bắt buộc để tránh ảo giác. |
| **3. Dynamic Decision** | **4/5** | Agent phải điều hướng theo kết quả quan sát từng bước: nếu sinh viên chưa có dữ liệu điểm GPA thì hỏi bổ sung, nếu lịch thi không tồn tại thì gợi ý cách tra cứu khác, nếu cần đặt hẹn thì chuyển sang tool đặt lịch. Quyết định bước sau phụ thuộc vào phản hồi công cụ và ngữ cảnh người dùng. |
| **4. Long Horizon Goal** | **4/5** | Bài toán yêu cầu giữ mục tiêu xuyên suốt qua nhiều lượt xử lý: từ tra cứu thông tin đến lên kế hoạch tư vấn và trả lời cuối cùng. Mặc dù không quá dài như hệ thống xử lý nhiều nhiệm vụ phức tạp, nhưng vẫn cần duy trì ngữ cảnh và mục tiêu chính qua nhiều bước tương tác. |
| **TỔNG ĐIỂM AGENTIC FIT** | **18/20** | *Nếu tổng điểm > 12/20: Bài toán rất phù hợp triển khai Agentic System.* |

---

## 2. TRÍCH XUẤT KẾT QUẢ WATERFALL TRACE LOG (SAU KHI CHẠY TEST SUITE TRÊN API THẬT)

> ⚠️ **YÊU CẦU NGHIỆM THU:** Mở tệp `.env` điền `GEMINI_API_KEY` (hoặc `OPENAI_API_KEY`) để kết nối LLM thật trước khi thực thi `python src/app.py --all`. Bài nộp chỉ dùng Mock Offline Provider sẽ không đạt điểm nghiệm thực tế.

Dán 1 đoạn trích xuất log tiêu biểu từ file `docs/trace_waterfall.json` sinh ra từ phản hồi LLM API thật:

```json
[
  {
    "step": 1,
    "query": "Chào bạn, bạn có thể giới thiệu quy chế học vụ cơ bản của Đại học VinUni không?",
    "action_type": "FINAL_ANSWER",
    "thought": "Gemini phản hồi trực tiếp bằng văn bản (không cần gọi công cụ).",
    "output": "Chào bạn! Tôi là Trợ lý Tác tử Học vụ Thông minh của Đại học VinUni. Dưới đây là tóm tắt các quy chế và quy định học vụ cơ bản tại Đại học VinUni:\n\n---\n\n### 1. Hệ thống Tín chỉ và Chương trình Đào tạo\n* **Đơn vị tích lũy:** Các chương trình cử nhân tại VinUni được thiết kế theo hệ thống tín chỉ chuẩn quốc tế.\n* **Tải học tập (Course Load):** Sinh viên chính quy thường đăng ký từ **12 đến 18 tín chỉ** trong một học kỳ chính (Thu hoặc Xuân).\n\n---\n\n### 2. Thang điểm và Đánh giá Học tập\n* **Thang điểm 4.0 (GPA):** VinUni áp dụng thang điểm 4 (A = 4.0, B = 3.0, C = 2.0, D = 1.0, F = 0.0).\n* **Đánh giá quá trình (Continuous Assessment):** Kết quả môn học bao gồm bài tập, làm việc nhóm, thuyết trình, kiểm tra giữa kỳ và thi kết thúc môn học.\n* **Yêu cầu duy trì (Academic Standing):**\n  * **Tốt (Good Standing):** GPA tích lũy $\\ge 2.0$.\n  * **Cảnh báo học tập (Academic Probation):** Nếu GPA tích lũy hoặc GPA học kỳ giảm xuống dưới $2.0$.\n\n---\n\n### 3. Quy định Điểm danh và Tham gia Lớp học\n* **Chuyên cần:** Sinh viên được yêu cầu tham gia tối thiểu **80%** số buổi học trên lớp của mỗi môn học (hoặc theo yêu cầu cụ thể của từng giảng viên trong Syllabus).\n* **Nghỉ học có lý do:** Cần nộp minh chứng (giấy khám sức khỏe, lý do cá nhân chính đáng) lên Phòng Giáo vụ / Cố vấn học tập để được xem xét duyệt nghỉ phép.\n\n---\n\n### 4. Liêm chính Học thuật (Academic Integrity)\n* VinUni áp dụng chính sách nghiêm ngặt về liêm chính học thuật: **Không gian lận, không đạo văn (Plagiarism), không hỗ trợ hành vi gian lận**.\n* Mọi vi phạm có thể dẫn đến điểm 0 cho bài thi/môn học, cảnh cáo cấp trường hoặc buộc xuất học tùy mức độ.\n\n---\n\n### 5. Đăng ký Môn học & Đặt lịch Tư vấn\n* **Thêm/Hủy môn học (Add/Drop Period):** Thường diễn ra trong 1–2 tuần đầu tiên của học kỳ.\n* **Cố vấn Học tập (Academic Advisor):** Mỗi sinh viên đều có cố vấn học tập đồng hành để định hướng kế hoạch học tập, chọn chuyên ngành và hỗ trợ khi gặp khó khăn.\n\n---\n\n📌 **Lưu ý:** Nếu bạn cần tra cứu thông tin học vụ cá nhân (điểm số, danh sách môn học) hoặc đặt lịch hẹn tư vấn với Cố vấn Học tập, vui lòng cung cấp **Mã sinh viên** (ví dụ: `SV2026001`) để tôi hỗ trợ bạn nhé!",
    "latency_ms": 7685.4
  },
  {
    "step": 1,
    "query": "Hãy tra cứu thông tin học vụ của sinh viên SV2026001.",
    "action_type": "TOOL_EXECUTION",
    "tool_name": "academic_query",
    "arguments": {
      "student_id": "SV2026001"
    },
    "observation": {
      "status": "SUCCESS",
      "student_id": "SV2026001",
      "data": {
        "full_name": "Nguyễn Văn An",
        "class": "AI-K4",
        "gpa": 3.85,
        "email": "an.nv@vinuni.edu.vn",
        "status": "Đang học",
        "advisor": "PGS.TS Nguyễn Văn A"
      }
    },
    "latency_ms": 2047.07
  },
  {
    "step": 2,
    "query": "Hãy tra cứu thông tin học vụ của sinh viên SV2026001.",
    "action_type": "FINAL_ANSWER",
    "thought": "Tổng hợp kết quả từ MCP Server thành công.",
    "output": "Kết quả tra cứu cho sinh viên SV2026001 (Nguyễn Văn An): Lớp AI-K4, GPA: 3.85, Email: an.nv@vinuni.edu.vn, Trạng thái: Đang học, Cố vấn: PGS.TS Nguyễn Văn A.",
    "latency_ms": 10.0
  },
  {
    "step": 1,
    "query": "Sinh viên SV2026001 muốn đặt lịch tư vấn học vụ với cố vấn Nguyễn Thị Hạnh vào ngày 20/09/2026 lúc 15:30. Bạn có thể giúp đặt lịch cho em không?",
    "action_type": "TOOL_EXECUTION",
    "tool_name": "schedule_appointment",
    "arguments": {
      "student_id": "SV2026001",
      "advisor_name": "Nguyễn Thị Hạnh",
      "datetime_str": "15:30 20/09/2026"
    },
    "observation": {
      "status": "SUCCESS",
      "booking_id": "BK-SV2026001-99",
      "student_id": "SV2026001",
      "datetime": "15:30 20/09/2026",
      "advisor": "Nguyễn Thị Hạnh",
      "message": "Đặt lịch thành công cho sinh viên SV2026001 với Nguyễn Thị Hạnh vào lúc 15:30 20/09/2026."
    },
    "latency_ms": 2577.84
  }
]
```

---

## 3. TỔNG KẾT KẾT QUẢ NGHIỆM THU & NỘP BÀI

- [ ] Đã điền API Key thật trong `.env` và xác nhận Agent chạy mượt mà trên LLM API thật (Gemini/OpenAI).
- **Tổng số Test Cases đã chạy thành công:** 5 / 5 test cases.
- **Số lượt gọi Tool qua MCP Server chính xác:** 13 lượt.
- **Kết quả đẩy Repo nộp bài:** [ ] Đã Commit và Push mã nguồn thành công lên GitHub cá nhân.

---

> ✅ **HOÀN TẤT NỘP BÀI:** Sao chép đường link GitHub Repository cá nhân của bạn và dán vào ô nộp bài trên hệ thống LMS VLearn để hoàn tất Bài Lab 3!
