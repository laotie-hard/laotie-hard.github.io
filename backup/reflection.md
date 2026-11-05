quesion1:
天梯图书阅览室请你编写一个简单的图书借阅统计程序。当读者借书时，管理员输入书号并按下S键，程序开始计时；当读者还书时，管理员输入书号并按下E键，程序结束计时。书号为不超过1000的正整数。当管理员将0作为书号输入时，表示一天工作结束，你的程序应输出当天的读者借书次数和平均阅读时间。

注意：由于线路偶尔会有故障，可能出现不完整的纪录，即只有S没有E，或者只有E没有S的纪录，系统应能自动忽略这种无效纪录。另外，题目保证书号是书的唯一标识，同一本书在任何时间区间内只可能被一位读者借阅。

输入格式：
输入在第一行给出一个正整数N（≤10），随后给出N天的纪录。每天的纪录由若干次借阅操作组成，每次操作占一行，格式为：

书号（[1, 1000]内的整数） 键值（S或E） 发生时间（hh:mm，其中hh是[0,23]内的整数，mm是[0, 59]内整数）

每一天的纪录保证按时间递增的顺序给出。

输出格式：
对每天的纪录，在一行中输出当天的读者借书次数和平均阅读时间（以分钟为单位的精确到个位的整数时间）。
answer1:
````
#include <iostream>
using namespace std;

int main() {
    int N;
    cin >> N;

    while (N--) {
        int start[1001];
        for (int i = 0; i <= 1000; i++) {
            start[i] = -1;
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
                start[id] = t;
            } else if (op == 'E') {
                if (start[id] != -1) {
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