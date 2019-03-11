K-d Tree
---

K-d 树是有效寻找最近邻的优秀数据结构; 它也是一个二叉树, 其中每个节点都是 K 维点


Searching for a nearest neighbour in a k-d tree proceeds as follows:

1. Starting with the root node, the algorithm moves down the tree recursively, in the same way that it would if the search point were being inserted (i.e. it goes left or right depending on whether the point is lesser than or greater than the current node in the split dimension).

2. Once the algorithm reaches a leaf node, it saves that node point as the "current best"

3. The algorithm unwinds the recursion of the tree, performing the following steps at each node:

    1. If the current node is closer than the current best, then it becomes the current best.

    2. The algorithm checks whether there could be any points on the other side of the splitting plane that are closer to the search point than the current best. In concept, this is done by intersecting the splitting hyperplane with a hypersphere around the search point that has a radius equal to the current nearest distance. Since the hyperplanes are all axis-aligned this is implemented as a simple comparison to see whether the distance between the splitting coordinate of the search point and current node is lesser than the distance (overall coordinates) from the search point to the current best.

        1. If the hypersphere crosses the plane, there could be nearer points on the other side of the plane, so the algorithm must move down the other branch of the tree from the current node looking for closer points, following the same recursive process as the entire search.

        2. If the hypersphere doesn't intersect the splitting plane, then the algorithm continues walking up the tree, and the entire branch on the other side of that node is eliminated.

4. When the algorithm finishes this process for the root node, then the search is complete.