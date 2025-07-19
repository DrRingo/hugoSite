---
title: "Giới thiệu bb-form: Công cụ tạo form terminal đẹp mắt với Clojure"
author: ["Nguyễn Bình Thành"]
publishDate: 2025-07-19T01:32:00+07:00
tags: ["clojure"]
categories: ["shell"]
draft: false
featured_image: "/assets/img/fish/trigla-pini.jpg"
---

## Mục đích sử dụng

**bb-form** là một công cụ mạnh mẽ được viết bằng Clojure và Babashka, giúp tạo ra những form thu thập dữ liệu đẹp mắt ngay trong terminal. Dự án này được thiết kế để giải quyết nhu cầu tạo giao diện người dùng thân thiện cho các ứng dụng command-line, đặc biệt hữu ích cho:

- **Thu thập dữ liệu từ người dùng**: Tạo form đăng ký, khảo sát, cấu hình
- **Tạo wizard cài đặt**: Hướng dẫn người dùng qua các bước cài đặt
- **Thu thập thông tin cấu hình**: Tạo file config với giao diện thân thiện
- **Tạo form phân nhánh**: Hỗ trợ logic phức tạp với các câu hỏi có điều kiện

### Điểm nổi bật của bb-form

✨ **Giao diện đẹp mắt**: Sử dụng Charm-gum để tạo giao diện terminal hiện đại  
🎯 **Validation thông minh**: Kiểm tra dữ liệu real-time với thông báo lỗi rõ ràng  
🌳 **Hỗ trợ phân nhánh**: Tạo form phức tạp với logic có điều kiện  
⚡ **Hiệu suất cao**: Chạy nhanh với Clojure Babashka  
🔧 **Dễ tùy chỉnh**: Cấu hình JSON đơn giản, linh hoạt

## Hướng dẫn cài đặt

### Yêu cầu hệ thống

Trước khi cài đặt bb-form, bạn cần có:

