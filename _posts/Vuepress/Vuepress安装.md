# Vuepress安装

> 安装nodejs
> 安装npm

## 安装与环境初始化
```bash
# 在项目中安装vuepress
npm install -D vuepress
# 创建项目文件夹
mkdir vuepressDemo && cd vuepressDemo
# 初始化npm
npm init -y
# 修改package.json
"scripts": {
    "docs:dev": "vuepress dev docs", 
    "docs:build": "vuepress build docs"
}
# 建立docs文件夹和根目录（docs）下markdown文件README.md
mkdir docs && echo '# Hello VuePress' > docs/README.md
# 运行
npm run docs:dev

# 必要时要npm安装环境
npm install -D echarts
npm install -D echarts-stat
npm install -D moment
npm install -D ant-design-vue

# 可以访问后，在docs中build出.vuepress文件夹
# 在components中放置vue组件
……
# 使用开发模式npm run docs:dev
```


## 项目结构
```bash
.demo
├── docs
│   ├── README.md
│   ├── template_barChart.md
│   ├── template_layout_tabContent.md
│   ├── template_polarBarChart.md
│   └── .vuepress
│				├── components
│   		│		├── template_barChart.vue
│				│		├── template_describeTable.vue
│				│		├── template_info.vue
│				│		└── template_inputTable.vue
│ 	 		├── config.js
│ 	 		├── dist
│  			│		├── 404.html
│				│   ├── assets
│				│   │   ├── css
│				│   │   │   └── ...
│				│   │   ├── img
│				│   │   │   └── ...
│				│   │   └── js
│				│   │       └── ...
│				│   └── index.html
│				└── public
│						└── logo.png
├── node_modules
│   └── ...
└── package.json
```

## config.js内容
```bash
module.exports = {
	title: '智慧机组诊断平台前端界面Vue组件用户手册',
	description: '东方电机智慧机组诊断平台前端界面Vue组件用户手册',
	markdown: {
		lineNumbers: true	
	},
	themeConfig: {
		logo: '/logo.png',
		sidebar: {
			'/': [
					{
						title: '控件模板',
						collapsable: false,
						children: [
							{
								title: '棒图', 
								path: '../template_barChart.md'
							},
							{
								title: '极坐标棒图', 
								path: '../template_polarBarChart.md'
							},
						]
					},
					{
						title: '布局模板',
						collapsable: false,
						children: [
							{
								title: '布局-左中右导抽', 
								path: '../template_layout_tabContent.md'
							}
						]
					},
				]
			}
		}
	}
```

## package.json内容
```bash
{
  "name": "vuepressDemo",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "docs:dev": "vuepress dev docs",
    "docs:build": "vuepress build docs"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "ant-design-vue": "^1.7.4",
    "echarts": "^5.0.2",
    "echarts-stat": "^1.2.0",
    "markdown-it": "^12.0.4",
    "moment": "^2.29.1",
    "vue": "^2.6.12",
    "vue-resource": "^1.5.2",
    "vuepress": "^1.8.2"
  }
}
```

## 主页README.md
```markdown
---
home: true
heroImage: /logo.png
heroText: 智慧机组诊断平台
tagline: Vue组件用户手册
actionText: 详细信息
actionLink: /template_barChart.md
features:
- title: 内容说明
  details: 本文件为东方电机智慧机组诊断平台Vue组件用户手册，包括交付用户的控件清单、必要的说明、示例等
- title: 环境说明
  details: Vue2 + AntD + Echarts ...
- title: 开发原则
  details: 高可复用性、高可自定义性，适应用户二次开发所需
footer: Copyright © 2021 DFEM
---
```

```markdown
---
tags: 
	- ['布局', 'layout', 'Layout', '页面']
---

# 页面布局（左、中、右、导航、抽屉）
***

## 组件描述
> 通过多个插槽定义了某tab项下的布局，包括左、中、右、导航、抽屉四个部分

## 模板结构
<<< @/docs/.vuepress/components/template_layout_tabContent.vue#template

## Props参数
<<< @/docs/.vuepress/components/template_layout_tabContent.vue#props

## 调用示例
​```vue
<template>
	<div>
		<template_layout_tabContent 
			leftSectionSpan=7 
			centerSectionSpan=9 
			rightSectionSpan=7 
			naviSectionSpan=9 
			marginTop_naviSection='20px'/>
	</div>
</template>
​```

::: warning 注意
各区域的slot插槽为：leftSection、rightSection、centerSection、drawerButton、naviSection，
其中，drawerButton是用于放置开启当前页面信息抽屉按钮的位置
:::

::: details 源码
<<<@/docs/.vuepress/components/template_layout_tabContent.vue
:::

<template>
	<div>
		<template_layout_tabContent 
			leftSectionSpan=7 
			centerSectionSpan=9 
			rightSectionSpan=7 
			naviSectionSpan=1 
			marginTop_naviSection='20px'/>
	</div>
</template>
```

## addon
### 适应hope主题的配置
```bash
const { config } = require("vuepress-theme-hope");

module.exports = config(
	{
		title: '开发手册',
		theme: 'hope',
		markdown: {lineNumbers: true},
		themeConfig: {
			logo: '/logo.png',
			displayAllHeaders: true,
			activeHeaderLinks: false,
			nav: [
					{ text: "Echarts", link: "https://echarts.apache.org/zh/index.html", icon: "info" },
					{ text: "AntD-Vue", link: "https://antdv.com/docs/vue/introduce-cn/", icon: "markdown" },
					{ text: "Element", link: "https://element.eleme.cn/#/zh-CN/component/installation", icon: "markdown" },
					{
						text: '其它',
						items: [
							{
								text: 'Icons',
								items:[
									{text: 'iconfont', link: 'https://www.iconfont.cn/'}, 
									{text: 'simpleicons', link: 'https://simpleicons.org/'}, 
									{text: 'shields', link: 'https://shields.io/'}, 
									{text: 'fontawesome', link: 'https://fontawesome.dashgame.com/#google_vignette'}, 
								]
							}
						]
					}
				],
			sidebar: [
				{
					title: "环境",
					icon: "creative",
					collapsable: false,
					children: [
						{path: "./Confluence/Confluence安装", title: "Confluence"},  
						{path: "./Jira/Jira安装", title: "Jira"}, 
						{path: "./Gitlab/Gitlab安装", title: "Gitlab"}, 
						{path: "./Java/Java安装", title: "Java"},
						{path: "./Docker/Docker安装", title: "Docker"}, 
						{path: "./JDK/JDK安装", title: "JDK"}, 
						{path: "./Mysql/Mysql安装", title: "Mysql"}, 
						{path: "./Kafka/Kafka安装", title: "Kafka"}, 
						{path: "./Vuepress/Vuepress安装", title: "Vuepress"}, 
						{path: "node", title: "Nodejs"}, 
						{path: "vuepress", title: "Vuepress"}, 
					],
				}, {
					title: "操作",
					icon: "layout",
					collapsable: false,
					children: [
						{path: "./Linux/Linux操作", title: "Linux"}, 
						{path: "./Docker/Docker操作", title: "Docker"}, 
						{path: "./Git/Git操作", title: "Git"}, 
						{path: "./Kafka/Kafka操作", title: "Kafka"}, 
						{path: "./Vuepress/Vuepress操作", title: "Vuepress"},
					]
				}

			],
		}
	}
)

```