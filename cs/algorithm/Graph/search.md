## Depth-First Search 深度优先
...




## Breath-First Search 广度优先
...



## [A* Search](https://en.wikipedia.org/wiki/A*_search_algorithm)

A* is an informed search algorithm, or a best-first search. It solves problems by searching among all possible paths to the solution(goal) for the one that incurs the smallest cost, and among these paths it first considers the ones that appear to lead most quickly to the solution.


``` python
import sys
import heapq
import time

from collections import defaultdict
from collections import namedtuple
from math import pow, sqrt


# consts used
Obstruction = '+'
Path_Mark = '@'

Point = namedtuple('Point', ('x', 'y'))


class Map(object):
    """ A simple N * N map
    """
    def __init__(self):
        self.pixel_map = []
        self.n = 0

    def load(self, content):
        print 'load map...'
        for line in content.split('\n'):
            if not line.strip(): continue
            row = [e for e in line.strip().split(' ')]
            self.pixel_map.append(row)
        # black magic
        self.n = len(row)
        print 'map size is %s * %s...' % (self.n, self.n)

    def display(self):
        print
        print '\n'.join(' '.join(e) for e in self.pixel_map)


def find_neighbors(target, map):
    x, y, n = target.x, target.y, map.n

    left, right = max(x-1, 0), min(x+1, n-1)
    up, bottom = max(y-1, 0), min(y+1, n-1)

    s = {
        Point(x0, y0)
        for x0 in range(left, right+1) for y0 in range(up, bottom+1)
        if map.pixel_map[y0][x0] != Obstruction
    }
    s.remove(target)
    return s


def dist_between(current, neighbor):
    return 1


def heuristic_cost_estimate(start, end):
    return sqrt(pow(start.x - end.x, 2) + pow(start.y - end.y, 2))


def a_star(start, goal, map):
    """ f(n) = g(n) + h(n)
    """
    heap_push, heap_pop = heapq.heappush, heapq.heappop

    # The set of nodes already evaluated
    closed_set = set()

    # The set of currently discovered nodes that are not evaluated yet.
    # Initially, only the start node is known.
    open_set = []

    # For each node, which node it can most efficiently be reached from.
    # If a node can be reached from many nodes, cameFrom will eventually contain the
    # most efficient previous step.
    came_from = dict()

    # For each node, the cost of getting from the start node to that node.
    g_score = defaultdict(lambda: sys.maxint)

    # The cost of going from start to start is zero.
    g_score[start] = 0

    # For each node, the total cost of getting from the start node to the goal
    # by passing by that node. That value is partly known, partly heuristic.
    f_score = defaultdict(lambda: sys.maxint)

    # For the first node, that value is completely heuristic.
    f_score[start] = heuristic_cost_estimate(start, goal)

    heap_push(open_set, (f_score[start], start))

    while open_set:
        # find the node in open_set having the lowest f_score[] value
        score, current = heap_pop(open_set)

        # if score != f_score[current]:  # TODO:
        #     print 'point {} heap score {} vs latest score {}'.format(current, score, f_score[current])

        if current == goal:
            return reconstruct_path(came_from, current)

        closed_set.add(current)

        for neighbor in find_neighbors(current, map):
            if neighbor in closed_set:
                continue  # Ignore the neighbor which is already evaluated.

            # Discover a new node
            is_new_node = neighbor not in set(e[1] for e in open_set)

            # The distance from start to a neighbor
            tentative_g_score = g_score[current] + dist_between(current, neighbor)
            if tentative_g_score >= g_score[neighbor]:
                if is_new_node:
                    heap_push(open_set, (f_score[neighbor], neighbor))
                continue  # This is not a better path.

            # This path is the best until now. Record it!
            came_from[neighbor] = current
            g_score[neighbor] = tentative_g_score
            f_score[neighbor] = tentative_g_score + heuristic_cost_estimate(neighbor, goal)

            if is_new_node:
                heap_push(open_set, (f_score[neighbor], neighbor))

    # Oops, we failed!
    return False


def reconstruct_path(came_from, current):
    total_path = [current]
    while current in came_from.keys():
        current = came_from[current]
        total_path.append(current)
    return total_path


def display(path, map):
    # mark the path
    for pt in path:
        assert map.pixel_map[pt.y][pt.x] != Obstruction, pt
        map.pixel_map[pt.y][pt.x] = Path_Mark
    map.display()


def main():
    x_map = Map()
    x_map.load(star_test_map)

    start = time.time()
    path = a_star(Point(1, 1), Point(28, 28), x_map)
    if not path:
        print 'Oops, fail to find a path!'
        return

    elapsed = time.time() - start
    print 'calc: elapsed time is %.3f seconds' % elapsed

    display(path, x_map)


star_test_map = '''
+ + + + + + + + + + + + + + + + + + + + + + + + + + + + + +
+ . . . . . . . . . . . . . . . . . . . . . . . . . . . . +
+ . . . . . . . . . . . . . . . . . . . . . . . . . . . . +
+ . . . . . . . . . . . . . . . . . . . . . . . . . . . . +
+ + + + + + . . + . . . . . . . . . . . . . . . . . . . . +
+ . . . . . . . + . . . . . . . . . . . . . . . . . . . . +
+ . . . . . . . + . . . . . . . . . . . . . . . . . . . . +
+ . . . + + + + + + + + + + + . . . . . . . . . . . . . . +
+ . . . + . . . + . . . . . . . . . . . . . . . . . . . . +
+ . . + + . . . + . . . . . . . . . . . . . . . . . . . . +
+ . . . . . . . + . . . . . . . . . . . . . . . . . . . . +
+ + + + . . . . + . . . . . . . . . . . . . . . . . . . . +
+ . . . . . . . + . . . . + + + + + + . . . . . . . . . . +
+ . . . . . . . + + + + . + . . . . + + . . . . . . . + . +
+ . . . . . . . . . . + + + . . . . . . . . . . . . . + . +
+ . . . . . . . . . . . . . . . . . . . . . . . . . . + . +
+ . . . . . . . . . . + + . . . + + + + + + + + + + + + + +
+ . . . . . . . . . . . + . . . . . . . . . . . . . . . . +
+ . . . . . . . . . . . + . + . . . . . . . . . . . . . . +
+ . . . . . . . . . . . + . + . . . . . . . . . . . . . . +
+ . . . . . . . . . . . + . + . . . . . . . . . . . . . . +
+ . . . . . . . . . . . + . + . . . . . . . . . . . . . . +
+ . . . . . . . . . . . + . + . . . . . . + + + . . . . . +
+ . . . . . . . . . . . + . + . . . . . . + + + . . . . . +
+ . . . . . . . . . . . + . + . . . . . . + + + . . . . . +
+ . . . . . . . . . . . + . + . . . . . . + + + . . . . . +
+ . . . . . . . . . . . . . . . . . . . . + + + . . . . . +
+ . . . . . . . . . . . + . + . . . . . . . + . . . . . . +
+ . . . . . . . . . . . + . + . . . . . . . . . . . . . . +
+ + + + + + + + + + + + + + + + + + + + + + + + + + + + + +
'''

if __name__ == '__main__':
    main()

```

