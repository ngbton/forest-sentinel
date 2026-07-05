# 🌲 FOREST SENTINEL

**HỆ THỐNG CẢNH BÁO CHÁY VÀ PHÁ RỪNG THÔNG MINH BẰNG AIOT**

**Cuộc thi Thiết kế Điện tử Việt Nam 2026**  
**Chủ đề:** AI nhúng cho hệ thống IoT thông minh

---

## 📋 Giới thiệu Dự Án

**Forest Sentinel** là hệ thống giám sát rừng thông minh sử dụng công nghệ **Edge AI** kết hợp mạng truyền thông **LoRa** tầm xa. Hệ thống có khả năng phát hiện sớm tiếng cháy rừng (crackling fire) và tiếng cưa máy (chainsaw) ngay tại biên, không phụ thuộc vào kết nối internet, phù hợp với điều kiện rừng sâu Việt Nam.

### Vấn đề thực tế
- Diện tích rừng Việt Nam và thế giới đang suy giảm nghiêm trọng do cháy rừng và khai thác trái phép.
- Các hệ thống hiện tại thường phụ thuộc Cloud/WiFi/4G → chi phí cao, khó triển khai ở vùng sâu.
- Forest Sentinel giải quyết bằng cách xử lý AI tại chỗ + truyền tin LoRa.

---

## ✨ Điểm Mới & Tính Sáng Tạo

- Kết hợp **3 yếu tố cốt lõi** trong một thiết bị: Edge AI + LoRa + Cảm biến âm thanh đơn lẻ.
- Xử lý nhận dạng âm thanh thời gian thực (< 500ms) ngay trên ESP32.
- Cơ chế **xác thực chéo giữa các Node** giúp giảm báo động giả và hỗ trợ định vị.
- Chi phí thấp, tiêu thụ năng lượng thấp, dễ mở rộng quy mô.

---

## 👥 Thành viên Đội FOREST SENTINEL

| STT | Họ và tên           | Vai trò chính                          | Trách nhiệm chính                                              |
|-----|---------------------|----------------------------------------|----------------------------------------------------------------|
| 1   | Nguyễn Bá Toàn      | Team Leader & Machine Learning         | Quản lý dự án, Xây dựng mô hình AI, Triển khai trên Edge       |
| 2   | Vũ Thành Danh       | Dataset & Machine Learning             | Thu thập & Tiền xử lý dữ liệu, Hỗ trợ Toàn training mô hình AI |
| 3   | Lê Văn Tấn Đạt      | LoRa                                   | Xây dựng Gateway, LoRa                                         |
| 4   | Vũ Hải Thiện        | Embedded System & Firmware             | Code ESP32, Hệ thống nhúng                                     |
| 5   | Nguyễn Trung Hậu    | System Integration & Testing           | Dashboard, Testing                                             |

---

## 🎯 Các Giai Đoạn Thực Hiện

### **Giai đoạn 1: Thu thập và Chuẩn hóa Dữ liệu** (Đang thực hiện)
**Mục tiêu:** Thu thập và chuẩn hóa **≥ 3500** mẫu âm thanh chất lượng cao.

**Các lớp âm thanh:**
- **Fire**: Tiếng cháy rừng, crackling fire, wildfire
- **Chainsaw**: Tiếng cưa máy, chặt cây trái phép
- **Background**: Âm thanh môi trường rừng (gió, mưa, chim, côn trùng...)

**Kết quả mong đợi:** Dataset cân bằng, gắn nhãn rõ ràng, đã augmentation.

### Giai đoạn 2: Thiết kế Hệ thống Cảnh báo LoRa
- Thiết kế Node IoT (ESP32 + Microphone + LoRa)
- Xây dựng Gateway LoRaWAN

### Giai đoạn 3: Xây dựng Mô hình Edge AI
- Feature extraction: **Log-Mel Spectrogram**
- Mô hình: **DS-CNN** tối ưu cho Edge
- Tối ưu: Quantization INT8, Pruning, Knowledge Distillation

