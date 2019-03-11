## 八皇后问题

解决方法: 回溯搜索 backtracking search: 回溯基于深度优先遍历, 每次选择一个 value, 如果不满足约束, 则回溯. 注意 backtracking search 只维护一个状态, 并不断修改这个状态, 而不是创建一个新的状态.


``` python

def search_eight_queens(size=8):
    states = [0] * size

    def conflicted(n):
        for i in range(n):
            if states[n] == states[i] or abs(n-i) == abs(states[n]-states[i]):
                return True
        return False

    depth = 1

    while 0 <= depth < size:
        # select un-assignment value
        while states[depth] < size and conflicted(depth):
            states[depth] += 1

        if states[depth] == size:
            # no legal values, backtracking
            states[depth] = 0; depth -= 1; states[depth] += 1
            continue

        if depth == size-1:  # complete
            display(states)
            # advance to next state
            states[depth] = 0; depth -= 1; states[depth] += 1
        else:
            depth += 1


def display(states, size=8):
    for s in states:
        print '. ' * s + '* ' + '. ' * (size -1 - s)
    print


if __name__ == '__main__':
    search_eight_queens()

```


## 汉诺塔

解决思路, 可以将圆盘为 n 问题, 递归的规约为对更少圆盘进行移动的同一个问题; 这是一种常见的计算模式, 称为树形递归;

树形递归计算过程通常极其低效, 但却非常直观, 容易理解...

``` python

def hannoi(a, b, c, n):
    """ 移动 n 个圆盘从 a 到 c
    """
    if n == 1:
        print 'move %s from %s to %s...' % (n, a, c)
        return

    hannoi(a, c, b, n-1)  # 将上面 n-1 个圆盘先从 a 移动到 b
    print 'move %s from %s to %s...' % (n, a, c)
    hannoi(b, a, c, n-1)  # 将 b 上的 n-1 个圆盘从 b 移动到 c
```
