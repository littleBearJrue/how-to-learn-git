# git commit 内容规范配置

## 安装使用commitizen

### 1. 优先全局安装commitizen

```
npm install -g commitizen
```

#### 2. 进入项目所在目录

```
commitizen init cz-conventional-changelog --save --save-exact
```

### 3. 使用git cz命令来取代 git commit即可



## 对提交内容合法性校验

[具体参考地址](http://marionebl.github.io/commitlint/#/guides-local-setup?id=install-commitlint)

这种方式使用命令行的情况下会比较有效果，只要一步步跟着提示走就可以按着这个约定俗成的规范完成commit内容的书写。但缺点就是没法在tortoiseGit中使用。



## 配置在TortoiseGit中使用的commit内容提示

### 1. 找到git的用户配置文件.gitconfig

一般都在C://users//你的用户名

### 2. 打开.gitconfig增加以下一行代码

```
[commit]
	template = C:/Users/（你的用户名）/.git_commit_template.txt
```

### 3. 在.gitconfig的同级目录下新增一个件.git_commit_template.txt

[.git_commit_template.txt文件路径](http://gogit.oa.com/gameLibrary/client_document/src/master/git%E7%9B%B8%E5%85%B3/.git_commit_template.txt)



### 4. 之后再tortoiseGit上点击commit操作后，就会生成一份规范的模板内容


![commit_msg](http://gogit.oa.com/gameLibrary/client_document/src/master/git%e7%9b%b8%e5%85%b3/resources/commit_msg.png)











