# Git提交内容规范
## 提交内容规范的意义：
1. 统一团队的commit标准，有利于后续对代码的review、版本发布、自动化生产change log等
2. 可以提供更多有效的历史信息，方便快速预览以及配合cherry-pick快速合并代码

## 提交日志的基本格式
```
<type>(<scope>): <subject>
    <空行>
<body>
    <空行>
<footer>
```

具体描述:
```
标题行：50个字符以内，描述主要变更内容

主体内容：更详细的说明文本，建议72个字符以内。 需要描述的信息包括:

1. 为什么这个变更是必须的? 它可能是用来修复一个bug，增加一个feature，提升性能、可靠性、稳定性等等
2. 他如何解决这个问题? 具体描述解决问题的步骤
3. 是否存在副作用、风险? 

尾部：如果需要的化可以添加一个链接到issue地址或者其它文档，或者关闭某个issue。
```

## Commit message格式说明
Commit message一般包括三部分：Header、Body和Footer

### Header说明
`type(scope):subject`
type：用于描述说明commit的类别，目前规定的提交类别有：
1. feat: 新增功能模块
2. fix: 修复bug
3. update: 更新功能
4. docs: 提交/修改文档
5. refactor: 代码重构，未新增任何功能和修复任何bug
6. build：改变构建流程，新增依赖库，工具等
7. style: 仅仅修改了代码的样式
8. test: 提交/修改测试用例
9. revert: 对代码的回滚

scope:用于说明commit的影响范围【可选填】
subject:commit的简要说明概况

### Body说明
对本次commit内容的详细描述，可分多行描述，把此次提交涉及到的信息分行写清楚

### Footer说明【可选填】
1. 不兼容变动：需要描述相关信息
2. 关闭指定Issue：输入Issue信息

### 例子展示
```
【feat】: 新增牌型库
    1. 新增牌型大对子基础牌型库
    2. 新增牌型顺子基础牌型库
```

