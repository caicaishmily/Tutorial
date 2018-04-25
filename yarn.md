一 Yarn介绍
    Yarn 是一个依赖管理工具。它能够管理你的代码，并与全世界的开发者分享代码。Yarn 是高效、安全和可靠的，你完全可以安心使用。

    Yarn 能够让你使用其他开发者开发的代码，让你更容易的开发软件。如果你在使用中发现任何问题，欢迎发 issue或者贡献代码，一旦问题被修复，你就可以继续使用 Yarn 战斗了。


    代码是通过包（有时也被称为模块）进行共享的。 在每一个包中包含了所有需要共享的代码，另外还定义了一个 package.json 文件，用来描述这个包。
二 Yarn常用命令
    初始化一个新的项目
        yarn init
    添加一个依赖包
        yarn add [package]
        yarn add [package]@[version]
        yarn add [package]@[tag]
    更新一个依赖包
        yarn upgrade [package]
        yarn upgrade [package]@[version]
        yarn upgrade [package]@[tag]
    删除一个依赖包
        yarn remove [package]
    安装所有的依赖包
        yarn
        yarn install