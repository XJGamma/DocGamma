# 客户端与服务端的通信接口说明

## 协议
```
https
```

## 注册、登录、注销

```
注册： /accounts/signup  POST方法  参数：name, password
登录： /accounts/login   POST方法  参数：name, password
注销： /accounts/logout  POST方法  参数：name, token
```
