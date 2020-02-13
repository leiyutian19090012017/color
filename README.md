# color
颜色填充。编写函数，实现许多图片编辑软件都支持的“颜色填充”功能。给定一个屏幕（以二维数组表示，元素为颜色值）、一个点和一个新的颜色值，将新颜色值填入这个点的周围区域，直到原来的颜色值全都改变。

示例1:

 输入：
image = [[1,1,1],[1,1,0],[1,0,1]] 
sr = 1, sc = 1, newColor = 2
 输出：[[2,2,2],[2,2,0],[2,0,1]]
 解释: 
在图像的正中间，(坐标(sr,sc)=(1,1)),
在路径上所有符合条件的像素点的颜色都被更改成2。
注意，右下角的像素没有更改为2，
因为它不是在上下左右四个方向上与初始点相连的像素点。

说明：

    image 和 image[0] 的长度在范围 [1, 50] 内。
    给出的初始点将满足 0 <= sr < image.length 和 0 <= sc < image[0].length。
    image[i][j] 和 newColor 表示的颜色值在范围 [0, 65535]内。

class Solution {
    static constexpr int dirs[4][2] = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
public:
    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int newColor) {
        int color = image[sr][sc];
        if (color == newColor) {
            return image;
        }

        int m = image.size();    
        int n = image[0].size();
        queue<pair<int, int>> q;
        q.emplace(make_pair(sr, sc));
        while (!q.empty()) {
            int row = q.front().first;
            int col = q.front().second;
            q.pop();
            image[row][col] = newColor;
            for (auto& dir : dirs) {
                int rowT = row + dir[0];
                int colT = col + dir[1];
                if (rowT >= 0 && rowT < m && colT >= 0 && colT < n && image[rowT][colT] == color) {
                    q.emplace(make_pair(rowT, colT));
                }
            }
            
        }
        return image;
    }
};

