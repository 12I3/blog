---
title: axios拦截器
# date: 2020-06-27 15:27:12
tags:
cover: https://s1.ax1x.com/2020/06/27/NcZaqS.png
copyright: false

---

## 请求拦截器
```javascript
    let inc = axios.interceptors.request.use(
        config=>{
            //发送请求之前做些什么
            return config
        },
        err=>{
            //请求错误时做些什么
            return Promise.reject(err)
        })
```
<br/>

## 响应拦截器
```javascript
    let inc = axios.interceptors.response.use(
        response=>{
            //请求成功之后做些什么
            return response
        },
        err=>{
            //请求失败做些什么
            return Promise.reject(err)
        })
```
<br/>

## 取消拦截器的方法
```javascript
   axios.interceptors.request.eject(inc)
```
<br/>