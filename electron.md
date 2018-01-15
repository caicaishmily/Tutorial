一：electron简介
	Electron最初是叫Atom Shell,是GitHub开发的一个开源框架。它允许使用Node.js（作为后端）和Chromium（作为前端）完成桌面GUI应用程序的开发。
	Electron现已被多个开源Web应用程序用于前端与后端的开发，其中著名项目包括GitHub的Atom和微软的Visual Studio Code。
	该框架由Electron可执行文件（Windows中为electron.exe、macOS中为electron.app、Linux中为electron）提供。
	开发者可以自行添加标志、自定义图标、重命名或编辑Electron可执行文件。
二：主进程&渲染进程
	主进程：
		在 Electron 里，运行 package.json 里 main 脚本的进程被称为主进程。在主进程运行的脚本可以以创建 web 页面的形式展示 GUI。
	渲染进程：
		由于 Electron 使用 Chromium 来展示页面，所以 Chromium 的多进程结构也被充分利用。每个 Electron 的页面都在运行着自己的进程，这样的进程我们称之为渲染进程。
	在一般浏览器中，网页通常会在沙盒环境下运行，并且不允许访问原生资源。然而，Electron 用户拥有在网页中调用 io.js 的 APIs 的能力，可以与底层操作系统直接交互。
	两者之间的区别：
		主进程使用 BroswerWindow 实例创建网页。每个 BroswerWindow 实例都在自己的渲染进程里运行着一个网页。当一个 BroswerWindow 实例被销毁后，相应的渲染进程也会被终止。
		主进程管理所有页面和与之对应的渲染进程。每个渲染进程都是相互独立的，并且只关心他们自己的网页。
		由于在网页里管理原生 GUI 资源是非常危险而且容易造成资源泄露，所以在网页面调用 GUI 相关的 APIs 是不被允许的。如果你想在网页里使用 GUI 操作，其对应的渲染进程必须与主进程进行通讯，请求主进程进行相关的 GUI 操作。
	在 Electron，我们提供用于在主进程与渲染进程之间通讯的 ipc 模块。并且也有一个远程进程调用风格的通讯模块 remote。
三：开始你的第一个electron
	2.1 一个基础的Electron包含三个文件：
		package.json（元数据）,
		main.js（代码）
		index.html（图形用户界面）
	2.2 让我们来制作第一个electron应用吧;
		这是electron在GitHub上的地址 https://github.com/electron，里面有相关的很多库。其中就包括一个demo演示，还有quickstart库以及electron
		我们先来克隆一下那个demo，看看效果，地址是https://github.com/electron/electron-api-demos.git
		由于该框架依赖于nodejs，所以你的电脑必须先安装node，在这里我就不多说了。
		克隆好之后进入对应的目录下面，然后安装安装依赖包 npm install，(国内推荐使用淘宝镜像，那样会快一点)
		安装好之后，直接运行npm start就会启动一个应用程序
	2.3 quickstart按照上面的方式依次执行就可以了
