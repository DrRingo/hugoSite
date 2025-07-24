---
title: "Org-mode Linking by ID: Giải pháp liên kết thông minh cho Emacs"
author: ["Nguyễn Bình Thành"]
publishDate: 2025-07-19T16:26:00+07:00
categories: ["shell"]
draft: false
featured_image: "/assets/img/fish/cyprinus-dobula.jpg"
---

## Giới thiệu {#giới-thiệu}

**Orgmode-linked-by-id** là extension cho Emacs Org-mode giúp bạn tạo liên
kết chéo bền vững giữa các tiêu đề, hình ảnh, bảng bằng ID thay vì tên
tiêu đề. Điều này giải quyết triệt để vấn đề link bị hỏng khi đổi tên
header, đồng thời giúp bạn dễ dàng tham chiếu đến bất kỳ mục nào trong
ghi chú, kể cả khi tài liệu lớn hoặc nhiều file.


## Tại sao nên dùng liên kết bằng ID? {#tại-sao-nên-dùng-liên-kết-bằng-id}

-   **Ổn định:** Khi đổi tên tiêu đề, liên kết truyền thống sẽ hỏng, còn
    liên kết theo ID luôn hoạt động.
-   **Tự động:** Không cần nghĩ tên ID thủ công, chỉ cần dùng
    `org-id-get-create` (thường là `SPC m I`).
-   **Tìm kiếm nhanh:** Có thể tìm và chèn liên kết đến bất kỳ tiêu đề, hình
    ảnh, bảng nào trong file hoặc thư mục với fuzzy search (Helm).


## Các tính năng chính {#các-tính-năng-chính}

1.  **Liên kết header trong file hiện tại**
    -   Phím tắt: `C-c l i` (hoặc `SPC l i` với Doom)
    -   Tìm tất cả header có ID trong file đang mở, chọn từ danh sách và
        chèn liên kết ID vào vị trí con trỏ.
2.  **Liên kết header trong thư mục**
    -   Phím tắt: `C-c l f` (hoặc `SPC l f`)
    -   Tìm header có ID trong tất cả file `.org` trong thư mục (không bao
        gồm thư mục con), fuzzy search với Helm, chọn tương tác.
3.  **Liên kết đến hình ảnh/bảng có tên**
    -   Phím tắt: `C-c l c` (hoặc `SPC l c`)
    -   Tìm đối tượng có `#+NAME` và `#+CAPTION`, hiển thị danh sách
        caption cho người dùng chọn, cho phép tuỳ chỉnh mô tả liên kết.


## Cài đặt {#cài-đặt}


### Doom Emacs {#doom-emacs}

1.  Thêm vào `~/.config/doom/packages.el`:
    ```elisp
          (package! orgmode-linked-by-id
            :recipe (:host github :repo "drringo/orgmode-linked-by-id"))
    ```

2.  Chạy `doom sync` và khởi động lại Emacs.

3.  Thêm vào `~/.config/doom/config.el`:
    ```elisp
          (require 'orgmode-linked-by-id)
    ```

4.  (Tùy chọn) Nếu muốn dùng phím tắt kiểu Doom (`SPC l i`...), thêm:
    ```elisp
          (when (fboundp 'map!)
            (map! :leader
                  (:prefix ("l" . "org link by id")
                   :desc "Insert ID in file"   "i" #'drringo/org-get-headers-with-ids
                   :desc "Insert ID in folder" "f" #'drringo/org-get-headers-with-ids-in-folder
                   :desc "Insert entity link"  "c" #'drringo/helm-insert-org-image-link-with-custom-caption)))
    ```


### Emacs thường {#emacs-thường}

1.  Clone repo:
    ```sh
          git clone https://github.com/drringo/orgmode-linked-by-id.git ~/.emacs.d/lisp/orgmode-linked-by-id
    ```

2.  Thêm vào `init.el` hoặc `.emacs`:
    ```elisp
          (add-to-list 'load-path "~/.emacs.d/lisp/orgmode-linked-by-id")
          (require 'orgmode-linked-by-id)
    ```


## Hướng dẫn sử dụng {#hướng-dẫn-sử-dụng}


### Quy trình cơ bản {#quy-trình-cơ-bản}

1.  **Tạo ID cho header:** Đặt con trỏ vào tiêu đề, dùng `SPC m I` (hoặc
    `org-id-get-create`).
2.  **Chèn liên kết:** Dùng phím tắt tương ứng (`C-c l i`, `C-c l f`,
    `C-c l c`).
3.  **Chọn header/đối tượng:** Từ danh sách hiển thị (Helm).
4.  **Tùy chỉnh mô tả:** Có thể sửa description trước khi chèn link.


### Ví dụ {#ví-dụ}

```org
* Môn học: Lập trình Python
:PROPERTIES:
:ID: python-course
:END:

* Bài 1: Giới thiệu Python
:PROPERTIES:
:ID: python-intro
:END:

Nội dung tham chiếu đến [[id:python-intro][Bài 1]].
```

```org
#+NAME: my-image
#+CAPTION: Hình ảnh mẫu
[[file:image.png]]

Liên kết đến [[my-image][Hình ảnh mẫu]].
```


## So sánh với phương pháp truyền thống {#so-sánh-với-phương-pháp-truyền-thống}

| Phương pháp truyền thống        | Extension này                |
|---------------------------------|------------------------------|
| `[[*Header name][Header name]]` | `[[id:abc123][Header name]]` |
| Hỏng khi header thay đổi        | Vẫn hoạt động                |
| Khó tìm kiếm                    | Tìm kiếm dễ dàng             |


## Lưu ý {#lưu-ý}

-   Extension tương thích cả Doom Emacs và Emacs thường.
-   Không dùng `map!` trong file package, chỉ dùng trong config cá nhân
    nếu bạn dùng Doom.
-   Tất cả phím tắt đều có sẵn qua `global-set-key`.


## Đóng góp &amp; Liên hệ {#đóng-góp-liên-hệ}

-   **Repository:** <https://github.com/drringo/orgmode-linked-by-id>
-   **Issues:** <https://github.com/drringo/orgmode-linked-by-id/issues>

---

_Extension này được phát triển để tối ưu trải nghiệm liên kết trong
Org-mode. Mọi đóng góp, phản hồi đều được hoan nghênh!_
