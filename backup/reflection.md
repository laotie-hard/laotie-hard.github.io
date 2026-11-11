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

# quesion3:

对一个十进制数的各位数字做一次平方和，称作一次迭代。如果一个十进制数能通过若干次迭代得到 1，就称该数为幸福数。1 是一个幸福数。此外，例如 19 经过 1 次迭代得到 82，2 次迭代后得到 68，3 次迭代后得到 100，最后得到 1。则 19 就是幸福数。显然，在一个幸福数迭代到 1 的过程中经过的数字都是幸福数，它们的幸福是依附于初始数字的。例如 82、68、100 的幸福是依附于 19 的。而一个特立独行的幸福数，是在一个有限的区间内不依附于任何其它数字的；其独立性就是依附于它的的幸福数的个数。如果这个数还是个素数，则其独立性加倍。例如 19 在区间[1, 100] 内就是一个特立独行的幸福数，其独立性为 2×4=8。

另一方面，如果一个大于1的数字经过数次迭代后进入了死循环，那这个数就不幸福。例如 29 迭代得到 85、89、145、42、20、4、16、37、58、89、…… 可见 89 到 58 形成了死循环，所以 29 就不幸福。

本题就要求你编写程序，列出给定区间内的所有特立独行的幸福数和它的独立性。

输入格式：
输入在第一行给出闭区间的两个端点：1<A<B≤10 
4
 。

输出格式：
按递增顺序列出给定闭区间 [A,B] 内的所有特立独行的幸福数和它的独立性。每对数字占一行，数字间以 1 个空格分隔。

如果区间内没有幸福数，则在一行中输出 SAD。

## ds-answer:
````
#include <iostream>
using namespace std;

int nxt(int x) {         //求位和
    int s = 0;
    while (x) {
        int d = x % 10;
        s += d * d;
        x /= 10;
    }
    return s;
}

bool isPrime(int x) {     //求素数
    if (x < 2) return false;
    for (int i = 2; i * i <= x; i++) {
        if (x % i == 0) return false;
    }
    return true;
}

int main() {
    int A, B;
    cin >> A >> B;

    const int MAXN = 10005;

    bool happy[MAXN] = {false};    //幸福数
    int len[MAXN] = {0};      //计算独立性用
    int seen[MAXN] = {0};   //判重
    int stamp = 0;       //轮次数

    for (int x = A; x <= B; x++) {
        stamp++;
        int cur = x;
        int cnt = 0;
        bool ok = false;

        while (true) {
            if (cur == 1) {
                ok = true;
                break;
            }
            if (seen[cur] == stamp) {      //是否有死循环
                ok = false;
                break;
            }
            seen[cur] = stamp;
            cnt++;
            cur = nxt(cur);
        }

        if (ok) {
            happy[x] = true;
            len[x] = cnt;
        }
    }         //记下幸福数

    bool used[MAXN] = {false};

    for (int x = A; x <= B; x++) {
        if (!happy[x]) continue;

        int cur = x;
        bool first = true;

        while (cur != 1) {
            if (!first && cur >= A && cur <= B) {        // !first跳过对x的记录,并记录范围内的幸福数
                used[cur] = true;
            }
            first = false;
            cur = nxt(cur);
        }
    }

    bool any = false;

    for (int x = A; x <= B; x++) {
        if (happy[x] && !used[x]) {           //直接用[x]，不在意具体下标排布
            any = true;
            int k = len[x];
            if (isPrime(x)) k *= 2;
            cout << x << " " << k << "\n";
        }
    }

    if (!any) {
        cout << "SAD\n";
    }

    return 0;
}
````
**任务板块的分解，对数组下标与值的练习（类似q1），死循环判断（重复判断），bool类型的数组，多个数组达成多维数组作用，变量和判断的位置存放**

# 段错误

1. 数组的越界（访问问题）
2. 野指针or无指针
3. size_t or auto型时,x<0->x=+max