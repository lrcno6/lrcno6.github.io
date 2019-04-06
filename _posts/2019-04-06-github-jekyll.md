---
title: 在GitHub上用Jekyll搭建极简博客
description: 竟然不用安装Jekyll?
permalink: /github-jekyll.html
categories: [Jekyll]
tags: [GitHub Pages,Jekyll,blog,Markdown]
---

*注:本文默认你有Markdown及Git&GitHub的基础*

*所以请不要问我诸如怎样使用Git和怎样在GitHub上建仓库之类的问题*

---

## *GitHub Pages*

*GitHub Pages*是*GitHub*提供的一个静态网站功能

(因为GitHub Pages不支持后台功能,所以功能还是有限 ~~所以还不如自己开服务器~~)

通过*GitHub Pages*可以做一些简单、可访问的网站

现在*GitHub Pages*还支持*Jekyll*。这样我们就能实现一个博客了。

## step 1:建立一个*GitHub Pages*网站

1. 网站地址为: https://{username}.github.io/

	直接将仓库名设为{username}.github.io即可
2. 网站地址为: https://{username}.github.io/{repository-name}

	1. 将仓库名设为{repository-name}
	2. 确保存在master分支(在master分支上push一些东西)
	3. 打开Settings,找到*GitHub Pages*,在Source中的下拉框中选择master branch

		![github-jekyll-001](/pic/github-jekyll-001.png)

(如果你现在就想看效果,又有一些*HTML*知识的话,现在就可以在index.html里面写一些东西)

## step 2:使用*Jekyll*

1. 点击Settings/*GitHub Pages*中的Choose a theme按钮

	![github-jekyll-002](/pic/github-jekyll-002.png)
2. 选择一个你喜欢的主题,点击Select theme
3. 打开index.md,输入以下内容:

	```md
	---
	title: {title}
	description: {description}
	categories: [{categories}]
	tags: [{tags}]
	---
	
	{Markdown content}
	```

	例如:

	```md
	---
	title: 示例
	description: 一篇示例文章
	categories: [Jekyll]
	tags: [示例,Markdown,Jekyll]
	---

	# 示例

	只是一篇示例文章罢了
	```

	(front matter中的信息(如果不需要)可以不加)

4. commit, push后试一下效果(只能在master分支上)

	在浏览器打开https://{username}.github.io/或https://{username}.github.io/{repository-name}(有时会需要等几分钟网站才会更新)

	如果你能看到与选择主题时看到的类似界面时,说明你已经成功了!

## step 3:添加其它文章

<!-- 其实只要在仓库中添加{filename}.md或{filename}.html即可(其实*HTML*文件本人并没有试验过) -->

<!-- 地址就是https://{username}.github.io/{filename}.html或https://{username}.github.io/{repository-name}/{filename}.html -->

(在这里讲添加post的做法)

在仓库中添加_posts文件夹,下面就可以任意添加文件了,但必须加上日期。格式如下:

```
{year}-{mm}-{dd}-{title}.md 或 {year}-{mm}-{dd}-{title}.html
```


例如:

```
2019-04-06-github-jekyll.md
```

默认地址为https://{username}.github.io/{year}/{mm}/{dd}/{title}.html或https://{username}.github.io/{repository-name}/{year}/{mm}/{dd}/{title}.html

如果想修改地址,则需要在文章的front matter(就是开头有title和description的那个)中添加:

```md
permalink: {url}
```

例如:

```md
permalink: /github-jekyll.html
```

这样文章地址就是https://{username}.github.io/github-jekyll.html或https://{username}.github.io/{repository-name}/github-jekyll.html

## step 4: 修改默认布局

当你打开你的网站时,你也许会发现一些问题,例如文章标题,网页中的主标题和副标题可能不对。以下提供修改办法:

1. 复制/下载https://github.com/pages-themes/{theme-name}中的_layouts/default.html至你的仓库的_layouts/default.html

2. 修改网页中的主标题和副标题

	你可以通过直接查阅源代码,或者浏览器中的检查功能,找到default.html中设置主标题和副标题的标签。如: (可能不同)

	```html
	<h1 class="project-name">{{ page.title | default: site.title | default: site.github.repository_name }}</h1>
    <h2 class="project-tagline">{{ page.description | default: site.description | default: site.github.project_tagline }}</h2>
	```

	大致意思是说,如果这个page的标题非空(page.title),就使用它;否则用网站的标题(site.title)。如果网站标题也为空就使网站的*GitHub*仓库名

	下一句类似

	但这样做(至少个人认为)其实很蠢,有些多余,所以不如改成:

	```html
	<h1 class="project-name">{{ page.title }}</h1>
    <h2 class="project-tagline">{{ page.description }}</h2>
	```

3. 修改文章标题(未测试)

	这里的标题指的是*HTML*中title标签所指的标题

	因为default.html中的SEO已经通过title标签指定了标题,所以如果要修改标题只能用*JavaScript*。

	你可以在head标签的最后添加:

	```html
	<script>document.title="{title}"</script>
	```

4. 其它各种玄学操作

	这需要你有*HTML*和*JavaScript*的基础

## step 5:添加图片

你当然可以使用各种图床,但竟然你都有自己的网站了,为何不把图片放在网站里呢?

在仓库下添加pic(或其它名字)文件夹,把图片放在里面。之后就只需要:

```md
<!-- for Markdown -->
![{description}](/pic/{picture-name})
```

或者

```html
<!-- for HTML -->
<img src="/pic/{picture-name}" alt="{description}">
```

---

## 最后插一嘴

确实没安装Jekyll,但我们仍然能用它。副标题可不是唬人的。

by *lrcno6*