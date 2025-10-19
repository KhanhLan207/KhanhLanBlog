---
title: "JavaScript ES6 - Những Tính Năng Hiện Đại"
date: 2023-10-24
draft: false
tags: ["JavaScript", "ES6", "Lập Trình"]
categories: ["JavaScript"]
cover:
  image: "/images/posts/javascript-es6.svg"
  alt: "JavaScript ES6"
  caption: "Những tính năng hiện đại"
---

# JavaScript ES6 - Những Tính Năng Hiện Đại

![JavaScript ES6](/KhanhLanBlog/images/posts/javascript-es6.svg)

ECMAScript 6 (ES6), còn được gọi là ECMAScript 2015, là một bản cập nhật lớn cho JavaScript, giới thiệu nhiều tính năng mới giúp viết mã dễ dàng và hiệu quả hơn.

## Các Tính Năng Chính Của ES6

### 1. Let và Const

ES6 giới thiệu hai từ khóa mới để khai báo biến: `let` và `const`.

```javascript
// let - phạm vi block
let x = 10;
if (true) {
  let x = 20; // Biến x khác với x ở ngoài
  console.log(x); // 20
}
console.log(x); // 10

// const - hằng số
const PI = 3.14;
// PI = 3.15; // Lỗi: không thể gán lại giá trị cho hằng số
```

### 2. Arrow Functions

Arrow functions cung cấp cú pháp ngắn gọn hơn để viết biểu thức hàm.

```javascript
// Hàm thông thường
function tong(a, b) {
  return a + b;
}

// Arrow function
const tongArrow = (a, b) => a + b;

// Arrow function với nhiều dòng
const kiemTra = (so) => {
  if (so > 0) {
    return "Dương";
  } else {
    return "Âm hoặc Zero";
  }
};
```

### 3. Template Literals

Template literals cho phép nhúng biểu thức vào chuỗi và viết chuỗi nhiều dòng dễ dàng.

```javascript
const ten = "JavaScript";
const nam = 1995;

// Chuỗi thông thường
console.log("Ngôn ngữ " + ten + " ra đời năm " + nam);

// Template literal
console.log(`Ngôn ngữ ${ten} ra đời năm ${nam}`);

// Chuỗi nhiều dòng
const html = `
<div>
    <h1>Tiêu đề</h1>
    <p>Đoạn văn</p>
</div>
`;
```

### 4. Destructuring Assignment

Destructuring cho phép trích xuất dữ liệu từ mảng hoặc đối tượng vào các biến riêng biệt.

```javascript
// Destructuring mảng
const mang = [1, 2, 3];
const [a, b, c] = mang;
console.log(a, b, c); // 1 2 3

// Destructuring đối tượng
const nguoi = {
  ten: "Nguyễn Văn A",
  tuoi: 30,
  diaChi: "Hà Nội",
};

const { ten, tuoi, diaChi } = nguoi;
console.log(ten, tuoi, diaChi); // Nguyễn Văn A 30 Hà Nội

// Đổi tên biến khi destructuring
const { ten: hoTen, tuoi: namSinh } = nguoi;
console.log(hoTen, namSinh); // Nguyễn Văn A 30
```

### 5. Default Parameters

ES6 cho phép thiết lập giá trị mặc định cho tham số hàm.

```javascript
function xinChao(ten = "Bạn") {
  console.log(`Xin chào, ${ten}!`);
}

xinChao(); // Xin chào, Bạn!
xinChao("Nguyễn Văn A"); // Xin chào, Nguyễn Văn A!
```

### 6. Rest Parameters và Spread Operator

Rest parameters cho phép biểu diễn một số lượng đối số không xác định dưới dạng một mảng.

```javascript
function tinhTong(...soHang) {
  return soHang.reduce((tong, so) => tong + so, 0);
}

console.log(tinhTong(1, 2, 3, 4, 5)); // 15
```

Spread operator cho phép mở rộng một mảng hoặc đối tượng.

```javascript
// Mở rộng mảng
const mang1 = [1, 2, 3];
const mang2 = [...mang1, 4, 5];
console.log(mang2); // [1, 2, 3, 4, 5]

// Mở rộng đối tượng
const nguoi = {
  ten: "Nguyễn Văn A",
  tuoi: 30,
};

const nguoiChiTiet = {
  ...nguoi,
  diaChi: "Hà Nội",
  ngheNghiep: "Lập trình viên",
};

console.log(nguoiChiTiet);
// { ten: "Nguyễn Văn A", tuoi: 30, diaChi: "Hà Nội", ngheNghiep: "Lập trình viên" }
```

### 7. Classes

ES6 giới thiệu cú pháp lớp, giúp lập trình hướng đối tượng dễ dàng hơn.

```javascript
class NguoiDung {
  constructor(ten, email) {
    this.ten = ten;
    this.email = email;
  }

  xinChao() {
    console.log(`Xin chào, tôi là ${this.ten}`);
  }

  static kiemTraEmail(email) {
    return email.includes("@");
  }
}

const nguoiDung = new NguoiDung("Nguyễn Văn A", "nguyenvana@example.com");
nguoiDung.xinChao(); // Xin chào, tôi là Nguyễn Văn A

// Kế thừa
class QuanTriVien extends NguoiDung {
  constructor(ten, email, quyen) {
    super(ten, email);
    this.quyen = quyen;
  }

  kiemTraQuyen() {
    console.log(`${this.ten} có quyền: ${this.quyen}`);
  }
}

const admin = new QuanTriVien("Admin", "admin@example.com", "Toàn quyền");
admin.xinChao(); // Xin chào, tôi là Admin
admin.kiemTraQuyen(); // Admin có quyền: Toàn quyền
```

### 8. Promises

Promises cung cấp một cách tốt hơn để xử lý các hoạt động bất đồng bộ.

```javascript
function taiDuLieu(url) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (url) {
        resolve(`Dữ liệu từ ${url}`);
      } else {
        reject("URL không hợp lệ");
      }
    }, 1000);
  });
}

taiDuLieu("api.example.com/data")
  .then((data) => console.log(data))
  .catch((error) => console.error(error));
```

### 9. Modules

ES6 giới thiệu hệ thống module tích hợp, cho phép chia mã thành các phần nhỏ hơn, dễ quản lý.

```javascript
// math.js
export function tinhTong(a, b) {
  return a + b;
}

export function tinhHieu(a, b) {
  return a - b;
}

// main.js
import { tinhTong, tinhHieu } from "./math.js";

console.log(tinhTong(5, 3)); // 8
console.log(tinhHieu(5, 3)); // 2

// Hoặc import tất cả
import * as Math from "./math.js";

console.log(Math.tinhTong(5, 3)); // 8
console.log(Math.tinhHieu(5, 3)); // 2
```

## Kết Luận

ES6 đã mang lại nhiều cải tiến đáng kể cho JavaScript, giúp mã nguồn trở nên sạch sẽ, dễ đọc và dễ bảo trì hơn. Các tính năng này đã trở thành tiêu chuẩn trong phát triển JavaScript hiện đại.

Trong các bài viết tiếp theo, chúng ta sẽ tìm hiểu về các tính năng mới trong các phiên bản ECMAScript sau ES6, cũng như các framework và thư viện JavaScript phổ biến.