The output as following shown
<pre>
load map...
map size is 30 * 30...
calc: elapsed time is 0.027 seconds

+ + + + + + + + + + + + + + + + + + + + + + + + + + + + + +
+ @ . . . . . . . . . . . . . . . . . . . . . . . . . . . +
+ . @ . . . . . . . . . . . . . . . . . . . . . . . . . . +
+ . . @ @ @ . . . . . . . . . . . . . . . . . . . . . . . +
+ + + + + + @ . + . . . . . . . . . . . . . . . . . . . . +
+ . . . . @ . . + . . . . . . . . . . . . . . . . . . . . +
+ . . . @ . . . + . . . . . . . . . . . . . . . . . . . . +
+ . . @ + + + + + + + + + + + . . . . . . . . . . . . . . +
+ . . @ + . . . + . . . . . . . . . . . . . . . . . . . . +
+ . @ + + . . . + . . . . . . . . . . . . . . . . . . . . +
+ . . @ . . . . + . . . . . . . . . . . . . . . . . . . . +
+ + + + @ . . . + . . . . . . . . . . . . . . . . . . . . +
+ . . . . @ . . + . . . . + + + + + + . . . . . . . . . . +
+ . . . . . @ . + + + + . + . . . . + + . . . . . . . + . +
+ . . . . . . @ . . . + + + . . . . . . . . . . . . . + . +
+ . . . . . . . @ . . @ @ . . . . . . . . . . . . . . + . +
+ . . . . . . . . @ @ + + @ . . + + + + + + + + + + + + + +
+ . . . . . . . . . . . + . @ . . . . . . . . . . . . . . +
+ . . . . . . . . . . . + . + @ . . . . . . . . . . . . . +
+ . . . . . . . . . . . + . + . @ . . . . . . . . . . . . +
+ . . . . . . . . . . . + . + . . @ . . . . . . . . . . . +
+ . . . . . . . . . . . + . + . . . @ . . . . . . . . . . +
+ . . . . . . . . . . . + . + . . . . @ . + + + . . . . . +
+ . . . . . . . . . . . + . + . . . . . @ + + + . . . . . +
+ . . . . . . . . . . . + . + . . . . . @ + + + . . . . . +
+ . . . . . . . . . . . + . + . . . . . @ + + + . . . . . +
+ . . . . . . . . . . . . . . . . . . . @ + + + . . . . . +
+ . . . . . . . . . . . + . + . . . . . . @ + . . . . . . +
+ . . . . . . . . . . . + . + . . . . . . . @ @ @ @ @ @ @ +
+ + + + + + + + + + + + + + + + + + + + + + + + + + + + + +
</pre>