AppleScript学习笔记
===

###Tell语句
---
Tell语句的作用是指明脚本要控制的程序对象。Tell语句具有两种语法。

* 简单形式：`tell referenceToObject to statement`
* 复合形式：以`tell referenceToObject`开始，`end tell`结尾，中间包含命令语句。

	其中：referenceToObject为需要控制的对象，如一个应用程序，一个窗口。statement为命令语句，包含至少一个命令。

下面实例将关闭Finder程序中位于最前的窗口，将使用两种形式的Tell语句，两种形式作用结果相同。

```
-- 简单形式
tell front window of application "Finder" to close

-- 复合形式
tell application "Finder"
	close front window
end tell
```

###条件语句
---
If语句用于在满足一定条件的情况下执行语句，或者依据条件实现程序流程跳转。

* 简单形式：`if boolean then statement`
* 复合形式：

```
	if boolean1 then
		statement1
	else if boolean2 then
		statement2
	else
		statement3
	end if
```

###循环语句
---
####退出循环的命令  
退出循环的命令`exit`(完整的为`exit repeat`)。除了exit可以强制退出循环外，`return`也可以起到退出循环的作用，但是return的实际意义是退出当前的事件处理器，返回脚本流程。

####无限循环
```
repeat
	-- do something
end repeat
```
####限定次数循环
```
-- 语法中的n指定了循环多少次。n必须为整数或者整形数据，且大于等于1
repeat n times
	-- do something
end repeat	
```
####“直到”循环
```
-- 直到boolean为真，停止循环
repeat until boolean
	-- do something
end repeat
```
####“当”循环
```
-- boolean为真，循环反复执行
repeat while boolean
	-- do something
end repeat
```
####变量循环
```
-- stepValue可省略，默认值为1；loopVariable无需事先定义。
repeat with loopVariable from startValue to stopValue by stepValue
	-- do something
end repeat
```
####List类型数据循环
```
-- loopVariable无需事先定义，list是List型或者Record型数据。
-- 在循环体中，loopVariable将依次得到item 1 of list, item 2 of list...这样的指针（指向list中的第几项）。
-- 如果要得到list中的具体内容，使用contents of loopVariable来获得。
repeat with loopVariable in list
	-- do something
end repeat
```

###Considering/Ignoring语句（用于文本比较）
---
此语句可以在比较文本时，指定忽略或考虑某一属性（如大小写，空格等等）。

```
-- 考虑attribute1但忽略attribute2，其中but ignoring attribute2可以省略
-- considering和ignoring位置可以互换，但是end consideriing也要相应改成end ignoring。
considering attribute1 but ignoring attribute2
	-- compare texts
end considering
```

attribute应该为下面列表中的任意一个：

```
case			大小写
diacriticals	字母变调符号（如e和é）
hyphens			连字符（-）
numeric string	数字化字符串（默认是忽略的），用于比较版本号是启用它
punctuation		标点符号（,.?!等等，包括中文标点）
white space		空格
```