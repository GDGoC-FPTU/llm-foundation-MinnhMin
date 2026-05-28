# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

*   **Kết quả phản hồi thực tế (Minh họa quy luật):**
    *   **Temperature = 0.0:** "Việt Nam là quốc gia xuất khẩu hạt điều lớn nhất thế giới, chiếm hơn 60% sản lượng toàn cầu. Ngoài ra, hang Sơn Đoòng tại Quảng Bình là hang động tự nhiên lớn nhất thế giới."
    *   **Temperature = 0.5:** "Một sự thật thú vị là Việt Nam là nước xuất khẩu cà phê lớn thứ hai thế giới, chỉ sau Brazil. Văn hóa cà phê sữa đá ở đây cũng rất nổi tiếng và được du khách quốc tế yêu thích."
    *   **Temperature = 1.0:** "Đất nước hình chữ S uốn lượn không chỉ có lịch sử hào hùng mà ẩm thực còn là sự giao thoa nghệ thuật tuyệt vời! Từ những gánh phở đêm đến nhịp sống năng động đầy sắc màu phố thị."
    *   **Temperature = 1.5:** "Việt Nam! Vùng đất ngọc ngà của những nụ cười rồng bay lấp lánh vũ trụ xanh mướt rặng tre. Có những huyền thoại cổ xưa kể về những hạt phù sa lấp lánh biết hát bài ca ngàn năm..."

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> *Khi giá trị temperature tăng dần từ 0.0 lên 1.5, phản hồi của mô hình chuyển đổi rõ rệt từ trạng thái nhất quán, chính xác và an toàn sang ngẫu nhiên, bay bổng và sáng tạo hơn. Ở mức thấp (0.0 và 0.5), văn phong gãy gọn và lặp lại các sự thật địa lý, kinh tế cốt lõi được ghi nhận đầy đủ. Tuy nhiên, khi đạt đến mức rất cao (1.5), mô hình bắt đầu mất logic cấu trúc câu, sử dụng từ ngữ kỳ lạ và xuất hiện hiện tượng "ảo tưởng thông tin" (hallucination) không còn đúng với thực tế.*

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> *Tôi sẽ đặt temperature ở mức **0.0** (hoặc tối đa là **0.2**). Vì hệ thống hỗ trợ khách hàng đòi hỏi tính chính xác tuyệt đối, thông tin đồng nhất và đáng tin cậy về các chính sách, giá cả hay thông số sản phẩm, cấu hình thấp giúp triệt tiêu hoàn toàn khả năng mô hình tự ý sáng tạo thông tin sai lệch gây rủi ro pháp lý cho doanh nghiệp.*

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> *Dựa vào bảng giá `PRICING_1M_TOKENS`, chi phí cho cả 1 triệu token đầu vào (Input) của GPT-4o đắt hơn GPT-4o-mini là 33.33 lần ($5.00 so với $0.150), và chi phí đầu ra (Output) cũng đắt hơn chính xác 33.33 lần ($20.00 so với $0.600). Do đó, tổng chi phí vận hành tổng thể cho toàn bộ hệ thống workload này của GPT-4o sẽ luôn đắt hơn **33.33 lần** so với GPT-4o-mini mà không phụ thuộc vào tỉ lệ chia tách số lượng token đầu vào hay đầu ra của người dùng.*

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> *   **Trường hợp GPT-4o xứng đáng:** Khi hệ thống cần giải quyết các tác vụ phức tạp đòi hỏi khả năng tư duy logic và suy luận bậc cao như phân tích chuyên sâu báo cáo tài chính doanh nghiệp, rà soát tìm lỗi bảo mật mã nguồn hệ thống phức tạp, hoặc dịch thuật các văn bản pháp lý đa ngôn ngữ đòi hỏi độ chính xác cao.
> *   **Trường hợp GPT-4o-mini tốt hơn:** Khi cần triển khai các tác vụ lặp đi lặp lại với số lượng dữ liệu cực lớn nhưng có độ phức tạp thấp (high-volume, low-complexity) như tự động phân loại cảm xúc bình luận của người dùng (Sentiment Analysis), tóm tắt nhanh nội dung email, hoặc trích xuất thông tin cơ bản từ các hóa đơn mua hàng.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> *Streaming đóng vai trò quan trọng nhất trong các ứng dụng trò chuyện trực tiếp tương tác trực tiếp với con người (như các hệ thống Chatbot trợ lý ảo), nơi văn bản dài cần thời gian tạo ra; việc chữ chạy đến đâu hiển thị ngay đến đó giúp giảm thời gian chờ đợi tâm lý (Perceived Latency) và mang lại cảm giác phản hồi tức thì. Ngược lại, chế độ Non-streaming lại phù hợp hơn đối với các tác vụ xử lý dữ liệu ngầm (Backend/Batch processing) không có giao diện người dùng trực tiếp, các bài toán cần phân tích dữ liệu hàng loạt, chấm điểm tự động, hoặc khi hệ thống lập trình cần lấy toàn bộ cấu trúc chuỗi đầu ra (ví dụ định dạng JSON hoàn chỉnh) để bóc tách xử lý logic cho các bước tiếp theo một cách an toàn.*


## Danh Sách Kiểm Tra Nộp Bài
- [x] Tất cả tests pass: `pytest tests/ -v`
- [x] `call_openai` đã triển khai và kiểm thử
- [x] `call_openai_mini` đã triển khai và kiểm thử
- [x] `compare_models` đã triển khai và kiểm thử
- [x] `streaming_chatbot` đã triển khai và kiểm thử
- [x] `retry_with_backoff` đã triển khai và kiểm thử
- [x] `batch_compare` đã triển khai và kiểm thử
- [x] `format_comparison_table` đã triển khai và kiểm thử
- [x] `exercises.md` đã điền đầy đủ
- [x] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 
