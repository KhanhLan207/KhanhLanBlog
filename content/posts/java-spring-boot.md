---
title: "Spring Boot - Framework Java Hiện Đại"
date: 2023-10-28
draft: false
tags: ["Java", "Spring Boot", "Framework", "Backend"]
categories: ["Java"]
cover:
  image: "/KhanhLanBlog/images/posts/spring-boot.svg"
  alt: "Spring Boot Framework"
  caption: "Framework Java hiện đại"
---

# Spring Boot - Framework Java Hiện Đại

![Spring Boot](/KhanhLanBlog/images/posts/spring-boot.svg)

Spring Boot là một framework phổ biến cho phát triển ứng dụng Java, giúp đơn giản hóa quá trình cấu hình và triển khai ứng dụng Spring.

## Giới Thiệu Về Spring Boot

Spring Boot là một phần của hệ sinh thái Spring Framework, được phát triển bởi Pivotal Team. Nó cung cấp cách tiếp cận "opinionated" để xây dựng ứng dụng Spring, giúp giảm thiểu thời gian cấu hình và tăng năng suất phát triển.

## Ưu Điểm Của Spring Boot

1. **Cấu hình tự động**: Spring Boot tự động cấu hình ứng dụng dựa trên các phụ thuộc có trong classpath.
2. **Máy chủ nhúng**: Tích hợp sẵn Tomcat, Jetty hoặc Undertow, không cần triển khai WAR files.
3. **Starter dependencies**: Đơn giản hóa cấu hình Maven/Gradle với các starter dependencies.
4. **Actuator**: Cung cấp các tính năng sẵn có để giám sát và quản lý ứng dụng.
5. **Không cần XML**: Cấu hình dựa trên Java, annotations và YAML/properties.

## Tạo Ứng Dụng Spring Boot Đầu Tiên

### Sử Dụng Spring Initializr

