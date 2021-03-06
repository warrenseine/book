---
layout: content
title: 别名
prev: 配置
next: 算数
link_prev: /zh-cn/configuration.html
link_next: /zh-cn/math.html
---

Nu 编写长管道的能力可以让你对数据和系统进行大量控制，但这需要打很多字。在预想中，你可以保存写好的管道并重复使用。

这就是别名要做的事情。

一个别名让你为一个命令块创建一个较短的名字。当别名被执行时，它就表现得像你输入了完整的命令块一样。

例如：

```
> alias ls-names [] { ls | select name }
> ls-names
────┬────────────────────
 #  │ name
────┼────────────────────
  0 │ 404.html
  1 │ CONTRIBUTING.md
  2 │ Gemfile
  3 │ Gemfile.lock
  4 │ LICENSE
```

## 参数

别名同样可以使用传递给命令块的可选参数。它们中的每一个在块中都是新的变量。

```
> alias e [msg] { echo $msg }
> e "hello world"
hello world
```

可以有任意数量的参数。当用户未提供值时，块中的变量将会作为 Nothing 并被移除。

## 持久化

默认情况下，别名只在当前会话中可用。这对临时性地帮助和测试新别名有用，单如果别名已经能真正地工作了，它们就需要被持久化。要做到它，用 `--save` （或 `-s` 的短形式）来调用 alias 指令。例如：

```
alias e --save [msg] { echo $msg }
```

别名将被存储在启动配置文件中，你可以使用 `config --get startup` 来查看它们。如果你得到一个错误，则是 `startup` 配置文件还不存在。

你同样可以直接在 config.toml 文件中编辑别名，例如使用 `vi`：

```
config --path | vi $it
```
