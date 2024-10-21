# Kéo và Thả RAG

## Tổng quan

![Ảnh chụp màn hình ứng dụng](https://storage.googleapis.com/mle-courses-prod/users/61b6fa1ba83a7e37c8309756/private-files/cf0ae020-8b6c-11ef-b095-cf36210a4279-Screen_Shot_2024_10_16_at_10.14.27.png)

[Xem video demo](https://www.youtube.com/watch?v=VjVHAfFvnQM&feature=youtu.be)

Dự án này triển khai quy trình **RAG (Tạo nội dung có bổ sung thông tin từ tìm kiếm)**. Người dùng có thể tải lên các tệp dữ liệu (CSV, JSON, PDF, DOCX), lưu nội dung vào **kho vector Chroma**, và tương tác với dữ liệu thông qua chatbot sử dụng **Gemini** hoặc các mô hình nguồn mở cục bộ như các mô hình từ **OLLAMA**. Chatbot sẽ truy xuất thông tin liên quan từ các tệp đã tải lên và sử dụng **LLMs** (Mô hình ngôn ngữ lớn) để cải thiện câu hỏi của người dùng, trả về các phản hồi có ý nghĩa.

## Các tính năng
1. **Tải lên các tệp CSV, JSON, PDF, hoặc DOCX** – Người dùng có thể tải tệp lên ở nhiều định dạng và chọn các cột hoặc phần để lập chỉ mục cho việc tìm kiếm dựa trên vector.
2. **Lưu trữ và truy xuất vector embeddings** sử dụng **Chroma** – Tự động lưu trữ embeddings từ các tệp tải lên và truy xuất nội dung liên quan cho các truy vấn.
3. **Chatbot tương tác** – Sử dụng **API Gemini** hoặc các mô hình cục bộ để tạo phản hồi nâng cao theo ngữ cảnh.
4. **Tùy chọn LLM tùy chỉnh** – Chọn giữa **Gemini trên đám mây** hoặc các LLM cục bộ, bao gồm **OLLAMA** và nhiều mô hình nguồn mở.
5. **Tùy chọn chunking linh hoạt** – Người dùng có thể áp dụng các chiến lược chunking như **Recursive Token Chunking**, **Agentic Chunking**, hoặc bỏ qua chunking.

## Chạy ứng dụng

### 1. Sao chép kho mã nguồn
```bash
https://github.com/PineappleCuteCute/Drop-RAG.git
cd drop-rag
```

### 2. Cài đặt các gói cần thiết
```bash
pip install -r requirements.txt
```

### 3. Chạy ứng dụng Streamlit
```bash
streamlit run app.py
```

Ứng dụng sẽ có thể truy cập tại `http://localhost:8501`.

## Hướng dẫn sử dụng

### 1. **Tải dữ liệu**
Tải tệp CSV, JSON, PDF, hoặc DOCX lên. Bạn có thể chọn cột nào để lập chỉ mục cho các tìm kiếm dựa trên vector.

### 2. **Embeddings và lưu trữ**
Dữ liệu được lưu trong **kho vector Chroma**, nơi embeddings vector được tạo bằng các mô hình như `all-MiniLM-L6-v2` (dành cho tiếng Anh) hoặc `keepitreal/vietnamese-sbert` (dành cho tiếng Việt).

### 3. **Chọn LLM**
Bạn có thể chọn sử dụng:
- **Gemini API**: Yêu cầu **khóa API Gemini** để tạo phản hồi. Nhận khóa [tại đây](https://aistudio.google.com/app/apikey).
- **LLM cục bộ qua OLLAMA**: Sử dụng **OLLAMA** để chạy các mô hình như `llama`, `gpt-j` và các mô hình nguồn mở khác trên máy tính cục bộ của bạn.

### Các tùy chọn mô hình OLLAMA

Dưới đây là danh sách các mô hình có sẵn cho **OLLAMA**, cùng với các định danh tương ứng:

| Tên mô hình                           | Kích thước mô hình | Định danh OLLAMA        |
|---------------------------------------|-------------------|-------------------------|
| Llama 3.2 (3B - 2.0GB)                | 3B (2.0GB)        | `llama3.2`              |
| Llama 3.2 (1B - 1.3GB)                | 1B (1.3GB)        | `llama3.2:1b`           |
| Llama 3.1 (8B - 4.7GB)                | 8B (4.7GB)        | `llama3.1`              |
| Llama 3.1 (70B - 40GB)                | 70B (40GB)        | `llama3.1:70b`          |
| Llama 3.1 (405B - 231GB)              | 405B (231GB)      | `llama3.1:405b`         |
| Phi 3 Mini (3.8B - 2.3GB)             | 3.8B (2.3GB)      | `phi3`                  |
| Phi 3 Medium (14B - 7.9GB)            | 14B (7.9GB)       | `phi3:medium`           |
| Gemma 2 (2B - 1.6GB)                  | 2B (1.6GB)        | `gemma2:2b`             |
| Gemma 2 (9B - 5.5GB)                  | 9B (5.5GB)        | `gemma2`                |
| Gemma 2 (27B - 16GB)                  | 27B (16GB)        | `gemma2:27b`            |
| Mistral (7B - 4.1GB)                  | 7B (4.1GB)        | `mistral`               |
| Moondream 2 (1.4B - 829MB)            | 1.4B (829MB)      | `moondream`             |
| Neural Chat (7B - 4.1GB)              | 7B (4.1GB)        | `neural-chat`           |
| Starling (7B - 4.1GB)                 | 7B (4.1GB)        | `starling-lm`           |
| Code Llama (7B - 3.8GB)               | 7B (3.8GB)        | `codellama`             |
| Llama 2 Uncensored (7B - 3.8GB)       | 7B (3.8GB)        | `llama2-uncensored`     |
| LLaVA (7B - 4.5GB)                    | 7B (4.5GB)        | `llava`                 |
| Solar (10.7B - 6.1GB)                 | 10.7B (6.1GB)     | `solar`                 |

### 4. **Tương tác với chatbot**
Sau khi tải dữ liệu và chọn LLM, bạn có thể bắt đầu tương tác với chatbot, chatbot sẽ truy xuất và bổ sung phản hồi dựa trên dữ liệu đã lưu.

### 5. **Tùy chọn chunking**
Trước khi truy vấn chatbot, người dùng có thể chọn từ các phương pháp chunking khác nhau:
- **Không chia nhỏ**: Sử dụng toàn bộ tài liệu mà không chia thành phần nhỏ.
- **Chia nhỏ theo số token**: Chia tài liệu thành các phần nhỏ dựa trên số lượng token.
- **Chia nhỏ theo nghĩa**: Nhóm văn bản theo ý nghĩa, giúp cải thiện độ chính xác của việc truy xuất.
- **Chia nhỏ động**: Quản lý các đoạn văn bản một cách động bằng cách sử dụng agent dựa trên LLM.

## Ghi chú
- Cần có **khóa API Gemini** nếu bạn chọn mô hình **Gemini**.
- Để suy luận mô hình cục bộ bằng **OLLAMA**, đảm bảo rằng **Docker** đã được cài đặt để chạy các mô hình cục bộ.

## Khắc phục sự cố

- Nếu truy vấn không trả về kết quả, hãy kiểm tra xem bạn đã chọn đúng cột để lập chỉ mục và embeddings đã được lưu trữ đúng cách.
- Đảm bảo khóa API hợp lệ (nếu sử dụng Gemini) và kho vector đã được khởi tạo trước khi sử dụng chatbot.
