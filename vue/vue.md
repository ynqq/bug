### vue+vite打包配置
1. 部署二级文件夹目录下面
    1. 修改 <font color="#00baff">vite.config.j\[t]s</font> 里面的 <font color="#00baff">base</font> 属性 改为 <font color="#00baff">/xxx/</font>
        * 可以使用 <font color="#00baff">loadEnv</font> 方法获取环境变量的配置
            ```js
            const envConfig = loadEnv(mode, './')
            ```
    2. 修改路由配置文件里面的 <font color="#00baff">createWebHistory</font> 方法
        ```js
            createWebHistory('/vite/'/** 二级文件加名称 **/)
        ```
2. 使用history模式刷新之后404
    * node+express
        1. 下载安装 <font color="#00baff">connect-history-api-fallback</font>
        2. 在入口js里面引用并使用
            ```js
            const history = require('connect-history-api-fallback')
            // 要在 static 之前引用
            app.use(history({
                index: './vite/index.html' // 默认是index.html 如果文件名不是index可以自己配置 路径相对于 static
            }))
            app.use(express.static(path.resolve(__dirname, './view')))
            ```