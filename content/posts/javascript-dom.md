---
title: "JavaScript DOM - Tương Tác Với Trang Web"
date: 2023-10-25
draft: false
tags: ["JavaScript", "DOM", "Web", "Lập Trình"]
categories: ["JavaScript"]
cover:
    image: "/images/posts/javascript-dom.svg"
    alt: "JavaScript DOM"
    caption: "Tương tác với DOM"
---

# JavaScript DOM - Tương Tác Với Trang Web

![JavaScript DOM](/images/posts/javascript-dom.svg)

Document Object Model (DOM) là một giao diện lập trình cho phép JavaScript tương tác với HTML và CSS, giúp tạo ra các trang web động và tương tác.

## DOM Là Gì?

DOM biểu diễn trang web dưới dạng cấu trúc cây, trong đó mỗi thẻ HTML là một nút (node). JavaScript có thể truy cập và thay đổi tất cả các phần tử trong cây DOM này.

```
document
└── html
    ├── head
    │   ├── title
    │   └── meta
    └── body
        ├── header
        ├── div
        │   ├── h1
        │   └── p
        └── footer
```

## Truy Cập Các Phần Tử DOM

JavaScript cung cấp nhiều phương thức để truy cập các phần tử DOM:

```javascript
// Truy cập theo ID
const tieuDe = document.getElementById("tieuDe");

// Truy cập theo tên thẻ
const doanVan = document.getElementsByTagName("p");

// Truy cập theo tên lớp
const mucLuc = document.getElementsByClassName("muc-luc");

// Truy cập bằng CSS selector
const nutBam = document.querySelector("#nut-bam");
const cacMucLuc = document.querySelectorAll(".muc-luc");
```

## Thay Đổi Nội Dung DOM

Sau khi truy cập được phần tử, bạn có thể thay đổi nội dung của nó:

```javascript
// Thay đổi nội dung văn bản
tieuDe.textContent = "Tiêu đề mới";

// Thay đổi HTML
tieuDe.innerHTML = "Tiêu đề <span style='color: red;'>mới</span>";

// Thay đổi thuộc tính
const hinhAnh = document.getElementById("hinh-anh");
hinhAnh.src = "duong-dan-moi.jpg";
hinhAnh.alt = "Mô tả mới";

// Thêm/xóa lớp CSS
tieuDe.classList.add("noi-bat");
tieuDe.classList.remove("an");
tieuDe.classList.toggle("hien-thi");

// Thay đổi kiểu trực tiếp
tieuDe.style.color = "blue";
tieuDe.style.fontSize = "24px";
tieuDe.style.fontWeight = "bold";
```

## Tạo và Xóa Phần Tử

JavaScript cho phép tạo và xóa các phần tử DOM:

```javascript
// Tạo phần tử mới
const doanVanMoi = document.createElement("p");
doanVanMoi.textContent = "Đây là đoạn văn mới.";

// Thêm phần tử vào DOM
document.body.appendChild(doanVanMoi);

// Thêm phần tử vào vị trí cụ thể
const phanNoiDung = document.getElementById("noi-dung");
phanNoiDung.insertBefore(doanVanMoi, phanNoiDung.firstChild);

// Xóa phần tử
const phanTuCanXoa = document.getElementById("phan-tu-can-xoa");
phanTuCanXoa.remove();

// Hoặc xóa thông qua phần tử cha
const phanTuCha = document.getElementById("phan-tu-cha");
const phanTuCon = document.getElementById("phan-tu-con");
phanTuCha.removeChild(phanTuCon);
```

## Xử Lý Sự Kiện

Sự kiện cho phép JavaScript phản hồi các hành động của người dùng:

```javascript
// Thêm trình xử lý sự kiện
const nutBam = document.getElementById("nut-bam");

nutBam.addEventListener("click", function() {
    alert("Bạn đã nhấn vào nút!");
});

// Sử dụng arrow function
nutBam.addEventListener("mouseover", () => {
    nutBam.style.backgroundColor = "lightblue";
});

nutBam.addEventListener("mouseout", () => {
    nutBam.style.backgroundColor = "";
});

// Xóa trình xử lý sự kiện
function xuLyClick() {
    alert("Xử lý click!");
}

nutBam.addEventListener("click", xuLyClick);
// Sau đó, khi không cần nữa
nutBam.removeEventListener("click", xuLyClick);
```

