GraphQL
  GraphQL 是一种 API 查询语言, 用于服务器端执行按已定义类型系统的查询. GraphQL 不与任何特定的数据库或存储引擎进行绑定, 而是由您的代码和数据支持.
  通过定义类型和字段类型来创建 GraphQL 服务, 提供方法给每一个类型字段. 例如, 一个 GraphQL 服务, 告诉我们谁是登录用户(me), 用户信息可能是像这样显示:
  
    type Query {
      me: User
    }
    type User {
      id: ID
      name: String
    }
  为每个字段类型定义的函数:
  
    function Query_me(request) {
      return request.auth.user;
    }
    function User_name(user) {
      return user.getName();
    }
  一旦 GraphQL 服务启动(通常是基于Web URL服务), 可以通过 GraphQL 查询语句来验证和执行. 接收到的查询语句首先被确认是否仅引用定义的类型字段, 然后运行提供的函数以生成结果.
  示例查询请求:
  
    {
      me {
        name
      }
    }
  可能处理得到的 JSON:
  
    {
      "me": {
        "name": "Luke Skywalker"
      }
    }
