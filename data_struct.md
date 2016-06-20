# 可能用到的数据结构

```
MetaBookInfo: <- S
    <!-- 标准书籍的数据结构，用于存放服务器已知书籍信息 -->
    id
    name
    images
    isbn
    pages
```

```
Book: <- C
    <!-- 客户端书籍的数据结构 -->
    id
    name
    image
    isbn
    pages
    current_page
    finish_time
    total_reading_time
```

```
Remind: <- C
    <!-- 读书开始提醒 -->
    book_id => Book
    remind_time
```

```
Timer: <- C
    <!-- 延时 -->
```

```
FinishTimer: <- C
    <!-- 读书结束提醒 -->
```

```
User: <- S
    id
    name
    password
    salt
    avatar
    cookie
```

```
User: <- C
    name
    avatar
    cookie
```

```
BookComment: <- C
    id
    book_id => Book
    content
    created_time
```
