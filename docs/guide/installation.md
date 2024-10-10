# 使用vite构建Vue+TypeScript项目
在使用 Vite 创建项目时，通常会使用一些命令来初始化和设置项目。Vite 是一个快速的前端构建工具，支持现代 JavaScript 框架如 Vue、React、Svelte 等。下面将详细介绍如何使用 Vite 创建项目的各种命令以及它们之间的区别。
## 1.安装 Vite
首先，确保您的计算机上已经安装了Node.js和npm（Node.js的包管理器）。然后，在终端中输入以下命令来全局安装Vite：
```
npm install -g create-vite
```
或者使⽤ yarn 或 pnpm ：
```
--------------------------------------
yarn global add create-vite
--------------------------------------

# 或

--------------------------------------
pnpm add -g create-vite
--------------------------------------

```
## 2.创建 Vite 项目
Vite推荐使用npm create vite@latest命令来初始化项目。这是因为create-vite这个包会自动根据模板来设置项目配置。基本的命令格式如下：
```
npm create vite@latest
```
好的，下面是完善后的文本：

---

## 3.选择模板

在使用以上命令创建项目时，你会被提示选择一个项目模板。常见的模板选项包括：

vanilla: 原生 JavaScript 项目<br>
vanilla-ts: 原生 TypeScript 项目<br>
vue: Vue 3 项目<br>
vue-ts: Vue 3 + TypeScript 项目<br>
react: React 项目<br>
react-ts: React + TypeScript 项目<br>
preact: Preact 项目<br>
preact-ts: Preact + TypeScript 项目<br>
lit: Lit 项目<br>
lit-ts: Lit + TypeScript 项目<br>
svelte: Svelte 项目<br>
svelte-ts: Svelte + TypeScript 项目<br>
如果你已经知道自己想要使用的模板，可以直接在命令行中指定，而不需要通过交互式的选项来选择。例如，如果你想创建一个 Vue 3 项目，可以使用以下命令：
```
npm create vite@latest my-vue-app -- --template vue
```
这条命令将会创建一个名为 my-vue-app 的 Vue 3 项目。
## 4.项目启动和开发
创建完项目后，需要进入项目目录并安装依赖：

```
cd my-vue-app
npm install
```
然后，运行以下命令启动开发服务器：

```
npm run dev
```
Vite 会启动一个开发服务器，通常会在 http://localhost:5173 上运行。

使用 Vite 创建项目时，可以利用不同的模板快速启动各种类型的应用程序。Vite 提供了多种内置的模板和脚手架选项，支持不同的框架和技术栈。

