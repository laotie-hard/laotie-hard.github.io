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
void getelem(linklist L,elemtype&e){
