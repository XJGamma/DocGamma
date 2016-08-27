# 客户端与服务端的通信接口说明

## 协议
> HTTPS

## 接口说明
> 参数形式按照具体HTTP方法实现
> 例如： GET方法 some/path?para1=val1&para2=val2

> 返回值采用JSON格式
> 格式统一为
> ```
> {
>     code: val,    # 返回码
                    # 0 成功
                    # 1 服务器出错
                    # 2 登录信息过期，需重新登录
                    # 3 用户账户异常
>     return: ret   # 返回数据，请求响应的结果
> }
> ```
> 一个完整的登录成功的返回结果如下
> ```
> {
>     code: 0,
>     return: {
>         code: 0,
>         msg: "登陆成功",
>         token: "token_for_example"
>     }
> }
> ```

### 接口范例
```
path: /api/example
method: GET
parameters:
    para1       # 参数1
        val1    # para1取值说明
        val2
    para2       # 参数2
        val3
    >
        pair_val1, pair_val2    # 成对参数说明
return:
    return1     # 返回1
        ret1    # return1取值说明
        ret2
    return2     # 返回2
        ret3
    >
        pair_ret1, pair_ret2    # 成对返回值说明
remark: 备注
```

### 注册
```
path: /accounts/signup
method: POST
parameters：
    name        # 用户名
    password    # 密码
return:
    code        # 状态码
    msg         # 说明信息
    token       # 注册成功后返回token，使其为登录状态
    >
        0, "注册成功", "token_for_example"
        1, "该用户名已注册", ""
```

### 登录
```
path: /accounts/login
method: POST
parameters：
    name        # 用户名
    password    # 密码
return:
    code        # 状态码
    msg         # 说明信息
    token       # 保持其登录状态
    >
        0, "登录成功", "token_for_example"
        1, "用户名或密码错误", ""     # 不用区分是哪种错误
```

### 注销
```
path: /accounts/logout
method: POST
parameters：
    name        # 用户名
    token       # 保存登录状态的token
retrun:
    code        # 状态码
    msg         # 说明信息
    >
        0, "注销成功"
remark: 客户端访问该API前应删除本地token，如遇网络错误，本地登录信息也应当被清除
```

### 更换密码
```
path: /accounts/password/change
method: POST
parameters:
    name
    token
    old_password
    new_password
return:
    code
    msg
    >
        0, "密码设置成功"
        1, "原密码错误"
```

### 更换头像
```
path: /accounts/avatar/change
method: POST
parameters:
    name
    token
    avatar
return:
    code
    msg
    >
        0, "头像更换成功"
        1, "遇到一些问题"
```

### 获取头像
```
path: /accounts/avatar
method: GET
parameters:
    name
return:
    code
    avatar
    >
        0, O(∩_∩)O~
        1,          # "头像获取失败"
```

### 数据同步检查
```
path: /data/check
method: POST
parameters:
    name
    token
    check_list
        [{created_at, updated_at}, {created_at, updated_at}, ...]   # 创建时间与修改时间的列表
return:
    pull_list       # 客户端落后于服务端的部分
        [created_at, created_at, ...]
    push_list       # 服务端落后于客户端的部分
        [created_at, created_at, ...]
remark: 当返回的两个列表都为空时，表明已经同步
```

### 数据上传
```
path: /data/push
method: POST
parameters:
    name
    token
    list        # 上传数据列表
        [{created_at, updated_at, content}, {...}, ...]
return:
    count
        3 # 成功上传3条数据
```

### 数据下载
```
path: /data/pull
method: GET
parameters:
    name
    token
    list        # 下载数据参数
        [created_at, created_at, ...]
return:
    list        # 下载数据
        [{created_at, updated_at, content}, {...}, ...]
```

### 数据同步
```
path: /data/sync
method: POST
parameters:
    name
    token
    check_list
        [{created_at, updated_at}, {created_at, updated_at}, ...]   # 创建时间与修改时间的列表
return:
    pull_list       # 客户端落后于服务端的部分
        [{created_at, updated_at, content}, {...}, ...]
    push_list       # 服务端落后于客户端的部分
        [created_at, created_at, ...]
remark: 与数据同步检查接口基本相同，但直接返回需要下载的部分，此步骤做完后需做一次数据上传操作
```
