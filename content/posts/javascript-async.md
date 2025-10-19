---
title: "JavaScript Bất Đồng Bộ - Promises, Async/Await"
date: 2023-10-26
draft: false
tags: ["JavaScript", "Async", "Promises", "Lập Trình"]
categories: ["JavaScript"]
cover:
    image: "/KhanhLanBlog/images/posts/javascript-async.svg"
    alt: "JavaScript Async"
    caption: "Promises, Async/Await"
---

# JavaScript Bất Đồng Bộ - Promises, Async/Await

![JavaScript Async](/KhanhLanBlog/images/posts/javascript-async.svg)

JavaScript là ngôn ngữ đơn luồng (single-threaded), nhưng có thể xử lý các tác vụ bất đồng bộ thông qua các cơ chế như callbacks, promises, và async/await.

## Tại Sao Cần Lập Trình Bất Đồng Bộ?

Lập trình bất đồng bộ cho phép thực hiện các tác vụ mà không chặn luồng chính, đặc biệt hữu ích cho:
- Gọi API
- Đọc/ghi tệp
- Truy vấn cơ sở dữ liệu
- Tải tài nguyên (hình ảnh, video)
- Thực hiện các tác vụ tốn thời gian

## Callbacks

Callbacks là cách truyền thống nhất để xử lý bất đồng bộ trong JavaScript.

```javascript
function taiDuLieu(url, callback) {
    console.log(`Bắt đầu tải dữ liệu từ ${url}`);
    
    setTimeout(() => {
        const duLieu = { id: 1, ten: "Dữ liệu từ " + url };
        callback(duLieu);
    }, 2000);
}

taiDuLieu("api.example.com/data", function(duLieu) {
    console.log("Dữ liệu đã tải xong:", duLieu);
});

console.log("Tiếp tục thực hiện các tác vụ khác...");
```

### Callback Hell

Khi có nhiều tác vụ bất đồng bộ lồng nhau, code có thể trở nên khó đọc và bảo trì, hiện tượng này được gọi là "callback hell" hoặc "pyramid of doom".

```javascript
taiDuLieu("api.example.com/users", function(users) {
    console.log("Đã tải danh sách người dùng");
    
    taiDuLieu(`api.example.com/users/${users[0].id}/posts`, function(posts) {
        console.log("Đã tải bài viết của người dùng");
        
        taiDuLieu(`api.example.com/posts/${posts[0].id}/comments`, function(comments) {
            console.log("Đã tải bình luận của bài viết");
            
            // Và còn nhiều lồng nhau nữa...
        });
    });
});
```

## Promises

Promises được giới thiệu để giải quyết vấn đề callback hell, cung cấp cách tốt hơn để xử lý các tác vụ bất đồng bộ.

```javascript
function taiDuLieu(url) {
    return new Promise((resolve, reject) => {
        console.log(`Bắt đầu tải dữ liệu từ ${url}`);
        
        setTimeout(() => {
            if (url.includes("error")) {
                reject(new Error("Không thể tải dữ liệu"));
            } else {
                const duLieu = { id: 1, ten: "Dữ liệu từ " + url };
                resolve(duLieu);
            }
        }, 2000);
    });
}

taiDuLieu("api.example.com/data")
    .then(duLieu => {
        console.log("Dữ liệu đã tải xong:", duLieu);
        return taiDuLieu("api.example.com/more-data");
    })
    .then(duLieuThem => {
        console.log("Dữ liệu thêm đã tải xong:", duLieuThem);
    })
    .catch(error => {
        console.error("Đã xảy ra lỗi:", error.message);
    })
    .finally(() => {
        console.log("Quá trình tải dữ liệu đã hoàn tất");
    });

console.log("Tiếp tục thực hiện các tác vụ khác...");
```

### Trạng Thái Của Promise

Một Promise có thể ở một trong ba trạng thái:
- **Pending**: Trạng thái ban đầu, chưa hoàn thành hoặc bị từ chối
- **Fulfilled**: Tác vụ đã hoàn thành thành công
- **Rejected**: Tác vụ đã thất bại

### Promise.all

`Promise.all` cho phép thực hiện nhiều promises đồng thời và đợi tất cả hoàn thành.

```javascript
const promise1 = taiDuLieu("api.example.com/users");
const promise2 = taiDuLieu("api.example.com/posts");
const promise3 = taiDuLieu("api.example.com/comments");

Promise.all([promise1, promise2, promise3])
    .then(ketQua => {
        const [users, posts, comments] = ketQua;
        console.log("Tất cả dữ liệu đã tải xong");
        console.log("Users:", users);
        console.log("Posts:", posts);
        console.log("Comments:", comments);
    })
    .catch(error => {
        console.error("Một trong các promises đã thất bại:", error.message);
    });
```

### Promise.race

`Promise.race` trả về promise đầu tiên hoàn thành (hoặc bị từ chối).

