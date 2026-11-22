# Classification-Gated Structured Medical Report Generation (`classification-gated-amrg`)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

## 1. Giới thiệu đề tài
Repository lưu trữ tài liệu tổng quan, thiết kế kiến trúc và kịch bản đánh giá thực nghiệm cho đề tài: **"Nghiên cứu phương pháp tự động sinh báo cáo y khoa có cấu trúc dựa trên cơ chế cổng phân loại bệnh lý đa nhãn"** (*Classification-Gated Structured Report Generation*).

## 2. Mục tiêu nghiên cứu
- Khắc phục hiện tượng **ảo giác lâm sàng** (*clinical hallucinations*) do giải mã văn bản tự do không ràng buộc.
- Cải thiện độ chính xác nhận diện các **bệnh lý hiếm dưới phân phối dữ liệu đuôi dài** (*long-tailed distribution*, ví dụ *consolidation* chỉ chiếm 3,9% dữ liệu).
- Chuẩn hóa báo cáo X-quang ngực theo 4 phân vùng giải phẫu (Phổi, Màng phổi, Trung thất, Thiết bị hỗ trợ).

## 3. Phương pháp đề xuất (Kiến trúc 3 giai đoạn)
1. **Giai đoạn 1 – Mã hóa thị giác đa góc nhìn:** Sử dụng **Swin-Transformer V2** trích xuất đặc trưng đồng thời từ ảnh X-quang thẳng và nghiêng.
2. **Giai đoạn 2 – Phân loại đồ thị đuôi dài 55 nhãn:** Xây dựng mạng tích chập đồ thị (**GCN**) trên 55 nhãn giải phẫu **RadGraph-XL / SRRG**, tối ưu bằng hàm mất mát **Focal Loss**.
3. **Giai đoạn 3 – Cổng tin cậy & Sinh báo cáo cấu trúc:** Lọc nhiễu qua ngưỡng tin cậy $\tau_k$, tạo câu lệnh cấu trúc $P_i(\mathcal{S}_i)$ dẫn hướng mô hình **LLaMA-3 (8B)** qua Adapter/Q-Former.

## 4. Kịch bản thực nghiệm & Kết quả đối sánh
- **Bộ dữ liệu chuẩn:** IU-Xray (7.470 ảnh) và MIMIC-CXR (377.110 ảnh).
- **Kịch bản bóc tách (Ablation Study):** `M0` (ResNet-50 + BCE Baseline) $\rightarrow$ `M1` (+Swin-Transformer V2) $\rightarrow$ `M2` (+GCN 55 nhãn & Focal Loss) $\rightarrow$ `M3` (+Cổng tin cậy $\tau_k$ & LLaMA-3).
- **Mốc đối sánh nền tảng:** Thu hẹp khoảng trống giữa mAP thực tế của ResNet-50 (`0,206` trên IU-Xray; `0,209` trên MIMIC-CXR) và ngưỡng tiềm năng lý thuyết (`0,292` BLEU-4).

## 5. Bản quyền và Giấy phép (License)
Dự án này được phát hành dưới giấy phép **MIT License** — cho phép tự do sử dụng, sao chép, chỉnh sửa và phân phối lại cho mục đích nghiên cứu lẫn thương mại với điều kiện giữ nguyên thông báo bản quyền. Xem chi tiết tại tệp [LICENSE](LICENSE).

## 6. Trích dẫn (Citation)
Nếu sử dụng tài liệu hoặc khung thiết kế từ repository này, vui lòng trích dẫn theo tệp [CITATION.cff](CITATION.cff).
