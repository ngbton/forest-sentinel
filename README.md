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

| STT | Họ và tên           | Vai trò chính                          | Trách nhiệm chính                  |
|-----|---------------------|----------------------------------------|------------------------------------|
| 1   | Nguyễn Bá Toàn      | Team Leader                            | Quản lý dự án, Phần cứng, LoRa     |
| 2   | [Tên TV 2]          | Dataset & Machine Learning             | Thu thập & Xử lý dữ liệu           |
| 3   | [Tên TV 3]          | Edge AI & Model Optimization           | Xây dựng mô hình, Triển khai Edge  |
| 4   | [Tên TV 4]          | Embedded System & Firmware             | Code ESP32, Hệ thống nhúng         |
| 5   | [Tên TV 5]          | System Integration & Testing           | Gateway, Dashboard, Testing        |

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

```bash
forest-sentinel-aiot/
├── data/
│   ├── raw/                 # Dữ liệu âm thanh thô
│   ├── processed/           # Dữ liệu sau tiền xử lý
│   ├── augmented/           # Dữ liệu sau augmentation
│   └── metadata.csv         # File nhãn và thông tin
├── notebooks/               # Jupyter notebooks phân tích dữ liệu
├── scripts/
│   ├── download/            # Script tải dataset
│   ├── preprocess/          # Lọc nhiễu, chuẩn hóa
│   ├── augmentation/        # Tăng cường dữ liệu
│   └── utils/               # Công cụ hỗ trợ
├── src/
│   ├── edge/                # Code chạy trên ESP32
│   ├── gateway/             # Code cho Gateway
│   └── dashboard/           # Web dashboard quản lý
├── hardware/
│   ├── schematics/          # Sơ đồ mạch
│   └── enclosure/           # Thiết kế vỏ
├── docs/
│   ├── proposal.pdf         # Đề xuất ý tưởng
│   ├── report/              # Báo cáo
│   └── images/              # Hình ảnh minh họa
├── requirements.txt
├── .gitignore
└── README.md
