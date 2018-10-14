# # 快手通信5.9版本协议签名

## 简介

通过快手通信协议实现自动化爬取快手视频，批量注册登录，点赞，评论，视频下载上传等功能

快手通信协议支持 iOS 5.9（最新）版本协议，最低兼容版本及Android支持请自测，之后会提供设备信息生成功能，方便调用协议

提供生成签名服务，方便对快手通信协议进行签名。签名参数: `sig`

项目持续更新中...

## 使用说明
通过调用API加签服务来完成获取新的设备信息及协议签名。

实现过程:
1. 通过访问 `https://api.appsign.vip:2688/token/kuaishou` 获取快手的最新版本加签token，token有效期为60分钟，token失效前请不要重复获取token
2. 自己生成设备信息。之后会开放设备信息生成接口
3. 有了设备信息和加签Token， 需要通过参数构造加签字符串，调用 `https://api.appsign.vip:2688/sign` 完成参数的加签

---

> token有效期为一个小时，支持多线程进行加签，token失效之前无需重复获取

## API参数
1. 获取快手加签Token
```
https://api.appsign.vip:2688/token/kuaishou  # 默认版本为最新
https://api.appsign.vip:2688/token/kuaishou/version/5.9
```
```
{
    "token":"5826aa5b56614ea798ca42d767170e74",
    "success":true
}
```

2. 参数加签
```
https://api.appsign.vip:2688/sign
{
    "token":"TOKEN",
    "query":"通过参数生成的加签字符串"
}
```
```
{
    "data":{
        "sign":"0041******cf******",
    },
    "success":true
}
```

> 提醒： 如果是post请求，post请求参数和get请求参数使用'&'符号链接成统一参数，传递到`query`参数
> 签名接口统一返回参数名为`sign`，但是发送给快手服务器的参数为`sig`

## APP版本信息
...

## 实例
* [x] 爬取首页视频: `feed.py`
* [ ] 视频搜索:
* [ ] 注册 
* [ ] 登录
* [ ] 点赞
* [ ] 评论
* [ ] 视频下载 无水印 
* [ ] 视频上传

## 更新
* 2018.09.28 更新支持最新版5.9协议，最低支持版本请自测