## Sự Kiện Phổ Biến

JavaScript hỗ trợ nhiều loại sự kiện:

```javascript
// Sự kiện chuột
element.addEventListener("click", xuLy);      // Nhấp chuột
element.addEventListener("dblclick", xuLy);   // Nhấp đúp
element.addEventListener("mouseover", xuLy);  // Di chuột vào
element.addEventListener("mouseout", xuLy);   // Di chuột ra
element.addEventListener("mousedown", xuLy);  // Nhấn chuột xuống
element.addEventListener("mouseup", xuLy);    // Thả chuột

// Sự kiện bàn phím
element.addEventListener("keydown", xuLy);    // Nhấn phím xuống
element.addEventListener("keyup", xuLy);      // Thả phím
element.addEventListener("keypress", xuLy);   // Nhấn phím (ký tự)

// Sự kiện form
form.addEventListener("submit", xuLy);        // Gửi form
input.addEventListener("change", xuLy);       // Thay đổi giá trị
input.addEventListener("focus", xuLy);        // Focus vào input
input.addEventListener("blur", xuLy);         // Mất focus

// Sự kiện window
window.addEventListener("load", xuLy);        // Trang đã tải xong
window.addEventListener("resize", xuLy);      // Thay đổi kích thước cửa sổ
window.addEventListener("scroll", xuLy);      // Cuộn trang
```

## Ví Dụ Thực Tế

### Ví dụ 1: Tạo danh sách động

```javascript
function themMucDanhSach() {
    // Lấy giá trị từ input
    const input = document.getElementById("muc-moi");
    const giaTriMoi = input.value.trim();
    
    if (giaTriMoi !== "") {
        // Tạo phần tử mới
        const mucMoi = document.createElement("li");
        mucMoi.textContent = giaTriMoi;
        
        // Thêm nút xóa
        const nutXoa = document.createElement("button");
        nutXoa.textContent = "Xóa";
        nutXoa.className = "nut-xoa";
        nutXoa.onclick = function() {
            mucMoi.remove();
        };
        
        mucMoi.appendChild(nutXoa);
        
        // Thêm vào danh sách
        document.getElementById("danh-sach").appendChild(mucMoi);
        
        // Xóa giá trị input
        input.value = "";
    }
}

// Thêm sự kiện cho nút
document.getElementById("nut-them").addEventListener("click", themMucDanhSach);
```

### Ví dụ 2: Xác thực form

```javascript
document.getElementById("form-dang-ky").addEventListener("submit", function(event) {
    let coLoi = false;
    
    // Kiểm tra tên
    const ten = document.getElementById("ten").value.trim();
    if (ten === "") {
        document.getElementById("loi-ten").textContent = "Vui lòng nhập tên";
        coLoi = true;
    } else {
        document.getElementById("loi-ten").textContent = "";
    }
    
    // Kiểm tra email
    const email = document.getElementById("email").value.trim();
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailRegex.test(email)) {
        document.getElementById("loi-email").textContent = "Email không hợp lệ";
        coLoi = true;
    } else {
        document.getElementById("loi-email").textContent = "";
    }
    
    // Nếu có lỗi, ngăn form gửi đi
    if (coLoi) {
        event.preventDefault();
    }
});
```

## Kết Luận

DOM là một công cụ mạnh mẽ cho phép JavaScript tương tác với trang web, tạo ra trải nghiệm người dùng động và tương tác. Hiểu và sử dụng DOM hiệu quả là kỹ năng cần thiết cho bất kỳ nhà phát triển web nào.

Trong các bài viết tiếp theo, chúng ta sẽ tìm hiểu về các thư viện và framework JavaScript hiện đại như React, Vue.js, và Angular, giúp đơn giản hóa việc thao tác DOM và xây dựng ứng dụng web phức tạp.