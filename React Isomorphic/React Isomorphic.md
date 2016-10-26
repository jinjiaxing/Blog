# React Isomorphic

所谓React同构：即可以在服务端通过nodejs渲染，又可以在服务端渲染，之后将控制权交给客户端  
		
		技术栈：react+redux+react-router+ compass+express+webpack

## Why？

* 为什么需要同构？

		1. 性能优化
		2. 用户体验
		3. 前端扩大技术栈，能够应用node

* 为什么需要引入nodejs呢？

		1. 数据模拟成本高，如需要mock数据
		2. api请求强依赖后端，之前联调需要等待后端接口完成，现在可同步进行，且可自由组合接口
		3. 适合前端技术落地，比如websocket等，技术栈更加广泛
		4. 高性能(不逊色与HHVM)，高并发异步请求
		5. React可以切前后端渲染，提升首页加载速度
		6. 提升SEO效果
		7. 可以尝试BigPipe技术，提升页面显示速度

## HOW？
### 页面渲染

1：React中的ReactDOM，在客户端通过 `ReactDOM.render()`方法构建页面    

2：在服务端则通过 `ReactDOMServer.renderToString()`方法构建，当然也可以通过`renderToStaticMarkup`方法，但我们这里就先不介绍了  
  
3：在服务端渲染的页面，会为组件添加 `checksum` ，而页面渲染完成之后，客户端在拿到直出的HTML页面之后（**需要注意的是，此时只是html渲染完成，但事件绑定并未完成**)，之后客户端会对这个字段进行对比
如果相同，则客户端不会在重新进行页面render，这样大大节省了响应时间，达到页面秒出
4：如果服务端使用的是`renderToStaticMarkup`方法渲染，则不会有这个`checksum`，纯服务端渲染的页面推荐用这种方法  

### 数据获取时机

1：一种是整体页面在服务端渲染之后，在客户端的`componentDidMount `生命周期函数去通过ajax调用，这样做法的优势就是服务端写起来简单，只是渲染页面即可  

2：另外一种是在是在服务端直接拉取好数据，存入redux的store中，之后一同发给客户端，这样做法的优势是节省了首页加载时间，但同时加大了一定的开发成本  

未完待续。。。

	