Cách đơn giản nhất để tạo ứng dụng Spring Boot là sử dụng [Spring Initializr](https://start.spring.io/):

1. Truy cập https://start.spring.io/
2. Chọn Maven hoặc Gradle
3. Chọn ngôn ngữ Java
4. Chọn phiên bản Spring Boot
5. Điền thông tin Group, Artifact
6. Thêm các dependencies (ví dụ: Spring Web, JPA, MySQL)
7. Tạo và tải về dự án

### Cấu Trúc Dự Án

```
my-spring-boot-app/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── example/
│   │   │           └── myapp/
│   │   │               ├── MySpringBootApplication.java
│   │   │               ├── controller/
│   │   │               ├── model/
│   │   │               ├── repository/
│   │   │               └── service/
│   │   └── resources/
│   │       ├── application.properties
│   │       ├── static/
│   │       └── templates/
│   └── test/
│       └── java/
│           └── com/
│               └── example/
│                   └── myapp/
│                       └── MySpringBootApplicationTests.java
├── pom.xml (hoặc build.gradle)
└── README.md
```

### Lớp Chính

```java
package com.example.myapp;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class MySpringBootApplication {
    public static void main(String[] args) {
        SpringApplication.run(MySpringBootApplication.class, args);
    }
}
```

## Xây Dựng REST API

### Model

```java
package com.example.myapp.model;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class SanPham {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String ten;
    private String moTa;
    private double gia;

    // Constructors, Getters và Setters

    public SanPham() {
    }

    public SanPham(String ten, String moTa, double gia) {
        this.ten = ten;
        this.moTa = moTa;
        this.gia = gia;
    }

    // Getters và Setters
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getTen() {
        return ten;
    }

    public void setTen(String ten) {
        this.ten = ten;
    }

    public String getMoTa() {
        return moTa;
    }

    public void setMoTa(String moTa) {
        this.moTa = moTa;
    }

    public double getGia() {
        return gia;
    }

    public void setGia(double gia) {
        this.gia = gia;
    }
}
```

### Repository

```java
package com.example.myapp.repository;

import com.example.myapp.model.SanPham;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

import java.util.List;

@Repository
public interface SanPhamRepository extends JpaRepository<SanPham, Long> {
    List<SanPham> findByTenContaining(String ten);
}
```

### Service

```java
package com.example.myapp.service;

import com.example.myapp.model.SanPham;
import com.example.myapp.repository.SanPhamRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;
import java.util.Optional;

@Service
public class SanPhamService {

    private final SanPhamRepository sanPhamRepository;

    @Autowired
    public SanPhamService(SanPhamRepository sanPhamRepository) {
        this.sanPhamRepository = sanPhamRepository;
    }

    public List<SanPham> layTatCaSanPham() {
        return sanPhamRepository.findAll();
    }

    public Optional<SanPham> laySanPhamTheoId(Long id) {
        return sanPhamRepository.findById(id);
    }

    public List<SanPham> timSanPhamTheoTen(String ten) {
        return sanPhamRepository.findByTenContaining(ten);
    }

    public SanPham luuSanPham(SanPham sanPham) {
        return sanPhamRepository.save(sanPham);
    }

    public void xoaSanPham(Long id) {
        sanPhamRepository.deleteById(id);
    }
}
```

### Controller

```java
package com.example.myapp.controller;

import com.example.myapp.model.SanPham;
import com.example.myapp.service.SanPhamService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import java.util.List;
import java.util.Optional;

@RestController
@RequestMapping("/api/sanpham")
public class SanPhamController {

    private final SanPhamService sanPhamService;

    @Autowired
    public SanPhamController(SanPhamService sanPhamService) {
        this.sanPhamService = sanPhamService;
    }

    @GetMapping
    public ResponseEntity<List<SanPham>> layTatCaSanPham() {
        List<SanPham> danhSachSanPham = sanPhamService.layTatCaSanPham();
        return new ResponseEntity<>(danhSachSanPham, HttpStatus.OK);
    }

    @GetMapping("/{id}")
    public ResponseEntity<SanPham> laySanPhamTheoId(@PathVariable Long id) {
        Optional<SanPham> sanPham = sanPhamService.laySanPhamTheoId(id);
        return sanPham.map(value -> new ResponseEntity<>(value, HttpStatus.OK))
                .orElseGet(() -> new ResponseEntity<>(HttpStatus.NOT_FOUND));
    }

    @GetMapping("/tim")
    public ResponseEntity<List<SanPham>> timSanPhamTheoTen(@RequestParam String ten) {
        List<SanPham> danhSachSanPham = sanPhamService.timSanPhamTheoTen(ten);
        return new ResponseEntity<>(danhSachSanPham, HttpStatus.OK);
    }

    @PostMapping
    public ResponseEntity<SanPham> themSanPham(@RequestBody SanPham sanPham) {
        SanPham sanPhamMoi = sanPhamService.luuSanPham(sanPham);
        return new ResponseEntity<>(sanPhamMoi, HttpStatus.CREATED);
    }

    @PutMapping("/{id}")
    public ResponseEntity<SanPham> capNhatSanPham(@PathVariable Long id, @RequestBody SanPham sanPham) {
        Optional<SanPham> sanPhamHienTai = sanPhamService.laySanPhamTheoId(id);

        if (sanPhamHienTai.isPresent()) {
            sanPham.setId(id);
            SanPham sanPhamCapNhat = sanPhamService.luuSanPham(sanPham);
            return new ResponseEntity<>(sanPhamCapNhat, HttpStatus.OK);
        } else {
            return new ResponseEntity<>(HttpStatus.NOT_FOUND);
        }
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void> xoaSanPham(@PathVariable Long id) {
        Optional<SanPham> sanPham = sanPhamService.laySanPhamTheoId(id);

        if (sanPham.isPresent()) {
            sanPhamService.xoaSanPham(id);
            return new ResponseEntity<>(HttpStatus.NO_CONTENT);
        } else {
            return new ResponseEntity<>(HttpStatus.NOT_FOUND);
        }
    }
}
```

## Cấu Hình Cơ Sở Dữ Liệu

### application.properties

```properties
# Cấu hình cơ sở dữ liệu
spring.datasource.url=jdbc:mysql://localhost:3306/myapp_db
spring.datasource.username=root
spring.datasource.password=password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# Cấu hình JPA/Hibernate
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect

# Cấu hình server
server.port=8080
```

## Spring Boot Security

Spring Security giúp bảo mật ứng dụng Spring Boot:

```java
package com.example.myapp.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.provisioning.InMemoryUserDetailsManager;
import org.springframework.security.web.SecurityFilterChain;

@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .antMatchers("/", "/home").permitAll()
                .antMatchers("/api/**").authenticated()
                .and()
            .formLogin()
                .loginPage("/login")
                .permitAll()
                .and()
            .logout()
                .permitAll();

        return http.build();
    }

    @Bean
    public UserDetailsService userDetailsService() {
        UserDetails user =
             User.withDefaultPasswordEncoder()
                .username("user")
                .password("password")
                .roles("USER")
                .build();

        return new InMemoryUserDetailsManager(user);
    }
}
```

## Thử Nghiệm Ứng Dụng

Để chạy ứng dụng Spring Boot:

```bash
./mvnw spring-boot:run
```

hoặc

```bash
./gradlew bootRun
```

## Kết Luận

Spring Boot là một framework mạnh mẽ cho phát triển ứng dụng Java, giúp đơn giản hóa quá trình cấu hình và triển khai. Với các tính năng như cấu hình tự động, máy chủ nhúng, và starter dependencies, Spring Boot giúp các nhà phát triển tập trung vào logic kinh doanh thay vì lo lắng về cấu hình.

Trong các bài viết tiếp theo, chúng ta sẽ đi sâu hơn vào các tính năng nâng cao của Spring Boot như microservices, Spring Cloud, và Spring Data.