### Giai đoạn 4: Đánh giá & Thử nghiệm Thực tế
- Thử nghiệm trong nhiều điều kiện thực tế
- Đánh giá: Accuracy, Precision, Recall, F1-score, Latency, Power consumption, False Positive Rate

---

## 📁 Cấu trúc Repository

# Kiến trúc Thư mục Dự án (Project Architecture)

```bash
forest-sentinel/
├── data/
│   ├── raw/                  # Dữ liệu âm thanh thô (.wav, .mp3 từ thực địa/dataset)
│   ├── processed/            # Dữ liệu sau tiền xử lý (đã cắt lọc nhiễu, chuyển thành Spectrogram)
│   ├── augmented/            # Dữ liệu sau khi tăng cường (thêm nhiễu trắng, thay đổi tốc độ)
│   └── metadata.csv          # File CSV lưu nhãn (label), đường dẫn file và thông tin dataset
├── models/                   # LƯU TRỮ VÀ QUẢN LÝ MÔ HÌNH AI
│   ├── checkpoints/          # Các điểm lưu trọng số tốt nhất trong quá trình training
│   └── exported/             # File mô hình đã xuất định dạng (.tflite, .onnx, .h5)
├── notebooks/                # Jupyter notebooks dùng để EDA, phân tích tín hiệu và thử nghiệm model
├── scripts/                  # CÁC SCRIPT PYTHON THỰC THI TÁC VỤ
│   ├── download/             # Script tự động tải và giải nén dataset từ nguồn mở
│   ├── preprocess/           # Script lọc nhiễu, chuẩn hóa tín hiệu, trích xuất đặc trưng (MFCC)
│   ├── augmentation/          # Script tăng cường dữ liệu âm thanh tự động
│   └── utils/                # Các hàm bổ trợ (đọc file, ghi log, định dạng cấu trúc dữ liệu)
├── src/                      # MÃ NGUỒN CHÍNH CỦA HỆ THỐNG
│   ├── edge/                 # Firmware chạy trên thiết bị đầu cuối (ESP32)
│   │   ├── include/          # File header định nghĩa chân pin, thông số kết nối Wi-Fi/LoRa
│   │   ├── lib/              # Driver điều khiển linh kiện (Microphone I2S, Module RF)
│   │   ├── model/            # File mô hình TinyML dạng mảng C++ (model_data.h)
│   │   └── src/              # Mã nguồn thực thi chính (main.cpp)
│   ├── gateway/              # Code xử lý cho Trạm trung chuyển dữ liệu (Gateway)
│   └── dashboard/            # Mã nguồn giao diện quản lý, giám sát trực quan (Web Dashboard)
├── hardware/                 # PHẦN CỨNG THIẾT BỊ
│   ├── schematics/           # Sơ đồ nguyên lý mạch điện (Altium, Proteus, KiCad)
│   └── enclosure/            # File thiết kế cơ khí 3D cho vỏ hộp bảo vệ (STL, STEP)
├── docs/                     # TÀI LIỆU DỰ ÁN
│   ├── proposal.pdf          # Đề xuất ý tưởng dự án ban đầu
│   ├── report/               # Nội dung báo cáo tiến độ, báo cáo đồ án
│   └── images/               # Hình ảnh sơ đồ khối, ảnh thực tế minh họa
├── tests/                    # Thư mục chứa các kịch bản kiểm thử tự động (Unit Test)
├── .env.example              # File cấu hình mẫu chứa các biến môi trường trống (MQTT, DB)
├── docker-compose.yml        # Kịch bản khởi chạy nhanh hạ tầng Gateway/Dashboard (MQTT Broker, DB)
├── requirements.txt          # Các thư viện Python cần thiết phục vụ cho dự án
├── .gitignore                # Khai báo các file và thư mục rác/nặng Git cần bỏ qua
└── README.md                 # Tài liệu hướng dẫn cài đặt và vận hành tổng quan dự án
