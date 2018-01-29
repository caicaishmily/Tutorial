一：ejs简单介绍
	EJS是客户端模板语言，最初是JavaScriptMVC的一部分，现在已经被DoneJS取代。这是ejs官网上对他的介绍。
二：ejs基本使用	
	EJS结合数据和模板来生成HTML。 比如现在我们要生成有一个标题和一个用品清单的页面。
	1 传统方式：
		<h1>水果</h1>
	    <ul>
	      <li>香蕉</li>
	      <li>苹果</li>
	      <li>西瓜</li>
	    </ul>
	2 使用ejs模板：
		假设服务器给你传过来的数据如下：
	      data：{	title:	'水果'
	          supplies:	['香蕉', '苹果', '西瓜']
	      }
		
		2.1 JavaScript拼字符串方式：
		
	      var html = "<h1>"+data.title+"</h1>";
	      html += "<ul>"
	      for(var i=0; i<data.supplies.length; i++) {
	      	html += "<li><a href='supplies/"+data.supplies[i]+"'>";
	      	html += data.supplies[i]+"</a></li>";
	      }
	      html += "</ul>";
		
		2.2 ejs template:
		
	      <h1><%= title %></h1>
	      <ul>
	        <% for(var i=0; i<supplies.length; i++) {%>
	        	<li><a><%= supplies[i] %></a></li>
	        <% } %>
	      </ul>
		正如上面所说的,ejs结合数据和模板来生成HTML。相较之下，ejs更加友好，明确且维护性良好
		2.3 ejs的优点
			没有混乱的HTML字符串连接。
			可以很轻松地从单独的文件加载模板。
			类似Rails的视图助手。
			模板缓存。
			智能错误处理。
			支持FF 1.5+，IE 6+，Opera 9，Safari 3。
			MIT许可证
三：ejs的语法：
	1 <% code %>用于执行其中javascript代码。
		example：<% alert('hello world') %>	
	2 <%= code %>会对code进行html转义;
		<h1><%=title %></h1>   注：会把title里面存的值给显示出来在h1中。
	3 <%- code %>将不会进行转义;这一行代码不会执行，像是被注释了一样，然后显示原来的html。也不会影响整个页面的执行。
		<h1><%-title %>asd</h1>  注：最后显示asd，及显示原网页
	4  支持自定义标签，比如'<%'可以使用'{{'，'%>'用'}}'代替；
		ejs 里，默认的闭合标记是 <% .. %>，我们也可以定义自己的标签。例如：
		app.set("view options",{ "open":"{{", "close":"}}"});
	5 提供一些辅助函数，用于模版中使用
		1)、first，返回数组的第一个元素；
		2)、last，返回数组的最后一个元素；
		3)、capitalize，返回首字母大写的字符串；
		4)、downcase，返回字符串的小写；
		5)、upcase，返回字符串的大写；
		6)、sort，排序（Object.create(obj).sort()？）；
		7)、sort_by:'prop'，按照指定的prop属性进行升序排序；
		8)、size，返回长度，即length属性，不一定非是数组才行；
		9)、plus:n，加上n，将转化为Number进行运算；
		10)、minus:n，减去n，将转化为Number进行运算；
		11)、times:n，乘以n，将转化为Number进行运算；
		12)、divided_by:n，除以n，将转化为Number进行运算；
		13)、join:'val'，将数组用'val'最为分隔符，进行合并成一个字符串；
		14)、truncate:n，截取前n个字符，超过长度时，将返回一个副本
		15)、truncate_words:n，取得字符串中的前n个word，word以空格进行分割；
		16)、replace:pattern,substitution，字符串替换，substitution不提供将删除匹配的子串；
		17)、prepend:val，如果操作数为数组，则进行合并；为字符串则添加val在前面；
		18)、append:val，如果操作数为数组，则进行合并；为字符串则添加val在后面；
		19)、map:'prop'，返回对象数组中属性为prop的值组成的数组；
		20)、reverse，翻转数组或字符串；
		21)、get:'prop'，取得属性为'prop'的值；
		22)、json，转化为json格式字符串
	6 <%- include filename %>加载其他页面模版；
四：ejs的使用
	加载一个模板文件，然后用数据渲染它
		html = new EJS({url: '/template.ejs'}).render(data)
	用来自JSON请求的数据呈现的模板的结果更新元素'todo'
		new EJS({url:'/todo.ejs'}).update('todo','/todo.json')
	
	基于我们之前写的模版生成一个EJS对象
		new EJS({url: 'path'})
		对象有下面两个成员函数
		1、ejs.compile(str, options); 将返回内部解析好的Function函数
		2、ejs.render(str, options); 返回经过解析的字符串
		ejs的render函数有两个参数 第一个是字符串，第二个是可选的对象，和其他javascript模版一样需要渲染的数据也是包含在option对象中的。
		ejs.render(str,option);  
		 // 渲染字符串 str 一般是通过nodejs文件系统的readfile方法读取 
		ejs.render(str,{  
		 	data : user_data  
		 // 需要渲染的数据 });
		其中options的一些参数为：
		1、cache：是否缓存解析后的模版，需要filename作为key；
		2、filename：模版文件名；
		3、scope：complile后的Function执行所在的上下文环境；
		4、debug：标识是否是debeg状态，debug为true则会输出生成的Function内容；
		5、compileDebug：标识是否是编译debug，为true则会生成解析过程中的跟踪信息，用于调试；
		6、client，标识是否用于浏览器客户端运行，为true则返回解析后的可以单独运行的Function函数；
		7、open，代码开头标记，默认为'<%'；
		8、close，代码结束标记，默认为'%>'；
		9、其他的一些用于解析模版时提供的变量。 在express中使用时，options参数将由response.render进行传入，其中包含了一些express中的设置，以及用户提供的变量值。
五：应用场景
	在基于WebService的AJAX网站开发中,EJS可以接收WebService异步传送过来的JSON格式的数据，将这种数据直接传入你的模板里，然后将结果插入到你的页面中。你所需要做的只是通过以下代码：
	new EJS({url:'comments.ejs'}).update('element_id', '/comments.json')
