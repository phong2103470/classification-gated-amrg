# Kịch bản thực nghiệm & Mốc đối sánh (`results/`)

- **Mốc đối sánh nền tảng:** ResNet-50 đạt mAP `0,206` (IU-Xray) và `0,209` (MIMIC-CXR); ngưỡng tiềm năng lý thuyết BLEU-4 đạt `0,292`.
- **Kịch bản bóc tách (Ablation Study):**
  - `M0`: ResNet-50 + BCE + giải mã tự do (Baseline).
  - `M1`: Thay bộ mã hóa bằng Swin-Transformer V2 đa góc nhìn.
  - `M2`: Bổ sung GCN 55 nhãn RadGraph-XL + Focal Loss.
  - `M3`: Tích hợp Cổng tin cậy $\tau_k$ + Prompt cấu trúc + LLaMA-3 (8B).
