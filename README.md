# local-feed-generation
依赖RPageSearch，使用本地文件生成RSS/atom/feed，支持workflow自动持续构建

> **此项目依赖项目[RPageSearch](https://github.com/RavelloH/RPageSearch)所生成的文件`search.json`，请先参考RPageSearch的README构建你的`search.json`**

## 效果
参见以下链接
```
https://ravelloh.top/feed/rss.xml
https://ravelloh.top/feed/feed.json
https://ravelloh.top/feed/atom.xml
```

## 使用
1.先在[RPageSearch](https://github.com/RavelloH/RPageSearch)中配置`search.json`的自动生成  
2.编辑你的feed.js，修改以下信息：
```js
const dataFilePath = '../assets/data/search.json'; // search.json的路径
const storagePath = '../feed/';  // 最终保存文件的路径
const siteDomain = 'https://ravelloh.top'; // 你的站点域名
const authorINFO = {  // 你的个人信息
    name: 'RavelloH',
    email: 'ravelloh@outlook.com',
    link: 'https://ravelloh.top/',
};
```

以下部分是你的RSS信息，可自行按需编辑：
```js
const feed = new Feed({
    title: "RavelloH's Blog / RavelloH的博客",  // 标题
    description: 'RSS - 博客文章订阅更新',        // 描述
    id: 'http://ravelloh.top/',                // id
    link: 'http://ravelloh.top/',              // 链接
    language: 'zh',                            // 语言
    image: 'https://ravelloh.top/assets/images/avatar.jpg',  // 封面
    favicon: 'https://ravelloh.top/favicon.ico',             // 站点图标
    copyright: `Copyright © 2019 - ${new Date().getFullYear()} RavelloH. All rights reserved.`,  // 版权信息
    generator: 'https://github.com/RavelloH/local-feed-generation',  // 生成器信息
    feedLinks: {  // 订阅链接
        json: 'https://ravelloh.top/feed/feed.json',
        atom: 'https://ravelloh.top/feed/atom.xml',
        rss: 'https://ravelloh.top/feed/rss.xml',
    },
    author: authorINFO,
});

```
3.执行生成
```
npm install feed
node feed.js
```


## 自动生成
你可以使用Github Actions在文件发生更新时自动生成站点地图，参考本仓库中的`.github/workflows/sitemap.yml`设置即可。  
如果同时部署了RPageSearch的自动生成，需要将此项目的执行顺序调至RPageSearch之后

## 依赖
https://github.com/jpmonette/feed
