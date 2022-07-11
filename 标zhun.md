组件：jeeXxxYyy

js:

使用箭头函数 ，参数为一个时不使用括号，尽量使用async/await处理嵌套的异步函数，散装数据使用vdata，不会变动的对象不要使用ref包装，存在返回值的函数使用 `@params`注释 ,函数命名动词+名词，推荐foreach，for of代替for循环

```js

//箭头函数接受值
//good
const getList = e =>{
    console.log(e)
}
//bad
const getList =(e) =>{
    console.log(e)
}
function getList(e){
    conssole.log(e)
}

//函数参数注释
//good
/*
    @params {String} a
    @params {Number} b
    @return {Number} c
*/
const addNumber = (a,b) =>{
    return a+b
}
//bad
//处理两数之和
const addNumber = (a,b) =>{
    return a+b
}
//async await使用
//good
const getLocation = () =>{
    return new Promise((resolve,reject) =>{
        uni.showLoading()
        uni.request({
            url: 'https://restapi.amap.com/v3/geocode/geo', // 调用高德接口
            data: {
                key: '1234',
                address: this.detailArea
            },
            success:  res => {
                console.log(123)
                resolve(res)
            },
            fail:err => {console.log(err) reject(err)}
        });
    })
}
const useLocal = (res) =>{
    console.log(res)
}

async const displayData =() =>{
   let res =  await getLocation()
    await useLocal(res)
}
//bad
const getLocation = () =>{ 
        uni.showLoading()
        uni.request({
            url: 'https://restapi.amap.com/v3/geocode/geo', // 调用高德接口
            data: {
                key: '123456',
                address: this.detailArea
            },
            success:  res => {
                console.log(123)
                useLocal(res)
            },
            fail:err => {console.log(err) }
        });

}
const useLocal = (res) =>{
    console.log(res)
}
//遍历数组
//good 
const list = [1,2,3,4]
list.forEach(item =>{
    console.log(item)
})
//not good
for(let i=0;i>=list.length;i++){
    console.log(list[i])
}

//对象取值
const obj ={
    a:1,b:2,c:3
}

//bad
const a = obj.a
const b = obj.b
//good 
const {a,b,c} = obj || {}
const {a:a1} = obj

//合并数据
const a = [1,2,3,4]
const b= [3,4,5,6]
const obj1 = {
    a:1
}
const obj2 = {
    b:1
}
//bad
const c = a.concat(b)
const obj = Object.assign({},obj1,obj2)
//good 
const c = [...new Set([...a,...b])]
const obj = {...obj1,...obj2}

```



sass

嵌套最多不超过3层，长命名使用`-`链接，可以使用 `@extent` 复用样式， 行内样式不要写`flex`相关 ，字体、颜色等可以在一个样式文件中统一定义 

