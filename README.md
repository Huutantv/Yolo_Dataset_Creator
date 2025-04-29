# YOLO Dataset Creator - Factory Automation

## Giới Thiệu

YOLO Dataset Creator là công cụ đơn giản, hiệu quả để tạo và chuẩn bị dữ liệu huấn luyện cho mô hình YOLO (You Only Look Once). Ứng dụng này cung cấp giao diện đồ họa thân thiện, cho phép:

- Tạo annotations cho ảnh ở định dạng YOLO chuẩn
- Quản lý và tổ chức các nhãn/lớp
- Chia dữ liệu thành tập huấn luyện, kiểm tra và xác thực
- Tự động tạo tệp cấu hình YAML cho huấn luyện YOLO

## Cài Đặt

### Yêu Cầu Hệ Thống

- Python 3.6 trở lên
- Các thư viện cần thiết được liệt kê trong `requirements.txt`

### Các Bước Cài Đặt

1. Clone hoặc tải xuống mã nguồn
2. Cài đặt các thư viện cần thiết:

```
pip install -r requirements.txt
```

3. Chạy ứng dụng:

```
python yolo_dataset_creator.py
```

## Hướng Dẫn Sử Dụng

### 1. Thiết Lập Dự Án

1. Khởi động ứng dụng
2. Nhấp vào **"Chọn thư mục ảnh"** để chọn thư mục chứa ảnh cần gán nhãn
3. Nhấp vào **"Chọn thư mục lưu"** để chọn nơi lưu dataset đã gán nhãn

### 2. Quản Lý Lớp (Classes)

Mặc định, ứng dụng tạo sẵn 3 lớp: person, car, dog. Bạn có thể:
- Thêm lớp mới: Nhập tên lớp vào ô văn bản và nhấp **"Thêm"**
- Xóa lớp: Chọn lớp từ danh sách và nhấp **"Xóa lớp đã chọn"**
- Lưu danh sách lớp: Nhấp **"Lưu danh sách lớp"** để lưu vào tệp `classes.txt`

### 3. Gán Nhãn Ảnh

1. Sử dụng các nút **"< Trước"** và **"Tiếp >"** để duyệt qua các ảnh
2. Chọn lớp từ danh sách bên trái
3. Vẽ hình chữ nhật trên ảnh bằng cách nhấp và kéo chuột
4. Kiểm tra các annotations trong danh sách bên trái
5. Xóa annotation nếu cần bằng cách chọn và nhấp **"Xóa annotation đã chọn"**
6. Nhấp **"Lưu annotations cho ảnh hiện tại"** để lưu nhãn cho ảnh đang xem

### 4. Xuất Dataset

1. Điều chỉnh phần trăm chia dữ liệu cho tập huấn luyện, kiểm thử và xác thực
2. Nhấp **"Chia dữ liệu và xuất dataset"** để tự động:
   - Chia ảnh đã gán nhãn thành các tập theo tỷ lệ đã chọn
   - Tạo cấu trúc thư mục chuẩn cho YOLO
   - Tạo tệp cấu hình YAML

## Cấu Trúc Dataset Xuất Ra

Sau khi xuất, dataset của bạn sẽ có cấu trúc như sau:

```
output_folder/
├── train/
│   ├── images/
│   └── labels/
├── val/
│   ├── images/ 
│   └── labels/
├── test/
│   ├── images/
│   └── labels/
├── classes.txt
└── dataset.yaml
```

## Định Dạng YOLO

Mỗi ảnh sẽ có một tệp nhãn tương ứng (`.txt`) với định dạng:
```
<class_id> <x_center> <y_center> <width> <height>
```
Trong đó:
- `class_id`: ID của lớp (bắt đầu từ 0)
- Tất cả các tọa độ đã được chuẩn hóa về khoảng [0,1]

## Mẹo Và Thủ Thuật

- **Hiệu quả**: Gán nhãn cho các ảnh có nội dung tương tự cùng một lúc 
- **Nhất quán**: Đảm bảo sử dụng nhãn một cách nhất quán trên tất cả ảnh
- **Tỷ lệ chia**: Khuyến nghị sử dụng tỷ lệ 70-80% cho tập huấn luyện, 10-15% cho tập xác thực và 10-15% cho tập kiểm thử
- **Lưu thường xuyên**: Lưu annotations sau khi hoàn thành mỗi ảnh

## Xử Lý Sự Cố

1. **Không tìm thấy ảnh**: Đảm bảo thư mục chứa các file ảnh có định dạng phổ biến (jpg, jpeg, png, bmp)
2. **Lỗi khi lưu**: Kiểm tra quyền truy cập vào thư mục đầu ra
3. **Annotations không hiển thị**: Đảm bảo đã chọn cùng thư mục đầu ra khi mở lại dự án

## Sử Dụng Dataset Với YOLO

Dataset đã tạo có thể được sử dụng trực tiếp với YOLOv5, YOLOv8 và các phiên bản khác của YOLO. Tệp `dataset.yaml` đã được tạo sẵn để sử dụng trong quá trình huấn luyện. 