- **[Clojure babashka](https://babashka.org/)** - Runtime Clojure nhanh
- **[Charm-gum](https://github.com/charmbracelet/gum)** - Thư viện tạo giao diện terminal đẹp

### Cài đặt nhanh với bbin (Khuyến nghị)

Nếu bạn đã có [bbin](https://github.com/babashka/bbin) - công cụ quản lý script Clojure:

```bash
# Cài đặt từ GitHub
bbin install io.github.drringo/bb-form

# Hoặc cài đặt từ thư mục local (cho phát triển)
bbin install .
```

Sau khi cài đặt, bạn có thể sử dụng ngay:

```bash
bb-form form.json [--values values.json] [--out output.json] [field1:value1 ...]
```

### Cài đặt thủ công

Nếu không có bbin, bạn có thể chạy trực tiếp:

```bash
bb src/com/drbinhthanh/bb_form.clj form.json [--values values.json] [--out output.json] [field1:value1 ...]
```

## Hướng dẫn sử dụng

### Cách sử dụng cơ bản

1. **Tạo file form JSON**: Định nghĩa cấu trúc form của bạn
2. **Chạy form**: Sử dụng lệnh bb-form với file config
3. **Thu thập kết quả**: Dữ liệu được lưu vào file JSON

### Ví dụ sử dụng

```bash
# Chạy form cơ bản
bb-form form_sample.json

# Chạy form với giá trị mặc định
bb-form form_sample.json --values values.json

# Chạy form với file output tùy chỉnh
bb-form form_sample.json --out my_result.json

# Chạy form với giá trị từ command line
bb-form form_sample.json name:"Nguyễn Văn A" age:25
```

### Tạo file form JSON

Cấu trúc cơ bản của file form:

```json
{
  "title": "Tiêu đề form",
  "description": "Mô tả form",
  "fields": [
    {
      "id": "tên_field",
      "label": "Nhãn hiển thị",
      "type": "loại_field",
      "required": true/false,
      "options": ["lựa chọn 1", "lựa chọn 2"],
      "regex": "^[a-zA-Z0-9]+$",
      "branch": {
        "lựa chọn": [
          {
            "id": "field_con",
            "label": "Nhãn field con",
            "type": "loại_field",
            "required": true/false
          }
        ]
      }
    }
  ]
}
```

### Các loại field hỗ trợ

- **text**: Input văn bản (hỗ trợ regex validation)
- **number**: Input số nguyên với validation
- **date**: Input ngày tháng (format DD-MM-YYYY)
- **select**: Dropdown chọn một lựa chọn
- **multiselect**: Chọn nhiều lựa chọn

### Ví dụ form thực tế

Dự án có sẵn ví dụ form tìm kiếm đài radio:

```json
{
  "title": "Tùy chọn đài radio",
  "description": "Các phương thức để search ra đài radio phù hợp",
  "fields": [
    {
      "id": "searchMethod",
      "label": "chọn phương pháp tìm kiếm",
      "type": "select",
      "options": ["UUID", "Tìm theo tên", "Tìm theo quốc gia"],
      "required": true,
      "branch": {
        "UUID": [
          {
            "id": "uuid",
            "label": "Nhập uuid của đài radio",
            "type": "text",
            "required": false
          }
        ],
        "Tìm theo tên": [
          {
            "id": "searchByNameSearch",
            "label": "Tên đài cần tìm",
            "type": "text",
            "required": false
          }
        ],
        "Tìm theo quốc gia": [
          {
            "id": "searchbyNation",
            "label": "Kí hiệu quốc gia (2 chữ) cần tìm",
            "type": "text",
            "required": false
          }
        ]
      }
    }
  ]
}
```

## Tính năng nổi bật

### Giao diện người dùng tối ưu

- **Màn hình sạch sẽ**: Tự động xóa màn hình trước khi hiển thị form
- **Dòng trạng thái cố định**: Hiển thị thông báo lỗi ở vị trí cố định
- **Validation real-time**: Thông báo lỗi ngay lập tức khi nhập sai
- **Giao diện nhất quán**: Thiết kế thống nhất trong suốt quá trình

### Tính năng phân nhánh mạnh mẽ

- **Logic có điều kiện**: Hiển thị field con dựa trên lựa chọn
- **Hỗ trợ nhiều cấp**: Có thể tạo phân nhánh phức tạp
- **Tự động ẩn/hiện**: Field được quản lý thông minh

### Validation thông minh

- **Regex validation**: Hỗ trợ kiểm tra định dạng với regex
- **Thông báo lỗi tùy chỉnh**: Tạo thông báo lỗi riêng cho từng field
- **Validation đa dạng**: Số, ngày tháng, email, v.v.

## Kết quả đầu ra

Dữ liệu được lưu vào file JSON với cấu trúc rõ ràng:

```json
{
  "selectedByUser": {
    "name": "Nguyễn Văn A",
    "age": 25,
    "gender": "Nữ",
    "gender_branch": {
      "Nữ": {
        "is_pregnant": "Có",
        "is_pregnant_branch": {
          "Có": {
            "gestational_age": 20
          }
        }
      }
    },
    "symptoms": ["Sốt", "Khó thở"],
    "symptoms_branch": {
      "Sốt": {
        "temperature": 38.5
      },
      "Khó thở": {
        "breath_level": "Vừa"
      }
    }
  }
}
```

## Hứa hẹn tính năng mới

### Tính năng đang phát triển

🚀 **Tích hợp API**: Kết nối với các dịch vụ web để validate dữ liệu  
🎨 **Theme tùy chỉnh**: Cho phép thay đổi màu sắc và style giao diện  
📱 **Responsive design**: Tối ưu cho các terminal có kích thước khác nhau  
🔄 **Auto-save**: Tự động lưu tiến độ khi điền form dài  
📊 **Thống kê**: Hiển thị tiến độ và thời gian hoàn thành  
🔗 **Export đa dạng**: Xuất dữ liệu ra CSV, XML, YAML  
🌐 **Internationalization**: Hỗ trợ đa ngôn ngữ  
⚙️ **Plugin system**: Cho phép mở rộng với plugin tùy chỉnh

### Tính năng dự kiến

- **Form builder GUI**: Tạo form bằng giao diện đồ họa
- **Template library**: Thư viện form mẫu cho các trường hợp phổ biến
- **Cloud sync**: Đồng bộ form và dữ liệu qua cloud
- **Collaboration**: Chia sẻ và cộng tác trên form
- **Analytics**: Phân tích dữ liệu thu thập được

## Kết luận

**bb-form** là một công cụ mạnh mẽ và linh hoạt cho việc tạo form trong terminal. Với giao diện đẹp mắt, tính năng phân nhánh thông minh và validation mạnh mẽ, nó là giải pháp hoàn hảo cho các nhà phát triển cần thu thập dữ liệu từ người dùng qua command-line.

Dự án đang phát triển tích cực với nhiều tính năng mới hấp dẫn sắp được ra mắt. Hãy thử ngay và đóng góp ý kiến để giúp bb-form trở nên hoàn thiện hơn!

---

_bb-form - Tạo form terminal đẹp mắt với sức mạnh của Clojure_ ✨
