---
title: "Giới Thiệu Về JavaScript - Ngôn Ngữ Của Web"
date: 2023-10-28
draft: false
tags: ["JavaScript", "Web", "Frontend"]
categories: ["JavaScript"]
cover:
    image: "/images/posts/javascript-header.svg"
    alt: "JavaScript Programming"
    caption: "Ngôn ngữ lập trình JavaScript"
---

# Giới Thiệu Về JavaScript - Ngôn Ngữ Của Web

![JavaScript Logo](/images/posts/javascript-header.svg)

JavaScript là ngôn ngữ lập trình phổ biến nhất trên web, cho phép tạo ra các trang web động và tương tác với người dùng.

## Lịch Sử JavaScript

JavaScript được tạo ra bởi Brendan Eich tại Netscape vào năm 1995, ban đầu có tên là Mocha, sau đó đổi thành LiveScript và cuối cùng là JavaScript. Mặc dù có "Java" trong tên, nhưng JavaScript hoàn toàn khác biệt với Java.

## Đặc Điểm Của JavaScript

1. **Ngôn ngữ kịch bản phía client**: JavaScript chủ yếu chạy trên trình duyệt của người dùng.
2. **Đa nền tảng**: Hoạt động trên nhiều trình duyệt và thiết bị khác nhau.
3. **Hướng đối tượng**: Sử dụng các khái niệm lập trình hướng đối tượng.
4. **Động**: Kiểu dữ liệu được xác định tại thời điểm chạy.
5. **Xử lý sự kiện**: Cho phép phản hồi các hành động của người dùng.

## Cách Sử Dụng JavaScript

JavaScript có thể được nhúng trực tiếp vào HTML hoặc được liên kết từ một tệp riêng biệt.

### Nhúng Trực Tiếp

```html
<!DOCTYPE html>
<html>
<head>
    <title>JavaScript Demo</title>
    <script>
        function xinChao() {
            alert("Xin chào từ JavaScript!");
        }
    </script>
</head>
<body>
    <button onclick="xinChao()">Nhấn vào đây</button>
</body>
</html>
```

### Liên Kết Từ Tệp Ngoài

```html
<!DOCTYPE html>
<html>
<head>
    <title>JavaScript Demo</title>
    <script src="script.js"></script>
</head>
<body>
    <button onclick="xinChao()">Nhấn vào đây</button>
</body>
</html>
```

Với nội dung tệp script.js:

```javascript
function xinChao() {
    alert("Xin chào từ JavaScript!");
}
```

## Cú Pháp Cơ Bản

### Biến và Kiểu Dữ Liệu

JavaScript có ba cách khai báo biến: var, let, và const.

```javascript
// Khai báo biến với var (phạm vi function)
var x = 10;

// Khai báo biến với let (phạm vi block)
let y = 20;

// Khai báo hằng số với const
const PI = 3.14;

// Các kiểu dữ liệu
let so = 10;                // Number
let chuoi = "JavaScript";   // String
let dung = true;            // Boolean
let mang = [1, 2, 3];       // Array
let doiTuong = {            // Object
    ten: "JavaScript",
    namRaMat: 1995
};
let khongXacDinh = undefined; // Undefined
let khongCoGiaTri = null;     // Null
```

### Hàm

```javascript
// Khai báo hàm
function tinhTong(a, b) {
    return a + b;
}

// Gọi hàm
let tong = tinhTong(5, 3);
console.log("Tổng: " + tong);

// Arrow function (ES6)
const nhan = (a, b) => a * b;
console.log("Tích: " + nhan(5, 3));
```

### Điều Kiện và Vòng Lặp

```javascript
// Câu lệnh if-else
let diem = 85;

if (diem >= 90) {
    console.log("Xuất sắc");
} else if (diem >= 80) {
    console.log("Giỏi");
} else if (diem >= 70) {
    console.log("Khá");
} else {
    console.log("Trung bình");
}

// Vòng lặp for
for (let i = 0; i < 5; i++) {
    console.log("Số: " + i);
}

// Vòng lặp while
let j = 0;
while (j < 5) {
    console.log("Số: " + j);
    j++;
}

// Vòng lặp for...of (ES6)
let mang = [1, 2, 3, 4, 5];
for (let phanTu of mang) {
    console.log(phanTu);
}

// Vòng lặp for...in
let doiTuong = {
    ten: "JavaScript",
    namRaMat: 1995,
    tacGia: "Brendan Eich"
};

for (let thuocTinh in doiTuong) {
    console.log(thuocTinh + ": " + doiTuong[thuocTinh]);
}
```

## DOM Manipulation

JavaScript có thể thay đổi nội dung, cấu trúc và kiểu của trang web thông qua Document Object Model (DOM).

```javascript
// Lấy phần tử theo ID
let tieuDe = document.getElementById("tieuDe");

// Thay đổi nội dung
tieuDe.innerHTML = "Tiêu đề mới";

// Thay đổi kiểu
tieuDe.style.color = "blue";
tieuDe.style.fontSize = "24px";

// Tạo phần tử mới
let doanVan = document.createElement("p");
doanVan.innerHTML = "Đây là một đoạn văn mới.";

// Thêm phần tử vào trang
document.body.appendChild(doanVan);

// Xử lý sự kiện
let nutBam = document.getElementById("nutBam");
nutBam.addEventListener("click", function() {
    alert("Bạn đã nhấn vào nút!");
});
```

## Xử Lý Bất Đồng Bộ

JavaScript xử lý các tác vụ bất đồng bộ thông qua callbacks, promises, và async/await.

```javascript
// Callback
function taiDuLieu(callback) {
    setTimeout(function() {
        console.log("Đã tải dữ liệu");
        callback("Dữ liệu");
    }, 2000);
}

taiDuLieu(function(data) {
    console.log("Dữ liệu nhận được: " + data);
});

// Promise
function taiDuLieuPromise() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            console.log("Đã tải dữ liệu");
            resolve("Dữ liệu");
        }, 2000);
    });
}

taiDuLieuPromise()
    .then(data => console.log("Dữ liệu nhận được: " + data))
    .catch(error => console.error("Lỗi: " + error));

// Async/Await (ES8)
async function xuLyDuLieu() {
    try {
        const data = await taiDuLieuPromise();
        console.log("Dữ liệu nhận được: " + data);
    } catch (error) {
        console.error("Lỗi: " + error);
    }
}

xuLyDuLieu();
```

## Kết Luận

JavaScript là một ngôn ngữ mạnh mẽ và linh hoạt, đóng vai trò quan trọng trong phát triển web hiện đại. Với sự phát triển không ngừng của các framework và thư viện như React, Angular, và Vue.js, JavaScript đã mở rộng phạm vi của mình từ phía client sang cả phía server (Node.js).

Trong các bài viết tiếp theo, chúng ta sẽ đi sâu hơn vào các khía cạnh nâng cao của JavaScript như ES6+, các framework phổ biến, và các kỹ thuật tối ưu hiệu suất.