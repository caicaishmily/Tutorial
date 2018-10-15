## Ecto 入门

### Ecto 是什么
  Ecto是Elixir的数据库包装器和查询生成器。 它提供了一个标准化的API和一组用于与所有不同类型的数据库交谈的抽象，因此Elixir开发人员可以通过使用类似的结构查询他们正在使用的任何数据库。
  
### 本次分享的重点
 一些关于Ecto的基础知识，例如创建，读取，更新和销毁PostgreSQL数据库中的记录。
    
### 前置知识
  - Elixir
  - Phoenix
  - PostgreSQL

### Ecto主要划分为四个部分：

  * Ecto.Repo   
    Repo是数据存储的包装器。 通过Repo，我们可以创建，更新，销毁和查询现有条目。 Repo需要适配器和认证才能与数据库通信
  * Ecto.Schema  
    模式用于将任何数据源映射到Elixir结构中。 我们经常使用它们将表映射到Elixir数据，但这是它们的一个用例，而不是使用Ecto的要求
  * Ecto.Changeset  
    变更集为开发人员提供了一种过滤和转换外部参数的方法，以及在将更改应用于数据之前跟踪和验证更改的机制
  * Ecto.Query  
    用Elixir语法编写的查询用于从给定的存储库中检索信息。 Ecto中的查询是安全的，避免了SQL注入等常见问题，同时仍然是可组合的，允许开发人员逐个构建查询而不是一次性构建查询
    
### 创建phoenix项目

  ```mix phx.new my_app ```
  
  We are all set! Go into your application by running:

   ``` cd my_app```

  Then configure your database in config/dev.exs and run:

   ```mix ecto.create```

  Start your Phoenix app with:

   ```mix phx.server```

  You can also run your app inside IEx (Interactive Elixir) as:

   ```iex -S mix phx.server```
