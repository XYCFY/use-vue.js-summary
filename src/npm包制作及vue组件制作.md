[TOC]

# npm 包制作

`1.node环境import/require('XX')的包名都是从node_modules内部查找而来`
`2.package.json及npm i XX 是从远程拉取代码到node_modules文件夹内`
`3.node环境引用import XX from 'XX'和引用相对路径文件都是正常引用`
`4.node使用commonjs规范，module.exports = XX , require('XX')暴露。`
`5.因此正常写好符合commonjs规范的代码，用package.json的main暴露，即可。`
`6.之后代码推送到远程仓库或者发布到npmjs`

#### 目录结构

- node_modules
- lib
  - index.js 组件对外接口
- package.json
- README.md

#### 入口文件 ./lib/index.js

<pre style="background-color:#282c34;color:#ddd">
  import Vue from 'vue'
  import XX from './XX'

  const fn = {
    globalComp() {
      const components = { XX }
      Object.keys(components).forEach(name => {
        Vue.component(name, components[name])
      })
    }
  }

  export { XX, fn }
  // import { XX, fn } from 'repo-name';
  module.exports = { XX, fn }  
  // const XX = require('repo-name'); 
  // XX.XX
  // XX.fn
</pre>

#### 引用入口 package.json - main

<pre style="background-color:#282c34;color:#ddd">
{
  "name": "repo-name",
  "version": "1.0.0",
  "description": "",
  "main": "./lib/index.js",
  ...
}
</pre>

1.源码引用，main 引用入口文件，上面写完直接就可以用，但使用环境需要跟开发环境一致，否则无法正确编译

vue cli 3 构建指定 vue 为 JS

- 写法例子
  vue-cli-service build --target lib --name myLib [entry]
  vue-cli-service build --target lib --name myLib ./lib/index.js

  2.构建指定 vue 为 JS，main 直接引用打包后的 JS。

### 地址写法

- 安装 master
  `git-protocols ://git@ git-host : git-user / repo-name.git`

  > git+ssh://git@github.com:git-user/repo-name.git --save-dev
  > git+ssh://git@e.coding.net:git-user/repo-name.git

- 安装 branch
  `git-protocols ://git@ git-host : git-user / repo-name.git#branch`

  > git+ssh://git@github.com:git-user/repo-name.git#branch --save-dev
  > git+ssh://git@e.coding.net:git-user/repo-name.git#branch

- 安装版本
  `git-protocols ://git@ git-host : git-user / repo-name.git#verison`
  > git+ssh://git@github.com:git-user/repo-name.git#verison --save-dev
  > git+ssh://git@e.coding.net:git-user/repo-name.git#verison

* 其他写法
  > npm install git+ssh://git@github.com:npm/cli.git#v1.0.27
  > npm install git+ssh://git@github.com:npm/cli#semver:^5.0
  > npm install git+https://isaacs@github.com/npm/cli.git
  > npm install git://github.com/npm/cli.git#v1.0.27
  > GIT_SSH_COMMAND='ssh -i ~/.ssh/custom_ident' npm install git+ssh://git@github.com:npm/cli.git

### 命令安装

yarn add XXXX
npm install XXXX --save-dev | -S

### package.json 安装

"dependencies": {
"repo-name": "git+ssh://git@github.com:git-user/repo-name.git"
}

npm i | yarn

### 使用方法

import { XX, fn } from 'repo-name';
const XX = require('repo-name');

### 参考资料

module.exports 与 exports，export 与 export default 之间的关系和区别 https://www.cnblogs.com/fayin/p/6831071.html
nodejs 中标准包的制作,上传,安装及卸载方法 https://www.cnblogs.com/xinjianheyi/p/6034027.html
Nodejs 发布自己的 npm 包并制作成命令行工具 https://blog.csdn.net/u011249920/article/details/54891882/
Vue cli 3 构建组件 https://cli.vuejs.org/zh/guide/build-targets.html#%E5%BA%94%E7%94%A8
npm 安装命令 https://docs.npmjs.com/cli/install
