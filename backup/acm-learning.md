# 输入
## 一行若干数：
```
int x;
while(cin >> x){
}
```
## n行若干数：
```
int n;
while(cin >> n){ 
    for(int i=0;i<n;i++){
        cin >> arr[i];
    }
}
```
## 若干行若干数：
```
#include \<iostream\>
#include \<string\>
#include \<sstream\>
#include \<vector\>
using namespace std;

int main(){
    string line;
    while(getline(cin, line)){
        stringstream ss(line);
        vector<int> v; 
        int num;
        while(ss >> num){
            v.push_back(num);
        }
        for(int i = 0; i < v.size(); i++){
            if(i != 0) cout << " ";    //输入空格（末尾无空格）
            cout << v[i];
        }
        cout << endl;
    }
    return 0;
}
```
# 前置数学

1. 变量类型的设计：int or double,int or long long... 注意输入数据范围，也可通过乘除顺序的改变控制范围
2.边界数据值（特值），注意输入数据边界
3.算法的复杂度，打表防超时