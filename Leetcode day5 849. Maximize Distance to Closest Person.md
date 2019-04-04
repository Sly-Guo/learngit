#Leetcode day5 849. Maximize Distance to Closest Person




---
##Description
In a row of seats, 1 represents a person sitting in that seat, and 0 represents that the seat is empty. 

There is at least one empty seat, and at least one person sitting.

Alex wants to sit in the seat such that the distance between him and the closest person to him is maximized. 

Return that maximum distance to closest person.

* __A funny comment on this problem:__

> Let's just call this what it is, this has nothing to do with picking seats, this is the algorithm for picking a urinal in a public bathroom :D

---
##python3

```
class Solution:
    def maxDistToClosest(self, seats: List[int]) -> int:
         # left记载当前位置左边第一个1的位置
        # count进行0的计数
        # _max_distance维护最大距离返回值
        left, count, _max_distance = -1, 0, 1
        for i, x in enumerate(seats):
            if x == 0:
                count += 1
            else:
                if left < 0:
                    # 左边没有1最大距离就是count
                    distance = count
                else:
                    # 左边有1最大距离就是一半左右
                    # 奇数个0正好在中间
                    # 偶数个0要比一半小1
                    distance = count // 2 + count % 2
                # 重置左边第一个1的位置
                # 遇到1重新计数0的个数
                left, count = i, 0
                # 更新最大距离
                _max_distance = max(_max_distance, distance)
        # 末尾一连串0的情况也可能刷新最大距离
        return max(_max_distance, count)
```

* The other approach

__Briefly__ describe the idea of this approach;

1. Firstly,  using 'people' as the seat a person is sitting on. Here: `people = i for i,seat in enumerate(seats) if seat`.
2. Secondly, initializing prev and future as the last seat being used and the next seat being used. __Note__: each one of them can be None.
3. Thirdly, employ a 'for' circle. Iterate throufh the seats, set `prev =i ` and find the first people. Then update prev and future continuously.


```
class Solution:
    def maxDistToClosest(self, seats: List[int]) -> int:
        people = (i for i, seat in enumerate(seats) if seat)
        prev, future = None, next(people)
        
        ans = 0
        for i, seat in enumerate(seats):
            if seat:
                prev = i  #update prev
            else:
                while future is not None and future < i: # update future
                    future = next(people, None)
                
                left = float('inf') if prev is None else i - prev
                right = float('inf') if future is None else future -i 
                ans = max(ans, min(left,right))
        return ans    

```
---
##C++

* This C++ approach just follows the basic logic idea.
*

```
class Solution {
public:
    int maxDistToClosest(vector<int>& seats) {
        
        
        int prev = -1;
        int ans = 1;
        for (int i = 0; i<seats.size(); i++)
        {
            if (seats[i])
            {
                if (prev == -1)
                    ans = i;
                else if (ans < (i - prev)/2)
                    ans = (i - prev)/2;
                
                prev = i ;
            }
            
            
            
        }
        
        if (ans < seats.size() - prev - 1)
            ans = seats.size() - prev - 1;
        return ans;
    }
};

```