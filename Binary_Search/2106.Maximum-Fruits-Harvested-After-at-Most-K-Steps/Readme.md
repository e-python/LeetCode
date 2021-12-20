### 2106.Maximum-Fruits-Harvested-After-at-Most-K-Steps

#### 解法1：双指针
首先我们要明确最优解的pattern，一定是往一个方向走x步到A，再返回起点（必然同样走了x步），再往另一个方向走y步到B。需要满足的约束是2x+y<=k. 注意，其中x不是必须的，可以为0.

我们不妨假设A和B分别在startPos的左边和右边。我们可以有这么一个发现：因为约束关系的存在，如果B点朝右变动，则A也不得不朝右变动。于是我们就有了滑动窗口的思想。我们从左往右尝试所有大于等于startPos的水果位置作为B，相应地为了满足约束，必然单调地从左往右单调移动A的位置，当使得恰好满足约束时AB的距离必然最远，能够得到的收获区间[A,B]也是最大的（在B点固定的情况下）。

注意这里有一个特殊的情况。当A点跨过了startPos时，A点的意义已经失效。这个时候我们需要检查x=0情况下，B点本身是否是一个可行解。即如果```pos[B]-startPos<=k```，那么此时双闭区间[A,B]内的val都是有效答案。

同理，我们在假设A和B分别在startPos的右边和左边。此时我们从右往左尝试所有小于等于startPos的水果位置作为B，相应地我们要把A从右往左单调地移动直至满足约束条件。此时[B,A]也是在固定B的情况下的最大收获区间。

这个解法是o(n)。

#### 解法2：二分搜值
将以上的解法稍微改动一下，确定了B点之后，我们对于A点的期望也就有了，可以直接在pos里二分。

假如B是在startPos的右边，那么我们就希望A是大于等于```startPos - (k-y)/2```的第一个位置。这样双闭区间[A,B]就是我们的最大收获。注意我们需要判定A是否合法。

同理假如B是在startPos的左边，那么我们就希望A是小于等于```startPos + (k-y)/2```的最后一个位置。这样双闭区间[B,A]就是我们的最大收获。同样我们需要判定A是否合法。