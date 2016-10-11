# freemarker 指令
## freemarker 代码片段
* <font color='red'>${....}</font>：interpolation(插值),freemarker输出值来替换括号内的表达式
* ftl标签：也称作指令，以 <font color='red'>#</font> 开头，用户自定义标签以 <font color='red'>@</font> 开头
* 注释：使用 <font color='red'> <#-- and --> </font>表示

## 基本指令
---
> ### if指令

if指令可以有条件的跳过模块的一些片段

>     指令语法:
>     <#if condition>
>     <#elseif condition>
>     <#else>
>     <#if>  
  
---
> ### list 指令  
  
list指令用于列表内容显示
>_else 指令从2.3.23版本开始支持，当数据内容为空时，才使用_  
>_sep 指令从2.3.23版本开始支持，用于显示每个数据之间的内容，如:苹果，橘子，菠萝,他们之间的逗号就可以用<#sep>, 来表示_
>
>     指令语法：
>     <#list sequence as item>
>         repeat each item <#sep>,<#sep>
>     <#else>  
>         when 0 item
>     <#list>

应用举例：
```
<ul>
	<#list misc.fruits as fruit>
		<li>${fruit}
	<#list>
</ul>
```
此方式有一个问题，若fruits数量为0时，依然会输出一个&lt;ul&gt;&lt;/ul&gt;标签

可修改为：
```
<#list misc.fruits>
	<ul>
		<#items as fruit>
			<li>${fruit>
		<#items>
	</ul>
<#list>
```
下面这种方式从2.3.23版本开始支持
```
<#list misc.fruits>
  <p>Fruits:
  <ul>
    <#items as fruit>
      <li>${fruit}<#sep> and</#sep>
    </#items>
  </ul>
<#else>
  <p>We have no fruits.
</#list>
```
---
> ### include 指令  

在模板中插入其他文件的内容

>     指令语法：
>     <#include desc>