```javascript
const promise1 = taiDuLieu("api.example.com/data1"); // 2 giây
const promise2 = new Promise((resolve) => {
    setTimeout(() => resolve("Dữ liệu nhanh"), 1000); // 1 giây
});

Promise.race([promise1, promise2])
    .then(ketQua => {
        console.log("Kết quả đầu tiên:", ketQua); // "Dữ liệu nhanh"
    })
    .catch(error => {
        console.error("Lỗi:", error.message);
    });
```

## Async/Await

Async/await là cú pháp "đường mật" (syntactic sugar) cho promises, giúp code bất đồng bộ trông giống như code đồng bộ, dễ đọc và dễ hiểu hơn.

```javascript
async function taiDuLieuNguoiDung() {
    try {
        console.log("Bắt đầu tải dữ liệu người dùng");
        
        const users = await taiDuLieu("api.example.com/users");
        console.log("Danh sách người dùng:", users);
        
        const posts = await taiDuLieu(`api.example.com/users/${users.id}/posts`);
        console.log("Bài viết của người dùng:", posts);
        
        const comments = await taiDuLieu(`api.example.com/posts/${posts.id}/comments`);
        console.log("Bình luận của bài viết:", comments);
        
        return { users, posts, comments };
    } catch (error) {
        console.error("Đã xảy ra lỗi:", error.message);
        throw error;
    } finally {
        console.log("Quá trình tải dữ liệu đã hoàn tất");
    }
}

// Gọi hàm async
taiDuLieuNguoiDung()
    .then(duLieu => {
        console.log("Tất cả dữ liệu:", duLieu);
    })
    .catch(error => {
        console.error("Lỗi từ hàm async:", error.message);
    });

console.log("Tiếp tục thực hiện các tác vụ khác...");
```

### Thực Hiện Nhiều Tác Vụ Đồng Thời Với Async/Await

```javascript
async function taiNhieuDuLieu() {
    try {
        console.log("Bắt đầu tải nhiều dữ liệu đồng thời");
        
        // Thực hiện đồng thời
        const [users, posts, comments] = await Promise.all([
            taiDuLieu("api.example.com/users"),
            taiDuLieu("api.example.com/posts"),
            taiDuLieu("api.example.com/comments")
        ]);
        
        console.log("Tất cả dữ liệu đã tải xong");
        console.log("Users:", users);
        console.log("Posts:", posts);
        console.log("Comments:", comments);
        
        return { users, posts, comments };
    } catch (error) {
        console.error("Đã xảy ra lỗi:", error.message);
        throw error;
    }
}
```

## Ví Dụ Thực Tế: Gọi API

### Sử Dụng Fetch API Với Promises

```javascript
function layDuLieuAPI(url) {
    return fetch(url)
        .then(response => {
            if (!response.ok) {
                throw new Error(`HTTP error! Status: ${response.status}`);
            }
            return response.json();
        });
}

layDuLieuAPI('https://jsonplaceholder.typicode.com/users')
    .then(users => {
        console.log("Danh sách người dùng:", users);
        return layDuLieuAPI(`https://jsonplaceholder.typicode.com/users/${users[0].id}/posts`);
    })
    .then(posts => {
        console.log("Bài viết của người dùng:", posts);
    })
    .catch(error => {
        console.error("Lỗi khi gọi API:", error.message);
    });
```

### Sử Dụng Fetch API Với Async/Await

```javascript
async function layDuLieuAPI(url) {
    try {
        const response = await fetch(url);
        
        if (!response.ok) {
            throw new Error(`HTTP error! Status: ${response.status}`);
        }
        
        return await response.json();
    } catch (error) {
        console.error("Lỗi khi gọi API:", error.message);
        throw error;
    }
}

async function hienThiDuLieuNguoiDung() {
    try {
        const users = await layDuLieuAPI('https://jsonplaceholder.typicode.com/users');
        console.log("Danh sách người dùng:", users);
        
        const posts = await layDuLieuAPI(`https://jsonplaceholder.typicode.com/users/${users[0].id}/posts`);
        console.log("Bài viết của người dùng:", posts);
        
        return { users, posts };
    } catch (error) {
        console.error("Không thể hiển thị dữ liệu:", error.message);
    }
}

hienThiDuLieuNguoiDung();
```

## Kết Luận

Lập trình bất đồng bộ là một phần quan trọng của JavaScript, đặc biệt trong phát triển web hiện đại. Promises và async/await cung cấp các cách mạnh mẽ và dễ đọc để xử lý các tác vụ bất đồng bộ, giúp tránh callback hell và làm cho mã nguồn dễ bảo trì hơn.

Trong các bài viết tiếp theo, chúng ta sẽ tìm hiểu về các framework JavaScript hiện đại và cách chúng xử lý các tác vụ bất đồng bộ.