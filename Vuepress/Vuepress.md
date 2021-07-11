# 一、预备下载安装

1. node

   > https://nodejs.org/zh-cn/  点下载安装即可

2. npm

   node自带的

3. git

   > https://git-scm.com/download/win 选择需要的版本下载即可

4. yarn

   > http://classic.yarnpkg.com/latest.msi  这是Windows版本的msi文件

   下载完之打开cmd 运行

   ```
   npm install --global yarn
   ```

下载完之后可以cmd 分别用

```
yarn --version
git --version
npm --version
node --version
```

查看版本

# 二、安装

1. 配置淘宝镜像

   ```
   npm config set registry https://registry.npm.taobao.org
   ```

2. 下载

   ```
   npm install -g vuepress
   ```

   > npm config set cache"D:\developTools\Node\node_cache"
   >
   > 设置全局模块存放路径
   >
   > npm config set prefix"D:\developTools\Node\node_global"
   >
   >  令npm install XXX -g安装以后模块就在D:\developTools\Node\node_global里
   >
   > 这是另一篇博客里的东西，不知道有用没用

3. 检查

   ```
   vuepress --version
   ```

   ```cli.js/1.8.2 win32-x64 node-v14.17.3``` 是我这里下载完后的版本号

## 可能遇到的问题

### 下载vuepress过程等待时间过长

解决方法：配置淘宝镜像```npm config set registry https://registry.npm.taobao.org```

然后输入```npm config get registry```

返回```https://registry.npm.taobao.org/```证明配置成功

然后下载即可

# 三、初步创建

1. 全局安装：```npm install -g vuepress``` 

   > 一般来说，这个过程中只要没出现红error就算是正常的好像warn没啥问题(我没遇见啥问题)

2.  创建个文件夹作为目录 ```$ mkdir Vuepress``` 

   这个文件夹是作为整个博客的项目目录

   > 目录名自己随便起，没啥强制性要求

3.  项目初始化 

   ```
   cd Vuepress
   npm init -y
   ```

   > 进入创建的目录并且初始化

    初始化后会生成一个`package.json`文件 

4.  在当前目录中创建一个`docs`目录 

   ```
   mkdir docs
   ```

   主要存放博客书记内容

   > 我觉得这个docs应该是不可更改的，因为我看别的博客也是说的docs，当然也是有可能可以弄别的名字

5.  首页内容书写(默认主题提供) 

   ```
   ---
   home: true
   heroImage: /logo.jpg
   actionText: 快速上手 →
   actionLink: /zh/guide/
   features:
   - title: 简洁至上
     details: 以 Markdown 为中心的项目结构，以最少的配置帮助你专注于写作。
   - title: Vue驱动
     details: 享受 Vue + webpack 的开发体验，在 Markdown 中使用 Vue 组件，同时可以使用 Vue 来开发自定义主题。
   - title: 高性能
     details: VuePress 为每个页面预渲染生成静态的 HTML，同时在页面被加载的时候，将作为 SPA 运行。
   footer: MIT Licensed | Copyright © 2018-present Evan You
   ---
   ```

   > 这个复制的时候一定要带上---，因为这是好像是Markdown的一个语法，类似于代码块前后要用```来括起来一样。
   >
   > home, actionText等的作用效果可以等做完再自己看着理解，都不难

# 四、核心配置

1.  在`docs`目录下创建`.vuepress`目录 

   ```
   cd docs
   mkdir .vuepress
   ```

   进入docs文件夹饼创建.vuepress文件夹

2.  新建总配置文件`config.js` 

   ```
   cd .vuepress
   touch config.js
   ```

   > config是整个项目的核心配置文件，所有菜单、栏目相关的配置均配置在该模块中

3.  在`config.js`中加入内容 

   ```
   module.exports = {
       title: '知码学院',
       description: '君哥带你上王者',
       dest: './dist',
       //运行所在目录，不写的话默认在.vuepress目录下
       port: '7777',
       //port端口号，它和最后的localhost后面跟的数字一样
       head: [
           ['link', {rel: 'icon', href: '/logo.jpg'}]
       ],
       markdown: {
           lineNumbers: true
       },
       themeConfig: {
       
          	//导航栏
           nav: [{
               text: '懵逼指南', link: '/guide/'
           }],
           
          //侧边栏，之后详解
           sidebar: {'/guide/':[
               {
                     title:'新手指南',
                     collapsable: true,
                     children:[
                       '/guide/notes/one',
                     ]
                   },
                   {
                     title:'知码学院',
                     collapsable: true,
                     children:[
                       '/guide/notes/two',
                     ]
                   }
               ]
           },
           sidebarDepth: 2,
           lastUpdated: 'Last Updated',
           searchMaxSuggestoins: 10,
           serviceWorker: {
               updatePopup: {
                   message: "有新的内容.",
                   buttonText: '更新'
               }
           },
           editLinks: true,
           editLinkText: '在 GitHub 上编辑此页 ！'
       }
   }
   ```

4. 使用```vuepress dev docs``` 来运行，运行之后给个地址·```http://localhost:7777/```

