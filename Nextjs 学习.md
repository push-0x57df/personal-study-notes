# Nextjs 学习

## 什么是 Next？能做什么？

Next 是一个应用在生产环境中的 react 框架，内置支持服务端渲染（SSR），静态页面生成（SSG），自带路由等

## 路由、页面间导航

### 静态路由

Next 静态路由把 /page 目录解析成根目录，将 URL 的域名后续部分按照文件系统的规则直接路由

例：

```
/page/index.js => /
/page/abc.js => /abc
```

### 动态路由

动态路由可以接收动态的路由参数

例如，将js文件名称设置为 [id].js

内容为：

```js
import Link from 'next/link'
import Head from 'next/head'
import Container from '../../components/container'
import { getAllPostIds, getPostData } from '../../lib/posts'
export default function Post({ postData }) {
return (
<container>
{postData.id}
<br>
{postData.title}
<br>
{postData.date}
</container>
)
}
export async function getStaticPaths() {
const paths = getAllPostIds()
return {
paths,
fallback: false
}
}
export async function getStaticProps({ params }) {
const postData = getPostData(params.id)
return {
props: {
postData
}
}
}
```

文件 post,js

``` js
export function getPostData(id) {
const postOne = {
title: 'One',
id: 1,
date: '7/12/2020'
}
const postTwo = {
title: 'Two',
id: 2,
date: '7/12/2020'
}
if(id == 'one'){
return postOne;
}else if(id == 'two'){
return postTwo;
}
}
export function getAllPostIds() {
return [{
params: {
id: 'one'
}
},
{
params: {
id: 'two'
}
}
];
}
```

启动后：

访问 localhost:3000/posts/one

![image-20220223113016574](Nextjs 学习.assets/image-20220223113016574.png)

访问 localhost:3000/posts/two

![image-20220223113100370](Nextjs 学习.assets/image-20220223113100370.png)

