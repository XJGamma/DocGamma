# 可能用到的数据结构

```
MetaBookInfo: <- S
    <!-- standard book information -->
    id
    name
    images
    isbn
    pages
```

```
Book: <- C
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
Remind: <- C <!-- 读书开始提醒 -->
    book_id => Book
    remind_time

Timer: <- C <!-- 延时 -->

FinishTimer: <- C <!-- 读书结束提醒 -->
```

```
User: <- S
    id
    name
    password
    salt
    avatar
    cookie

User: <- C
    name
    avatar
    cookie

BookComment:
    id
    book_id => Book
    content
    created_time
```
