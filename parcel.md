一：parcelJS是什么
	官网给出的解释是：极速零配置Web应用打包工具。官网上给出的数据打包速度大概是webpack的十倍
二：parcelJS的优点
	1 极速打包时间，快的飞起
		Parcel 使用 worker 进程去启用多核编译。同时有文件系统缓存，即使在重启构建后也能快速再编译。
	2 将你所有的资源打包
		Parcel 具备开箱即用的对 JS, CSS, HTML, 文件及更多的支持，而且不需要插件。
	3 自动转换
		如若有需要，Babel, PostCSS, 和PostHTML甚至 node_modules 包会被用于自动转换代码.
	4 零配置代码分拆
		使用动态 import() 语法, Parcel 将你的输出文件束(bundles)分拆，因此你只需要在初次加载时加载你所需要的代码。
	5 热模块替换
		Parcel 无需配置，在开发环境的时候会自动在浏览器内随着你的代码更改而去更新模块
	6 友好的错误日志
		当遇到错误时，Parcel 会输出 语法高亮的代码片段，帮助你定位问题。
三：快速开始
	1 首先通过yarn或者npm安装 Parcel:
		yarn global add parcel-bundler
		npm install -g parcel-bundler
	2 在你正在使用的项目目录下创建一个 package.json 文件:
		yarn init -y
		npm init -y
	3 Parcel 可以使用任何类型的文件作为入口，但是最好还是使用 HTML 或 JavaScript 文件。如果在 HTML 中使用相对路径引入主要的 JavaScript 文件，Parcel 也将会对它进行处理将其替换为相对于输出文件的 URL地址。接下来，创建一个 index.html 和 index.js 文件。
		index.html文件
			<html>
				<body>
				  <script src="./index.js"></script>
				</body>
			</html>
		index.js文件
			console.log('hello world');
	4 Parcel 内置了一个当你改变文件能够自动重建应用的开发服务器，而且为了实现快速开发该开发服务器支持热模块替换。只需要在入口文件指出：
		parcel index.html
	5 现在在浏览器中打开 http://localhost:1234/。你也可以使用 -p <port number> 选项覆盖默认的端口。 如果没有自己的服务器可使用开发服务器，或者你的应用程序完全由客户端呈现。如果有自己的服务器，你可以在watch 模式下运行 Parcel 。
	    当文件改变它仍然会自动重建并支持热替换，但是不会启动 web 服务。
		parcel watch index.html
