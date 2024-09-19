# 使用 Vue 3 构建你的 GitHub 个人主页

在这篇文章中，我将带你一步步从零开始使用 Vue 3 构建一个简单而美观的 GitHub 个人主页。如果你是初学者，不用担心，我会详细讲解每一步的操作，让你能够轻松上手。

## 环境准备

在开始之前，请确保你的开发环境已经准备好：

1. **Node.js 和 npm**：Vue CLI 依赖于 Node.js，你可以通过在命令行中输入 `node -v` 和 `npm -v` 检查是否已经安装。
Node.js可进入以下官方链接下载：
```bash
https://nodejs.org/zh-cn
```
 Node.js自带npm。
 
3. **Vue CLI**：通过以下命令全局安装 Vue CLI：


```bash
   npm install -g @vue/cli
```

## 创建 Vue 3 项目
现在我们开始创建一个新的 Vue 3 项目：

1.创建项目：

打开终端，进入你希望存放项目的目录，或进入目录路径下cmd，运行以下命令：

```bash
  vue create my-github-page
```
![](https://i-blog.csdnimg.cn/direct/b0aeb17a6122412cb984df8f9186d4e1.png)
运行后出现以上信息，可以上下选择Vue3或2的项目模板，Enter确认。

2.进入项目目录并启动开发服务器：



```bash
cd my-github-page
npm run serve
```
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/5d688c67801b45ae9b8b4a5449571d39.png)

启动成功后，打开浏览器并访问 http://localhost:8080/，你会看到 Vue 默认的欢迎页面。



## 项目结构介绍
生成的 Vue 项目有以下基本结构：



```bash
my-github-page/
│
├── public/          # 静态资源文件夹，存放公共资源
│   ├── index.html   # 入口HTML文件
│
├── src/             # 主代码目录
│   ├── assets/      # 静态资源文件夹，存放图片、样式等
│   ├── components/  # Vue 组件文件夹
│   ├── views/       # 页面文件夹（可选）
│   ├── App.vue      # 主应用组件
│   ├── main.js      # 入口JavaScript文件
│
├── package.json     # 项目依赖和脚本
└── README.md        # 项目文档
```
以下需要修改的开发文件请在这个结构里找。
## 开发个人主页

###### 1.修改 App.vue

首先，我们用Vscode或notepad++等软件打开App.vue文件，在其中添加导航栏、个人简介部分和项目展示部分。


```html
<template>
  <div id="app">
    <header>
      <h1>My GitHub Page</h1>
      <Navbar />
    </header>

    <main>
      <section id="about">
        <h2>About Me</h2>
        <p>Hi, I'm [Your Name]. I am a software developer with a passion for open source and building awesome projects.</p>
      </section>

      <section id="projects">
        <h2>Projects</h2>
        <ul>
          <li v-for="project in projects" :key="project.id">
            <a :href="project.url">{{ project.name }}</a> - {{ project.description }}
          </li>
        </ul>
      </section>

      <section id="contact">
        <h2>Contact</h2>
        <p>You can reach me at <a href="mailto:youremail@example.com">youremail@example.com</a>.</p>
      </section>
    </main>

    <footer>
      <p>&copy; 2024 My GitHub Page</p>
    </footer>
  </div>
</template>

<script setup>
import { reactive } from 'vue';
import Navbar from './components/Navbar.vue';

const projects = reactive([
  { id: 1, name: "Project One", description: "This is a project description", url: "https://github.com/yourusername/project-one" },
  { id: 2, name: "Project Two", description: "This is another project description", url: "https://github.com/yourusername/project-two" }
]);
</script>

<style>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  background-color: #f4f4f4;
}

header {
  background-color: #333;
  color: #fff;
  padding: 10px 0;
  text-align: center;
}

header h1 {
  margin: 0;
}

nav ul {
  list-style-type: none;
  padding: 0;
}

nav ul li {
  display: inline;
  margin: 0 10px;
}

nav ul li a {
  color: #fff;
  text-decoration: none;
}

main {
  padding: 20px;
}

section {
  margin-bottom: 40px;
}

footer {
  background-color: #333;
  color: #fff;
  text-align: center;
  padding: 10px 0;
}
</style>
```

###### 2. 创建并使用组件
为了更好地组织代码，我们可以将导航栏部分拆分成一个独立的组件。

1.创建 Navbar.vue 组件：

在 src/components/ 目录下创建一个名为 Navbar.vue 的文件：


```html
<template>
  <nav>
    <ul>
      <li><a href="#about">About Me</a></li>
      <li><a href="#projects">Projects</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>
</template>

<style scoped>
nav {
  background-color: #333;
  color: #fff;
  padding: 10px 0;
  text-align: center;
}

nav ul {
  list-style-type: none;
  padding: 0;
}

nav ul li {
  display: inline;
  margin: 0 10px;
}

nav ul li a {
  color: #fff;
  text-decoration: none;
}
</style>
```
2.	在 App.vue 中使用 Navbar 组件：

在 App.vue 中，我们已经通过 import Navbar from './components/Navbar.vue'; 引入了 Navbar.vue 组件，并在 `<template>` 部分使用了 `<Navbar />` 标签来渲染它。


###### 3. 添加项目数据

使用 Vue 3 的 reactive API，我们已经在 App.vue 中定义了项目数据：


```html
const projects = reactive([
  { id: 1, name: "Project One", description: "This is a project description", url: "https://github.com/yourusername/project-one" },
  { id: 2, name: "Project Two", description: "This is another project description", url: "https://github.com/yourusername/project-two" }
]);
```

###### 4. 样式美化

你可以继续使用 CSS 或者引入 CSS 框架来美化你的页面，使之更符合个人风格。
完成以上步骤后，再打开http://localhost:8080/，你就能看到有初步框架的页面了。


## 部署到 GitHub Pages

当你完成开发并准备上线时，可以将项目部署到 GitHub Pages：

###### 构建项目：

```java
npm run build
```

###### 将构建好的文件上传到 GitHub：

我们可以使用 gh-pages 工具将 dist 文件夹中的内容上传到 GitHub 仓库的 gh-pages 分支：

安装 gh-pages:

```java
npm install gh-pages --save-dev
```

在 package.json 中添加一个 deploy 脚本：


```java
"scripts": {
  "deploy": "npm run build && gh-pages -d dist"
}
```

运行部署命令：




```java
npm run deploy
```

这会将你的项目部署到 GitHub Pages，几分钟后你就能在浏览器中访问到你的个人主页了。

## 总结

通过这篇文章的指导，你应该已经学会了如何从零开始使用 Vue 3 创建一个个人主页并且将其部署到GitHub上。你可以根据自己的需要进一步扩展和美化你的主页。如果在过程中遇到问题，欢迎留言讨论！


转载请注明出处。
