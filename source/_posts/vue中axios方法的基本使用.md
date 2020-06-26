---
title: vue中axios方法的基本使用
date: 2020-06-17 15:27:12
tags:
cover: https://wx1.sbimg.cn/2020/06/23/1.png
copyright: false

---
## get,post,put,patch,delete

**get:** 获取数据
**post:** 提交数据
**put:** 更新数据
**patch:** 更新数据
**delete:** 删除数据

### put和patch的区别
put会把所有的数据都推送到服务端，而patch只将修改的数据推送到服务端
<br/>

## vue项目中引入axios
### 一、安装axios
```nodejs
$ npm install axios --save
```
<br/>

### 二、引入axios
在需要的vue文件中引入axios
```javascript
import axios from 'axios'
```
<br/>

## 使用axios
### 发送一个GET请求
axios封装了get方法，传入请求地址和请求参数，参数需要写在params属性下。
```javascript
    let url = '...'

    axios.get(url, {
      params:{
        id:12
      }
    }).then((res)=>{
      console.log(res) //返回的数据
    })
    .catch((err) => {  
      console.log(err) //错误信息
    })
```
<br/>

### 发送一个POST请求
post常用的data格式有两种：一种是form-data(表单提交，一般用于图片上传和文件上传),另一种是applicition/json。
```javascript
//applicition/json

    let url = '...'
    let data = {
        id: 1
    }

    axios.post(url, data).then((res)=>{
        console.log(res)
    })
```
```javascript
//form-data

    let url = '...'

    let data = {
        id: 1
    }
    let fd = new FormData()
    for(let key in data){
        fd.append(key, data[key])
    }
    axios.post(url, fd).then((res)=>{
        console.log(res)
    })
```
<br/>

## 发送一个delete请求
delete有的时候需要将参数拼接到url上,而有的时候需要放在请求体里面
将参数写在params就是将参数拼接在url上，将参数写在data属性下就是将参数放在请求体里。
```javascript
   //将参数拼到url
    axios.delete('/delete',{
      params:{
        id: 1
      }
    }).then(res=>{
      console.log(res)
    })
```
```javascript
   //将参数放在请求体
    axios.delete('/delete',{
      data:{
        id: 1
      }
    }).then(res=>{
      console.log(res)
    })
```
<br/>

## 另外一种写法
```javascript
//get请求
    axios({
        method:'get',
        url:'...',
        params:{
          id: 1
        }
    }).then(res=>{
      console.log(res)
    })

//post请求
    let data = {
        id: 1
    }
    axios({
        method: 'post',
        url: '..',
        data: data
    }).then(res=>{
        console.log(res)
    })

//delete请求
    axios({
        method: 'delete',
        url: '/delete',
        params:{id:12},  //参数拼接在url
        data:{id:12}     //参数放在请求体
    }).then(res=>{
        console.log(res)
    })
```
<br/>

## 并发请求
```javascript
      axios.all(
          [
              axios.get('...1.json'),
              axios.get('...2.json')
          ]
      ).then(
          axios.spread((dataRes, cityRes)=>{
              console.log(dataRes,cityRes)
          })
      )
```
axios.all()是一个数组，数组里面的值是一个一个的axios请求。
axios.spread()的作用分割不同请求的返回值，然后对这些返回值进行处理。
axios.spread()的参数是一个回调函数，axios.all()中有几个axios请求，与之对应spread()的回调函数中就要写几个参数用来存放请求的返回值。
<br/>
<br/>
<br/>