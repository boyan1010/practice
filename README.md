# practice
一些小练习的项目集合，作用未知，先攒着吧
## npm_link
作用：练习npm link
main_project为主项目
test_module_1为测试模块，该文件下执行npm link
模块会被链接到全局，路径是`${prefix}/lib/node_moudles/<package>`；windows与mac有区别
prefix 获取命令npm config get prefix;  // /usr/local

在主项目引用挂载到全局的模块: npm link test_module_1 
打印内容：/Users/anitacao/Desktop/Projects/npm_link练习/main_project/node_modules/test_module_1 -> /usr/local/lib/node_modules/test_module_1 -> /Users/anitacao/Desktop/Projects/npm_link练习/test_module_1

测试完成后删除 
npm unlink test_module_1 在项目中删除包的引用
删除全局的软连接

【注意】：执行`npm link moduleName`，npm link添加项目名称，而不是bin下的命令名
一个实例：
失败：我们将moduleB设置为依赖模块，在moduleA中引入moduleB，流程如下
在moduleB项目下package.json中加入bin 
```json
"bin": {
    "module-b-test": "index.js"
  },
```
执行`npm link`，在/usr/local/bin下创建软连接指向`/usr/local/lib/node_modules/moduleB`软连接文件，最终指向该项目下的index.js文件
在moduleA项目中引入moduleB模块，执行`npm link module-b-test`，打印错误如下
看错误提示：是在npm上查找远程的npm包，未找到
```shell
os ~/Desktop/Projects/cli-practice/npm_link/moduleA $ npm link module-b-test
npm ERR! code E404
npm ERR! 404 Not Found - GET https://registry.npmjs.org/module-b-test - Not found
npm ERR! 404 
npm ERR! 404  'module-b-test@latest' is not in the npm registry.
npm ERR! 404 You should bug the author to publish it (or use the name yourself!)
npm ERR! 404 
npm ERR! 404 Note that you can also install from a
npm ERR! 404 tarball, folder, http url, or git url.

npm ERR! A complete log of this run can be found in:
npm ERR!     /Users/xxx/.npm/_logs/2021-08-20T10_28_05_137Z-debug.log

```

问题原因：执行`npm link moduleB`，npm link添加项目名称，而不是bin下的命令名

/usr/local/bin/module-b-test -> /usr/local/lib/node_modules/moduleB/index.js
/usr/local/lib/node_modules/moduleB -> /Users/xxx/Desktop/Projects/cli-practice/npm_link/moduleB