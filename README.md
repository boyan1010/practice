# practice
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