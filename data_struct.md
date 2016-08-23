# 可能用到的数据结构

## 客户端

```
User:
    name
    avatar # 存放头像的路径 或者此项不是必须的，由于本地只存在一个用户
    cookie # 用于保持或者验证用户的登录状态
```

```
Book: # 客户端书籍的数据结构 !! 同步项
    id
    name
    image
    isbn
    pages
    current_page
    finish_time
    total_reading_time
    modified_time
    created_time
```

```
BookComment: # 书评 !! 同步项
    id
    book_id => Book
    content
    modified_time
    created_time
```

```
Remind: # 读书开始提醒
    book_id => Book
    remind_time
```

```
Timer: # 计时器提醒阅读完成
```

```
FinishTimer: # 读书结束提醒
```

## 服务端

```
MetaBookInfo: # 标准书籍的数据结构，用于存放服务器已知书籍信息 不知是否还有用
    id
    name
    images
    isbn
    pages
```

```
User: # 服务端用户表
    id
    name
    password
    password_hash_method
    salt
    avatar
    cookie
    cookie_created_time
    cookie_expiration_time
```

```
Data: # 数据同步表
    id
    user_id => User
    content
    created_time
    modified_time
```

```
Profile:
    cookie_life_time
    salt_algorithm
```
