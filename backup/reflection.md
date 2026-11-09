# quesion1:
天梯图书阅览室请你编写一个简单的图书借阅统计程序。当读者借书时，管理员输入书号并按下S键，程序开始计时；当读者还书时，管理员输入书号并按下E键，程序结束计时。书号为不超过1000的正整数。当管理员将0作为书号输入时，表示一天工作结束，你的程序应输出当天的读者借书次数和平均阅读时间。

注意：由于线路偶尔会有故障，可能出现不完整的纪录，即只有S没有E，或者只有E没有S的纪录，系统应能自动忽略这种无效纪录。另外，题目保证书号是书的唯一标识，同一本书在任何时间区间内只可能被一位读者借阅。

输入格式：
输入在第一行给出一个正整数N（≤10），随后给出N天的纪录。每天的纪录由若干次借阅操作组成，每次操作占一行，格式为：

书号（[1, 1000]内的整数） 键值（S或E） 发生时间（hh:mm，其中hh是[0,23]内的整数，mm是[0, 59]内整数）

每一天的纪录保证按时间递增的顺序给出。

输出格式：
对每天的纪录，在一行中输出当天的读者借书次数和平均阅读时间（以分钟为单位的精确到个位的整数时间）。
## answer:
````
#include <iostream>
using namespace std;

int main() {
    int N;
    cin >> N;

    while (N--) {           //二维转一维处理
        int start[1001];
        for (int i = 0; i <= 1000; i++) {
            start[i] = -1;          //防止与0冲突
        }

        int count = 0;
        int total = 0;

        int id;
        char op;

        while (cin >> id >> op) {
            int h, m;
            char colon;
            cin >> h >> colon >> m;

            if (id == 0) break;

            int t = h * 60 + m;

            if (op == 'S') {
                start[id] = t;        //利用[]和值把id与time联系
            } else if (op == 'E') {
                if (start[id] != -1) {     //同时作为判断条件
                    total += t - start[id];
                    count++;
                    start[id] = -1;
                }
            }
        }

        if (count == 0) {
            cout << "0 0" << endl;
        } else {
            int avg = (total + count / 2) / count;
            cout << count << " " << avg << endl;
        }
    }

    return 0;
}
````
**1.变量的设置（循环内外与输入安排）  2.利用数组的下标和数量建立对应关系，并可以用于逻辑判断（类布尔）**
# quesion2:
数学领域著名的“哥德巴赫猜想”的大致意思是：任何一个大于2的偶数总能表示为两个素数之和。比如：24=5+19，其中5和19都是素数。本实验的任务是设计一个程序，验证20亿以内的偶数都可以分解成两个素数之和。

输入格式：
输入在一行中给出一个(2, 2 000 000 000]范围内的偶数N。

输出格式：
在一行中按照格式“N = p + q”输出N的素数分解，其中p ≤ q均为素数。又因为这样的分解不唯一（例如24还可以分解为7+17），要求必须输出所有解中p最小的解。
## my answer(超时):
````
#include<iostream>
#include<cmath>
using namespace std;

bool isprime(long long a){
    for(long long i=2;i<=sqrt(a);i++){
        if(a%i==0){
            return 0;
        }
    }
    return 1;
}

int main(){
    long long n;
    cin>>n;
    long long p=2;
    long long q=2;
    int bo=0;
    for(;p<n;p++){
        if(isprime(p)){
            for(q=2;q<n;q++){
                if(isprime(q)){
                    if(p+q==n){
                        cout<<n<<" = "<<p<<" + "<<q;
                        bo=1;
                        break;
                    }
                }
            }
        }
        else
            continue;
        if(bo==1)
            break;
    }
    return 0;
}

````
## ds-anwer:
````
#include <iostream>
using namespace std;

bool isPrime(long long x) {
    if (x < 2) return false;
    for (long long i = 2; i <= x / i; i++) {     //   i*i优于sqrt调用
        if (x % i == 0) return false;
    }
    return true;
}

int main() {
    long long n;
    cin >> n;

    // 先试 p = 2(2是唯一的素偶数，但是没必要：偶-偶=偶必为合数)
    if (isPrime(n - 2)) {
        cout << n << " = 2 + " << n - 2;
        return 0;
    }

    // 再试奇数 p = 3, 5, 7, ...
    for (long long p = 3; p <= n / 2; p += 2) {   //只过奇数
        if (isPrime(p) && isPrime(n - p)) {            //用（n-p）代替第二次循环
            cout << n << " = " << p << " + " << n - p;
            return 0;
        }
    }

    return 0;
 }
````
**对函数调用的优化，对数据的处理，对for循环的改良（时间复杂度）**