//由于我先在word上做笔记，部分大小写可能出现混乱（首字母）
一：线性表
  1.数据元素的有限序列，由起始节点到终端结点，前驱与后继 
  2.1顺序存储：占用一片连续的存储空间
  储存空间不灵活，空间复杂度高,插入删除麻烦
  例如：多项式的系数与指数存放：
```  
typedef struct{
       float p;  //也可以typedef char/~ elemtype;方便后续管理维护
       int e;
  }poly;
  typedef struct{
       poly *elem;  //poly类型的数组（需申请内存，注意指针的类型） or elemtype elem[max];(#define max n) or new elemtype(n);
       int length;
  }list;
```
通常预定一些常量：对1错0 overflow-2；int->Status(判断返回类型)
2.2功能实现：
1.初始化:
```
Status inilist (list & L){
	L.elem=new elemtype(max);
	If(!L.elem)  //查看内存地址
		Exit(overflow);  //防止分配失败
	L.length=0;
	Return OK;
}
```
2.删除：
```
Void destroylist(list &L){
	if(L.elem)
		Delete L.elem;
}
```
3.取值：
```
Status getelem(list L,int i,int &e){
	//确定i值
	If(i<1||i>L.length)
		Return 0;
	e=L.elem[i-1];

	return 1;
}
```

4.查找：

```
	int findelem(list L,int e){
		int i=0;
		for(L.elem[max]){
			if(L.elem[i]==e)
				return (i+1);
			i++;
	}
	return 0;
	}
```
ASL=P(被寻找所需次数)*C（被找到概率）的n项求和
5.插入：
```
	Status inputlist(list &L,int i,int e){
		If(i<1||i>L.length+1)
			Return 0;
		If(L.length==max)
				Reurn 0;
		For(int t=L.length-1;t>=i-1;t--){
				L.elem[t]=L.elem[t+1];
		}
		L.elem[i-1]=e;	
		L.length++;
		Return OK; 
	}
```
6.删除：
```
	Int delrteelem(list&L,int i,int &e){
		If(i<1||i>L.length)
			Return 0;
		e=L.elem[i-1];
		For(int t=i;t<L.length;t++)
			L.elem[t-1]=L.elem[t];
		L.length--;
		Return e;	}
```
小总结:
	对于for循环的书写需注意（条件），数组下标与个数之间的转化，对于输入的边界审查，代码的格式细节