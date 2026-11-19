# 单链表
1.线性表的创建
```
typedef struct node{
       elemtype data;
       struct node* next;     //自引用struct node
}Node;    //Node:一个结构整体
typedef struct node* linklist;     //linklist:指向结构体的指针or头节点（代表一整个线性表）  Ai->Ai+1(p->next)
```
2.读取元素
```
Status getelem(linklist L,elemtype&e,int i){
linklist p=L->next;
int j=0;       
while(p&&j<i){    //p为p!=NULL
p=p->next;
j++;
}
if(p!||j>i){
return error;
}
else{
e=p->data;
return true;
}
```

3.插入
```
Status insert(linklist& L,int i,elemtype e){
int j=1;
linklist p=L;    //p为头指针，不是第一个链表
while(p&&j<i){
p=p->next;
j++;
}
linklist s=new linklist;
s->data=e;
s->next=p->next;
p->next=s;
return ok;
}
```

4.删除，类型同上，注意顺序即可

5.创建
```
void creat(linklist& L,int n){
linklist p,r;
int i;
L=new linklist;
r=L;               //r指向L的尾部
for(i=0;i<n;i++){
p=new linklist;
p->data=
r->next=p;
r=p;
}
r->next=NULL;
}
```

6.删除
```
Status delete(linklist& L){
linklist p,q;
p=L->next;
while(p){
q=p->next;
delete p;
p=q;
}
}
```

# 循环链表+双向链表（双向循环链表）
## 循环链表
引入尾指针rear
## 双向链表
引入返回指针prior
