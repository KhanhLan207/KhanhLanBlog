---
title: "Java Collections Framework - Cấu Trúc Dữ Liệu Trong Java"
date: 2023-10-28
draft: false
tags: ["Java", "Collections", "Data Structures"]
categories: ["Java"]
cover:
    image: "/images/posts/java-collections.svg"
    alt: "Java Collections Framework"
    caption: "Cấu trúc dữ liệu trong Java"
---

# Java Collections Framework - Cấu Trúc Dữ Liệu Trong Java

![Java Collections](/images/posts/java-collections.svg)

Java Collections Framework cung cấp một kiến trúc để lưu trữ và thao tác với các nhóm đối tượng. Framework này bao gồm các interfaces, implementations và algorithms.

## Tổng Quan Về Collections Framework

Collections Framework trong Java bao gồm:
- **Interfaces**: Các abstract data types đại diện cho collections
- **Implementations**: Các lớp cụ thể triển khai các interfaces
- **Algorithms**: Các phương thức thực hiện các thao tác hữu ích như tìm kiếm và sắp xếp

## Các Interface Chính

### Collection Interface

Interface cơ bản nhất trong hierarchy, định nghĩa các thao tác cơ bản như add, remove, contains.

```java
Collection<String> collection = new ArrayList<>();
collection.add("Java");
collection.add("Python");
collection.add("C++");
System.out.println("Số phần tử: " + collection.size());
```

### List Interface

List là một collection có thứ tự và cho phép các phần tử trùng lặp.

```java
List<String> list = new ArrayList<>();
list.add("Java");
list.add("Python");
list.add("Java"); // Cho phép trùng lặp
System.out.println("Phần tử ở vị trí 1: " + list.get(1));
```

### Set Interface

Set là một collection không cho phép các phần tử trùng lặp.

```java
Set<String> set = new HashSet<>();
set.add("Java");
set.add("Python");
set.add("Java"); // Không được thêm vào vì đã tồn tại
System.out.println("Số phần tử trong set: " + set.size()); // Kết quả: 2
```

### Map Interface

Map là một đối tượng ánh xạ mỗi key tới một giá trị.

```java
Map<String, Integer> map = new HashMap<>();
map.put("Java", 1995);
map.put("Python", 1991);
map.put("JavaScript", 1995);
System.out.println("Năm ra đời của Java: " + map.get("Java"));
```

## Các Lớp Triển Khai Phổ Biến

### ArrayList

ArrayList là một mảng động, cho phép thêm hoặc xóa phần tử sau khi mảng được tạo.

```java
ArrayList<String> arrayList = new ArrayList<>();
arrayList.add("Java");
arrayList.add("Python");
arrayList.add("C++");

// Duyệt qua các phần tử
for (String language : arrayList) {
    System.out.println(language);
}
```

### LinkedList

LinkedList triển khai List và Deque interfaces, cho phép thao tác hiệu quả ở đầu và cuối danh sách.

```java
LinkedList<String> linkedList = new LinkedList<>();
linkedList.add("Java");
linkedList.add("Python");
linkedList.addFirst("C++"); // Thêm vào đầu
linkedList.addLast("JavaScript"); // Thêm vào cuối

System.out.println("Phần tử đầu tiên: " + linkedList.getFirst());
System.out.println("Phần tử cuối cùng: " + linkedList.getLast());
```

### HashSet

HashSet là một Set không đảm bảo thứ tự các phần tử.

```java
HashSet<String> hashSet = new HashSet<>();
hashSet.add("Java");
hashSet.add("Python");
hashSet.add("C++");

// Kiểm tra phần tử tồn tại
System.out.println("Có chứa Java không? " + hashSet.contains("Java"));
```

### TreeSet

TreeSet là một Set sắp xếp các phần tử theo thứ tự tăng dần.

```java
TreeSet<String> treeSet = new TreeSet<>();
treeSet.add("Java");
treeSet.add("Python");
treeSet.add("C++");
treeSet.add("JavaScript");

// Các phần tử được sắp xếp theo thứ tự
for (String language : treeSet) {
    System.out.println(language);
}
```

### HashMap

HashMap lưu trữ các cặp key-value, không đảm bảo thứ tự.

```java
HashMap<String, Integer> hashMap = new HashMap<>();
hashMap.put("Java", 1995);
hashMap.put("Python", 1991);
hashMap.put("JavaScript", 1995);

// Duyệt qua các cặp key-value
for (Map.Entry<String, Integer> entry : hashMap.entrySet()) {
    System.out.println(entry.getKey() + " ra đời năm " + entry.getValue());
}
```

### TreeMap

TreeMap lưu trữ các cặp key-value, sắp xếp theo thứ tự tăng dần của key.

```java
TreeMap<String, Integer> treeMap = new TreeMap<>();
treeMap.put("Java", 1995);
treeMap.put("Python", 1991);
treeMap.put("JavaScript", 1995);
treeMap.put("C++", 1983);

// Các key được sắp xếp theo thứ tự
for (String key : treeMap.keySet()) {
    System.out.println(key + " ra đời năm " + treeMap.get(key));
}
```

## Các Thuật Toán Hữu Ích

Java Collections Framework cung cấp các thuật toán hữu ích thông qua lớp Collections:

```java
List<String> list = new ArrayList<>();
list.add("Java");
list.add("Python");
list.add("C++");
list.add("JavaScript");

// Sắp xếp
Collections.sort(list);
System.out.println("Danh sách sau khi sắp xếp: " + list);

// Đảo ngược
Collections.reverse(list);
System.out.println("Danh sách sau khi đảo ngược: " + list);

// Tìm kiếm nhị phân (yêu cầu danh sách đã sắp xếp)
Collections.sort(list);
int index = Collections.binarySearch(list, "Python");
System.out.println("Python ở vị trí: " + index);

// Xáo trộn
Collections.shuffle(list);
System.out.println("Danh sách sau khi xáo trộn: " + list);
```

## Kết Luận

Java Collections Framework là một công cụ mạnh mẽ để quản lý và thao tác với dữ liệu trong Java. Việc hiểu và sử dụng đúng các collection sẽ giúp bạn viết mã hiệu quả và tối ưu hơn.

Trong các bài viết tiếp theo, chúng ta sẽ đi sâu hơn vào các khía cạnh nâng cao của Collections Framework như concurrent collections và các kỹ thuật tối ưu hiệu suất.