# 可能用到的数据结构

## 客户端

```
User:
    name
    avatar # 存放头像的路径 或者此项不是必须的，由于本地只存在一个用户
    token # 用于保持或者验证用户的登录状态
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
    updated_at
    created_at
```

```
BookComment: # 书评 !! 同步项
    id
    book_id => Book
    content
    updated_at
    created_at
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
Book: # 标准书籍的数据结构，用于存放服务器已知书籍信息 不知是否还有用
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
    password_hash
    password_salt
    avatar
    token
    token_created_at
    token_expired_at
```

```
Data: # 数据同步表
    id
    user_id => User
    content
    created_at
    updated_at
```

```
服务端配置:
    token_life_time
```
