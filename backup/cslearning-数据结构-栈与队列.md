# 栈
1.定义
```
typedef int elemtype;
typedef struct{
elemtype data[max];
int top;         //栈顶
}stack;
``` 

2.插入
```
Status push(stack& s,elemtype e){
if(s->top==max-1)
return error;
s->top++;
s->data[s->top]=e;
return ok;
}
```

3.输出
```
Status pop(stcak& s,elemtype &e){
if(s->top==-1)         //-1表示0（0有下标表示）
return error;
e=s->data[s->top];
s->top--;
return ok;
}
```

# 链栈
1.定义
```
typeddef struct stacknode{
elemtype data;
struct stacknode *next;
}stacknode,*linkstackptr;          //货架

typedef struct
{
linkstackptr top;
int count;
}linkstack;                  //手册
```

2.进栈
```
Status push(linkstack& S,elemtype e){
linkstackptr s=new linkstackptr;
s->data=e;
s->next=S->top;
S->top=s;
S->count++;
return ok;
}
```

3.出栈类似，注意指针顺序与delete

# 队列
## 循环队列
