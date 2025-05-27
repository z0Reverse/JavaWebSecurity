
# UserDao的insertuserpay方法
疑似存在sql注入风险
![[Pasted image 20250527043446.png]]
未采用预编译等方法限制
分析代码之后的确存在sql注入风险，但是定位到使用该方法的地方之后
![[Pasted image 20250527044123.png]]
向上溯源就断掉了，该api或者说方法没有被使用