## 可能遇到的问题

### touch指令无效

问题所在：windows想使用touch指令需要单独安装 

解决：``` npm install touch-cli -g ```安装即可使用

## 顶部导航配置

1.  在当前目录创建一个`nav.js` 

   > 其实就是.vuepress目录

   输入

   ```
   module.exports = [
       {
           text: '懵逼指南', link: '/guide/
           //直接显示出来的
       },
       {
           text: '面试宝典', link: '/baodian/',
   		items: [
   		//通过items来形成类似下拉的效果
   		//text可以多次嵌套，但一般嵌套2，3次
               {text: '初级开发篇', link: '/baodian/zero/'},//这是内部链接
               {text: '中高进阶篇', link: '/baodian/high/'},
           ]
       },
       {
           text: '工具箱',
           items: [
   			{
                   text: '在线编辑',
   				items: [
   					{text: '图片压缩', link: 'https://tinypng.com/'}//外部链接
   				]
               },
   			{
                   text: '在线服务',
   				items: [
   					{text: '阿里云', link: 'https://www.aliyun.com/'},
   					{text: '腾讯云', link: 'https://cloud.tencent.com/'}
   				]
               },
   			{
                   text: '博客指南',
   				items: [
   					{text: '掘金', link: 'https://juejin.im/'},
   					{text: 'CSDN', link: 'https://blog.csdn.net/'}
   				]
               }
           ]
       }
   ]
   
   ```

   与此同时也要修改核心配置文件

   将其中的nav相关改成```nav: require("./nav.js"),``` 

   > ./ 是指当前目录

## 侧边栏配置

1. `sidebar`是左侧标题导航，可以指定配置也可以设置为`auto`

   ```
   module.exports = {
   	'/guide/': require('../guide/sidebar'),
   
   	'/baodian/zero': require('../baodian/zero/sidebar'),
   	'/baodian/high': require('../baodian/high/sidebar'),
   }	
   ```

   + /guide/：该key是与上述的nav中link对应，在请求nav时会自动切换当前的侧边目录，所以需要该配置
   + /baodian/zero同理
   + 后续的require表示引入一个指定目录的sidebar.js文件，其本身可以直接写在这里，但为了方便维护我们需要将每个模块的侧边栏js抽取出来，单独存放在内容模块的目录下

    其中一个目录：`/docs/guide/sidebar.js` 

   ```
   module.exports = [
   		{
   		  title:'新手指南',
   		  collapsable: true,
   		  children:[
   			'/guide/notes/one',
   		  ]
   		},
   		{
   		  title:'知码学院',
   		  collapsable: true,
   		  children:[
   			'/guide/notes/two',
   		  ]
   		}
   	]
   ```

   one和two对应的文件也要记得创建

   如果目标最后是/的话，最好在对应的文件夹里面加上README.md，

   因为最后是/的话，就默认寻找README.md
   
   > `title`：表示侧边栏大标题
   >
   > `collapsable`：是否可收缩
   >
   > `children`：具体的`.md`文件，这里无需指定后缀

# 五、静态资源配置

1. 图片

    默认的图片目录是`/docs/.vuepress/public` 

   我在public里新建一个img文件夹，添加logo.png图片

   在控制主页的README.md里修改为```heroImage: /img/logo.png```

2. css格式

   + public里新建css文件夹，创建style.css文件```touch style.css```

   + 输入

     ```
     #app .navbar .home-link span:before{
     	display: inline-block;
     	content:'';
     	width: 3rem;
     	height:2.4rem;
     	background:url('../img/logo.png') no-repeat;
     	background-size:100% 100%;
     	vertical-align: middle;
     }
     ```

   + 最后修改.vuepress 目录下的config.js里的head属性

     ```
     head: [
             ['link', {rel: 'icon', href: '/logo.jpg'}],
             ["link", { rel: 'stylesheet', href: '/css/style.css'}],
         ],
     ```

3. js

   + public里新建js文件夹，创建main.js文件

   + 输入

     ```function init(){
     function init(){
     	console.log(123);
     }
     //延迟加载，为了防止读取界面节点时界面未加载完成
     setTimeout("init()",500)
     ```

   + 在.vuepress 目录下的config.js里的head里添加

     ```
     ['scripts', {charset: 'utf-8', src:'/js/main.js'}],
     ```

## 可能遇到的问题

### 加载页面全是字符

猜测问题：在全局配置文件里的config.js文件里的head里操作不规范

+ scripts后面是否有, 号
+ []后面是否写了, 

# 六、主题

```https://vuepress-theme-reco.recoluan.com/ ``` 这个主题打不开

```https://www.chanx.tech/``` 这个是橙小白的博客，看起来挺不错的

```https://tsanfer.xyz/``` 这个推荐的，也还可以

```https://www.it235.com/``` 这个也还好吧