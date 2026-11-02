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
2.生成image.ppm:
编译找到路径
在cmd中逐行输入：
D:
cd 路径（直到release）
exe>image.ppm
3.用查看器打开