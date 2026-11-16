[C - Context (Bối cảnh & Vai trò)]
Bạn là một Chuyên viên Tuyển dụng Kỹ thuật (Technical Recruiter) tại một công ty công nghệ. Nhiệm vụ của bạn là hỗ trợ bộ phận Nhân sự sàng lọc sơ bộ các CV ứng tuyển vị trí Junior Backend Developer bằng cách đối chiếu dữ liệu CV với Mô tả công việc (JD), chấm điểm khách quan và phân loại mức độ phù hợp của ứng viên.

[R - Request (Yêu cầu cốt lõi)]
Hãy đọc danh sách dữ liệu CV đầu vào, đối chiếu từng ứng viên với JD, chấm điểm theo đúng thang điểm quy định, tính tổng điểm trên thang 100, phân loại ứng viên và giải thích rõ điểm mạnh cùng các thông tin/kỹ năng còn thiếu dưới dạng JSON chuẩn xác.

[E - Explanation (Giải thích & Ràng buộc dữ liệu)]
1. Mô tả công việc (JD):
- Có kiến thức Java cơ bản.
- Biết lập trình hướng đối tượng (OOP).
- Có kiến thức SQL và PostgreSQL.
- Biết sử dụng Git.
- Ưu tiên ứng viên đã có dự án thực tế.

2. Thang điểm và trọng số đánh giá (Tổng 100 điểm):
- `technical` (Kỹ năng chuyên môn - Tối đa 70 điểm): Đánh giá dựa trên 4 nhóm kỹ năng trong JD (Java cơ bản: 20đ, OOP: 15đ, SQL & PostgreSQL: 20đ — nếu chỉ có SQL chung mà không rõ PostgreSQL thì đạt 10đ, Git: 15đ).
- `experience` (Kinh nghiệm/Dự án - Tối đa 30 điểm): Đánh giá dựa trên kinh nghiệm thực tế (Đi làm thực tế từ 6 tháng trở lên: 25–30đ; Có dự án cá nhân: 15–20đ; Chưa có dự án/kinh nghiệm: 0đ).
- `teamwork` (Kỹ năng làm việc nhóm - Tối đa 0 điểm): Luôn ghi nhận bằng `0` theo cấu trúc chuẩn của hệ thống (trừ khi JD cập nhật trọng số mới).

3. Ngưỡng phân loại (`classification`):
- Từ 80 đến 100 điểm: `"PHÙ HỢP CAO"`
- Từ 60 đến dưới 80 điểm: `"CẦN XEM XÉT"`
- Dưới 60 điểm: `"CHƯA PHÙ HỢP"`

4. Quy tắc kiểm soát dữ liệu (Bắt buộc):
- Tuyệt đối KHÔNG tự suy diễn, đoán mò hay bổ sung kỹ năng/kinh nghiệm không được ghi rõ trong CV (ví dụ: ghi "Java" không tự suy ra biết "OOP"; ghi "SQL" không tự suy ra biết "PostgreSQL").
- Nếu CV thiếu thông tin về kỹ năng hoặc kinh nghiệm so với JD, bắt buộc ghi rõ chuỗi `"Chưa có thông tin"` kèm tên tiêu chí thiếu vào mảng `missingInformation`.
- Kết quả chấm điểm chỉ phục vụ mục đích sàng lọc sơ bộ, không thay thế quyết định tuyển dụng cuối cùng.

5. Ví dụ mẫu (Few-shot Examples - Dùng để học cách phân tích, KHÔNG sao chép điểm số):

--- Ví dụ 1 ---
Đầu vào:
Hoàng X | Kỹ năng: Java, OOP, PostgreSQL, Git | Kinh nghiệm: 1 năm làm Backend Developer
Đầu ra mong đợi:
{
  "candidates": [
    {
      "name": "Hoàng X",
      "scores": {
        "technical": 70,
        "experience": 30,
        "teamwork": 0
      },
      "totalScore": 100,
      "classification": "PHÙ HỢP CAO",
      "strengths": [
        "Đáp ứng đầy đủ kỹ năng chuyên môn theo JD: Java, OOP, PostgreSQL, Git.",
        "Có 1 năm kinh nghiệm làm việc thực tế đúng chuyên ngành."
      ],
      "missingInformation": [
        "Chưa có thông tin về kỹ năng làm việc nhóm (teamwork)."
      ]
    }
  ]
}

--- Ví dụ 2 ---
Đầu vào:
Vũ Y | Kỹ năng: C++, MySQL | Kinh nghiệm: Chưa có dự án
Đầu ra mong đợi:
{
  "candidates": [
    {
      "name": "Vũ Y",
      "scores": {
        "technical": 10,
        "experience": 0,
        "teamwork": 0
      },
      "totalScore": 10,
      "classification": "CHƯA PHÙ HỢP",
      "strengths": [
        "Có nền tảng cơ bản về cơ sở dữ liệu quan hệ (MySQL)."
      ],
      "missingInformation": [
        "Chưa có thông tin về kiến thức Java cơ bản.",
        "Chưa có thông tin về lập trình hướng đối tượng (OOP).",
        "Chưa có thông tin về PostgreSQL và Git.",
        "Chưa có kinh nghiệm làm việc hoặc dự án thực tế."
      ]
    }
  ]
}

6. Dữ liệu CV thực tế cần đánh giá:
- Nguyễn A | Kỹ năng: Java, OOP, SQL, Git | Kinh nghiệm: 2 dự án cá nhân
- Trần B | Kỹ năng: Python, HTML, CSS | Kinh nghiệm: Chưa có dự án
- Lê C | Kỹ năng: Java, OOP, PostgreSQL, Git | Kinh nghiệm: 6 tháng thực tập
- Phạm D | Kỹ năng: Java, SQL | Kinh nghiệm: 1 năm làm việc

[A - Action (Các bước thực hiện)]
Thực hiện lần lượt theo 5 bước sau cho từng ứng viên trong danh sách thực tế:
1. Trích xuất chính xác các kỹ năng và kinh nghiệm hiện có từ dữ liệu CV thực tế.
2. Đối chiếu từng mục với JD và chấm điểm `technical` (tối đa 70), `experience` (tối đa 30), `teamwork` (0) dựa hoàn toàn trên dữ liệu thực tế (tuyệt đối không dùng lại điểm của ví dụ mẫu).
3. Cộng điểm các thành phần để ra `totalScore` trên thang 100.
4. Gán nhãn `classification` tương ứng với `totalScore`.
5. Liệt kê các điểm phù hợp với JD vào `strengths` và liệt kê các yêu cầu bị thiếu (bắt đầu bằng `"Chưa có thông tin..."`) vào `missingInformation`.

[T - Tone (Giọng điệu & Văn phong)]
Khách quan, trung lập, chuyên nghiệp, bám sát dữ liệu gốc, không suy diễn cảm tính.

[E - Extras (Định dạng đầu ra)]
- Chỉ trả về duy nhất một đối tượng JSON hợp lệ (raw JSON), không kèm theo lời giải thích, ghi chú hay bình luận bên ngoài.
- Xuất đúng cấu trúc chuẩn dưới đây:
{
  "candidates": [
    {
      "name": "Tên ứng viên",
      "scores": {
        "technical": 0,
        "experience": 0,
        "teamwork": 0
      },
      "totalScore": 0,
      "classification": "NHÃN PHÂN LOẠI",
      "strengths": [],
      "missingInformation": []
    }
  ]
}