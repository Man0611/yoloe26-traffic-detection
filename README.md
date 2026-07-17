# YOLOE-26: Phát hiện xe máy và người đi bộ trên đường phố Việt Nam

## Giới thiệu

Project triển khai và đánh giá mô hình **YOLOE-26** (Sapkota & Karkee, 2026) cho bài toán
phân đoạn thực thể từ vựng mở (open-vocabulary instance segmentation) trên ảnh giao thông
Việt Nam, với đầy đủ 3 chế độ suy luận:

1. **Text prompt** (RepRTA) — chỉ định đối tượng bằng ngôn ngữ tự nhiên ("person", "motorcycle")
2. **Visual prompt** (SAVPE) — tìm các đối tượng tương tự chỉ từ 1 ví dụ mẫu
3. **Prompt-free** (LRPC) — tự động phát hiện với từ vựng tích hợp 4.585 lớp

## Cấu trúc repository

| Đường dẫn | Nội dung |
|---|---|
| `yoloe26-traffic-experiments-ipynb.ipynb` | Notebook toàn bộ thí nghiệm (chạy trên Kaggle, GPU T4) |
| `results/ket_qua_yoloe26/segment/predict/` | Thí nghiệm 1 — Text prompt |
| `results/ket_qua_yoloe26/segment/predict-2/` | Thí nghiệm 2 — Visual prompt |
| `results/ket_qua_yoloe26/segment/predict-3/` | Thí nghiệm 3 — Prompt-free |

## Dữ liệu

Bộ **Vietnamese Vehicles Dataset** (Kaggle, giấy phép CC0) — ảnh giao thông TP. Hồ Chí Minh
trong điều kiện ban ngày và ban đêm:
https://www.kaggle.com/datasets/duongtran1909/vietnamese-vehicles-dataset

## Cách chạy lại

1. Mở notebook trên Kaggle: https://www.kaggle.com/code/ngocman1/yoloe26-traffic-experiments-ipynb
2. Bấm **Copy & Edit**, thêm dataset qua **Add Input**, bật **GPU T4** trong Session options
3. Chạy lần lượt các cell

## Một số kết quả chính

- Text prompt phát hiện được xe máy/người đi bộ theo mô tả ngôn ngữ tự nhiên;
  tăng `imgsz=1280` và hạ `conf=0.1` cải thiện đáng kể khả năng bắt vật thể nhỏ ở xa
- Prompt-free tự nhận diện cả các lớp không được yêu cầu (bus, truck, eucalyptus tree);
  nâng ngưỡng `conf=0.4` loại bỏ phần lớn nhãn nhiễu ngữ cảnh (airport, terminal)
- Phân tích lỗi: mô hình khớp theo độ tương đồng embedding nên biểu tượng xe máy
  trên biển báo cấm cũng bị nhận là "motorcycle" — minh họa hạn chế của không gian
  nhúng thống nhất với các khái niệm giống nhau về mặt thị giác

## Tài liệu tham khảo

- R. Sapkota, M. Karkee, "YOLOE-26: Integrating YOLO26 with YOLOE for Real-Time
  Open-Vocabulary Instance Segmentation," arXiv:2602.00168, 2026
- Ultralytics YOLOE documentation: https://docs.ultralytics.com/models/yoloe
