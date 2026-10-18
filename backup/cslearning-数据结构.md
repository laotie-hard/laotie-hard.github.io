一：线性表
  1.数据元素的有限序列，由起始节点到终端结点，前驱与后继 
  2.1顺序存储：占用一片连续的存储空间
  储存空间不灵活，空间复杂度高
  例如：多项式的系数与指数存放：
  typedef struct{
       float p;  //也可以typedef char/~ elemtype;方便后续管理维护
       int e;
  }poly;
  typedef struct{
       poly *elem;  //poly类型的数组（需申请内存，注意指针的类型） or elemtype elem[max];(max需定义)
       int length;
  }list;