title: 搭建Hexo blog写作环境
date: 2015-3-12 14:17:16
categories: hexo
toc: true
---

2015-3-12 更新  完成使用GitHub搭建Hexo博客的记录

---

### **GitHub 篇**
使用GitHub Pages 搭建 独立博客，就是利用GitHub上对于每个单独的项目都可以设置演示与介绍的页面，简单来说就是创立 `gh-pages` 的分支。

### 首先你得有一个GitHub的账号 
  - 前往 [GitHub 官网地址](https://github.com)  注册一个账号 
 - 创建一个`repo`
 - 创建`gh-pages` branch
 
---

### 可以使用GitHub的二级域名 或者 购买一个域名

- [Daddy](https://www.Godaddy.com) 购买域名

- [dnspod](https://www.dnspod.cn/) 解析域名
 
---
### 在本地搭建 Hexo 

#### 搭建Git环境 

#### 搭建nodejs开发环境
  
#### 安装Hexo
  
#### 安装Hexo 的主题

- 初始化blog目录 

```
PS I:\GitHub\diary> hexo init
[info] Copying data
[info] You are almost done! Don't forget to run `npm install` before you start blogging with Hexo!
```
- 下载`Hexo`主题

```
PS I:\GitHub\diary> git clone https://github.com/iissnan/hexo-theme-next themes/next
Cloning into 'themes/next'...
remote: Counting objects: 2190, done.
remote: Compressing objects: 100% (110/110), done.
rRemote: Total 2190 (delta 50), reused 0 (delta 0), pack-reused 2073
 KiB/s
Receiving objects: 100% (2190/2190), 4.98 MiB | 56.00 KiB/s, done.
Resolving deltas: 100% (1145/1145), done.
Checking connectivity... done.
PS I:\GitHub\diary>
```
- 设置 `Hexo`


---
### 结合 travis 自动生成网页文件
 
---

### 结合prose.io 在线书写

---

### 结合koding.com 在线编译器 在线书写

---

### **VPS 篇**
待续。。。




### 更多：

- [如何搭建一个独立博客——简明Github Pages与Hexo教程](http://cnfeat.com/2014/05/10/2014-05-11-how-to-build-a-blog/)
- [Hexo 主题目录](https://github.com/hexojs/hexo/wiki/themes)
- [Hexo 官网](http://hexo.io/)