# **一：**
## 输出图像
1.
```
#include <iostream>
using namespace std;
int main() {

    // Image

    int image_width = 256;
    int image_height = 256;

    // Render

    cout << "P3\n" << image_width << ' ' << image_height << "\n255\n";

    for (int j = 0; j < image_height; j++) {
        for (int i = 0; i < image_width; i++) {
            auto r = double(i) / (image_width - 1);
            auto g = double(j) / (image_height - 1);
            auto b = 0.0;

            int ir = int(255.999 * r);
            int ig = int(255.999 * g);
            int ib = int(255.999 * b);

            cout << ir << ' ' << ig << ' ' << ib << '\n';
        }
    }
    return 0;
}
```
在这段代码中有一些需要注意的地方：

(1)像素按行写出。
(2)每一行的像素从左到右写出。
(3)这些行从上到下写出。
(4)按照惯例，每个红/绿/蓝分量在内部由取值范围为0.0到1.0的实值变量表示。在打印输出之前，必须将它们缩放为0到255之间的整数值。
红色从完全关闭（黑色）到完全打开（亮红色）从左到右变化，绿色从顶部完全关闭（黑色）到底部完全打开（亮绿色）变化。将红光和绿光相加会得到黄色，所以我们应该期望右下角是黄色的。

2.生成image.ppm:
编译找到路径
在cmd中逐行输入：
D:
cd 路径（直到release）
exe>image.ppm
3.用查看器打开

<img width="256" height="256" alt="Image" src="https://github.com/user-attachments/assets/7ba0cf8c-3122-4ad2-ab40-1acb9f167f29" />