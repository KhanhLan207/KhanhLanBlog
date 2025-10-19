---
title: "Lập Trình Hướng Đối Tượng Trong Java"
date: 2023-10-21
draft: false
tags: ["Java", "OOP", "Lập Trình"]
categories: ["Java"]
cover:
  image: "/KhanhLanBlog/images/posts/java-oop.svg"
  alt: "Java OOP"
  caption: "Lập trình hướng đối tượng trong Java"
---

# Lập Trình Hướng Đối Tượng Trong Java

![Java OOP](/KhanhLanBlog/images/posts/java-oop.svg)

Lập trình hướng đối tượng (Object-Oriented Programming - OOP) là một trong những đặc điểm quan trọng nhất của Java. Bài viết này sẽ giới thiệu các khái niệm cơ bản về OOP trong Java.

## Các Nguyên Lý Cơ Bản Của OOP

### 1. Tính Đóng Gói (Encapsulation)

Tính đóng gói cho phép ẩn các chi tiết triển khai và chỉ hiển thị chức năng cần thiết cho người dùng.

```java
public class SinhVien {
    // Thuộc tính private
    private String hoTen;
    private int tuoi;

    // Getter và Setter
    public String getHoTen() {
        return hoTen;
    }

    public void setHoTen(String hoTen) {
        this.hoTen = hoTen;
    }

    public int getTuoi() {
        return tuoi;
    }

    public void setTuoi(int tuoi) {
        if (tuoi > 0) {
            this.tuoi = tuoi;
        }
    }
}
```

### 2. Tính Kế Thừa (Inheritance)

Tính kế thừa cho phép một lớp (lớp con) kế thừa các thuộc tính và phương thức từ một lớp khác (lớp cha).

```java
// Lớp cha
public class NguoiDung {
    protected String tenDangNhap;
    protected String matKhau;

    public void dangNhap() {
        System.out.println("Đăng nhập với tên: " + tenDangNhap);
    }
}

// Lớp con
public class QuanTriVien extends NguoiDung {
    private int capDoQuyen;

    public void quanLyHeThong() {
        System.out.println("Quản lý hệ thống với quyền cấp: " + capDoQuyen);
    }
}
```

### 3. Tính Đa Hình (Polymorphism)

Tính đa hình cho phép các đối tượng của các lớp khác nhau được xử lý thông qua một giao diện chung.

```java
// Lớp cha
public class HinhHoc {
    public double tinhDienTich() {
        return 0;
    }
}

// Lớp con 1
public class HinhTron extends HinhHoc {
    private double banKinh;

    public HinhTron(double banKinh) {
        this.banKinh = banKinh;
    }

    @Override
    public double tinhDienTich() {
        return Math.PI * banKinh * banKinh;
    }
}

// Lớp con 2
public class HinhChuNhat extends HinhHoc {
    private double chieuDai;
    private double chieuRong;

    public HinhChuNhat(double chieuDai, double chieuRong) {
        this.chieuDai = chieuDai;
        this.chieuRong = chieuRong;
    }

    @Override
    public double tinhDienTich() {
        return chieuDai * chieuRong;
    }
}

// Sử dụng tính đa hình
public class Main {
    public static void main(String[] args) {
        HinhHoc hinh1 = new HinhTron(5);
        HinhHoc hinh2 = new HinhChuNhat(4, 6);

        System.out.println("Diện tích hình tròn: " + hinh1.tinhDienTich());
        System.out.println("Diện tích hình chữ nhật: " + hinh2.tinhDienTich());
    }
}
```

### 4. Tính Trừu Tượng (Abstraction)

Tính trừu tượng cho phép tập trung vào những gì một đối tượng làm thay vì cách nó thực hiện.

```java
// Lớp trừu tượng
public abstract class DongVat {
    protected String ten;

    public abstract void keu();

    public void an() {
        System.out.println(ten + " đang ăn...");
    }
}

// Lớp con triển khai
public class Cho extends DongVat {
    public Cho(String ten) {
        this.ten = ten;
    }

    @Override
    public void keu() {
        System.out.println(ten + " kêu: Gâu gâu!");
    }
}

public class Meo extends DongVat {
    public Meo(String ten) {
        this.ten = ten;
    }

    @Override
    public void keu() {
        System.out.println(ten + " kêu: Meo meo!");
    }
}
```

## Lớp Và Đối Tượng Trong Java

### Lớp (Class)

Lớp là một bản thiết kế hoặc nguyên mẫu để tạo ra các đối tượng. Nó định nghĩa các thuộc tính và phương thức mà các đối tượng của lớp đó sẽ có.

```java
public class SanPham {
    // Thuộc tính
    private String ten;
    private double gia;
    private int soLuong;

    // Constructor
    public SanPham(String ten, double gia, int soLuong) {
        this.ten = ten;
        this.gia = gia;
        this.soLuong = soLuong;
    }

    // Phương thức
    public double tinhTongGia() {
        return gia * soLuong;
    }

    public void hienThiThongTin() {
        System.out.println("Tên: " + ten);
        System.out.println("Giá: " + gia);
        System.out.println("Số lượng: " + soLuong);
        System.out.println("Tổng giá: " + tinhTongGia());
    }
}
```

### Đối Tượng (Object)

Đối tượng là một thể hiện của lớp, được tạo ra từ bản thiết kế của lớp.

```java
public class Main {
    public static void main(String[] args) {
        // Tạo đối tượng từ lớp SanPham
        SanPham sp1 = new SanPham("Laptop", 15000000, 2);
        SanPham sp2 = new SanPham("Điện thoại", 8000000, 3);

        // Sử dụng các phương thức của đối tượng
        sp1.hienThiThongTin();
        sp2.hienThiThongTin();
    }
}
```

## Kết Luận

Lập trình hướng đối tượng là một phương pháp mạnh mẽ trong Java, giúp tổ chức mã nguồn một cách có cấu trúc, dễ bảo trì và mở rộng. Hiểu và áp dụng đúng các nguyên lý OOP sẽ giúp bạn trở thành một lập trình viên Java giỏi.

Trong các bài viết tiếp theo, chúng ta sẽ tìm hiểu sâu hơn về các khía cạnh nâng cao của OOP trong Java như interface, lớp trừu tượng, và các mẫu thiết kế phổ biến.
