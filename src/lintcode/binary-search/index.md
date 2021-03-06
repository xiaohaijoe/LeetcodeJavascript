## 索引

- <a href="#14">14. 二分查找（简单）</a>
- <a href="#457">457. 经典二分查找问题（简单）</a>
- <a href="#458">458. 目标最后位置（简单）</a>
- <a href="#74">74. 第一个错误的代码版本（中等）</a>
- <a href="#447">447. 在大数组中查找（中等）</a>
- <a href="#159">159. 寻找旋转排序数组中的最小值（中等）</a>
- <a href="#28">28. 搜索二维矩阵（中等）</a>
- <a href="#61">61. 搜索区间（中等）</a>
- <a href="#585">585. 山脉序列中的最大值（中等）</a>
- <a href="#62">62. 搜索旋转排序数组（中等）</a>
- <a href="#75">75. 寻找峰值（中等）</a>
- <a href="#937">937. 可以完成的题目数量（中等）</a>

## 二分查找模板

**二分法模板的四点要素**

- start + 1 < end
- start + (end - start) / 2
- A[mid] ==, <, >
- A[start] A[end] ? target

**三个境界**

- 二分法模板
- OOXX
- Half half

```javascript
  binarySearch(nums, target) {
    if (!nums || nums.length === 0) {
      return -1;
    }

    let start = 0,
      end = nums.length - 1;
    let mid = 0;
    while (start + 1 < end) { // 结束条件
      mid = start + parseInt((end - start) / 2); // 中间切两刀
      if (nums[mid] === target) {
        end = mid;
      } else if (nums[mid] > target) {
        end = mid;
      } else {
        start = mid;
      }
    }

    if (nums[start] === target) {
      return start;
    }
    if (nums[end] === target) {
      return end;
    }
    return -1;
  }
```

## <a name='457'>457. 经典二分查找问题

**[链接](http://www.lintcode.com/problem/classical-binary-search/)**

**描述**
在一个排序数组中找一个数，返回该数出现的任意位置，如果不存在，返回 -1。

**样例**
样例 1：

```
输入：nums = [1,2,2,4,5,5], target = 2
输出：1 或者 2
```

样例 2：

```
输入：nums = [1,2,2,4,5,5], target = 6
输出：-1
```

**挑战**
O(logn) 的时间

```javascript
class Solution457 {
  binarySearch(nums, target) {
    if (!nums || nums.length === 0) {
      return -1;
    }

    let start = 0,
      end = nums.length - 1;
    let mid = 0;
    while (start + 1 < end) {
      mid = start + parseInt((end - start) / 2);
      if (nums[mid] === target) {
        return mid;
      } else if (nums[mid] > target) {
        end = mid;
      } else {
        start = mid;
      }
    }

    if (nums[start] === target) {
      return start;
    }
    if (nums[end] === target) {
      return end;
    }
    return -1;
  }
}
```

## <a name='14'>14. 二分查找

**[链接](https://www.lintcode.com/problem/first-position-of-target/)**

**描述**
给定一个排序的整数数组（升序）和一个要查找的整数 target，用 O(logn)的时间查找到 target 第一次出现的下标（从 0 开始），如果 target 不存在于数组中，返回-1。

**样例**

```
样例  1:
	输入:[1,4,4,5,7,7,8,9,9,10]，1
	输出: 0

	样例解释:
	第一次出现在第0个位置。

样例 2:
	输入: [1, 2, 3, 3, 4, 5, 10]，3
	输出: 2

	样例解释:
	第一次出现在第2个位置

样例 3:
	输入: [1, 2, 3, 3, 4, 5, 10]，6
	输出: -1

	样例解释:
	没有出现过6， 返回-1
```

**挑战**
如果数组中的整数个数超过了 2^32，你的算法是否会出错？

## <a name='458'>458. 目标最后位置

**[链接](https://www.lintcode.com/problem/458)**

**描述**
给一个升序数组，找到 target 最后一次出现的位置，如果没出现过返回 -1

**样例**

```
样例 1：

输入：nums = [1,2,2,4,5,5], target = 2
输出：2
样例 2：

输入：nums = [1,2,2,4,5,5], target = 6
输出：-1
```

```javascript
export class Solution {
  /**
   * lastPosition
   *
   * @param nums: An integer array sorted in ascending order
   * @param target: An integer
   * @return: An integer
   */
  lastPosition(nums, target) {
    // write your code here
    if (!nums || nums.length === 0) {
      return -1;
    }

    let start = 0,
      end = nums.length - 1;
    let mid = 0;
    while (start + 1 < end) {
      mid = start + parseInt((end - start) / 2);

      if (nums[mid] === target) {
        start = mid;
      } else if (nums[mid] > target) {
        end = mid;
      } else {
        start = mid;
      }
    }

    if (nums[end] === target) {
      return end;
    }
    if (nums[start] === target) {
      return start;
    }
    return -1;
  }
}
```

## <a name='74'>74. 第一个错误的代码版本（中等）

**[链接](https://www.lintcode.com/problem/first-bad-version/)**

**描述**
代码库的版本号是从 1 到 n 的整数。某一天，有人提交了错误版本的代码，因此造成自身及之后版本的代码在单元测试中均出错。请找出第一个错误的版本号。
<br>
你可以通过 isBadVersion 的接口来判断版本号 version 是否在单元测试中出错，具体接口详情和调用方法请见代码的注释部分。

**样例**

```
n = 5:

    isBadVersion(3) -> false
    isBadVersion(5) -> true
    isBadVersion(4) -> true

因此可以确定第四个版本是第一个错误版本。
```

```javascript
class Solution74 {
  /**
   * findFirstBadVersion
   *
   * @param n: An integer
   * @return: An integer which is the first bad version.
   */
  findFirstBadVersion(n) {
    // write your code here
    let start = 1,
      end = n;
    let mid = 1;

    while (start + 1 < end) {
      mid = start + parseInt((end - start) / 2);

      if (isBadVersion(mid) === true) {
        end = mid;
      } else {
        start = mid;
      }
    }

    if (isBadVersion(start)) {
      return start;
    }
    return end;
  }
}
```

## <a name='447'>447. 在大数组中查找（中等）

**[链接](https://www.lintcode.com/problem/search-in-a-big-sorted-array/)**

**描述**
给一个按照升序排序的非负整数数组。这个数组很大以至于你只能通过固定的接口 ArrayReader.get(k) 来访问第 k 个数(或者 C++里是 ArrayReader->get(k))，并且你也没有办法得知这个数组有多大。
<br>
找到给出的整数 target 第一次出现的位置。你的算法需要在 O(logk)的时间复杂度内完成，k 为 target 第一次出现的位置的下标。
<br>
如果找不到 target，返回-1。

**样例**

```
样例 1:

输入: [1, 3, 6, 9, 21, ...], target = 3
输出: 1
样例 2:

输入: [1, 3, 6, 9, 21, ...], target = 4
输出: -1
```

```javascript
export class Solution447 {
  /**
   * searchBigSortedArray
   *
   * @param reader: An instance of ArrayReader.
   * @param target: An integer
   * @return: An integer which is the first index of target.
   */
  searchBigSortedArray(reader, target) {
    // write your code here
    let start = 0,
      end = 10;
    let mid = 0;

    while (reader.get(end) < target && reader.get(end) !== 2147483647) {
      start = end;
      end *= 2;
    }

    while (start + 1 < end) {
      mid = start + parseInt((end - start) / 2);

      if (reader.get(mid) === target) {
        end = mid;
      } else if (reader.get(mid) > target) {
        end = mid;
      } else {
        start = mid;
      }
    }

    if (reader.get(start) === target) {
      return start;
    }
    if (reader.get(end) === target) {
      return end;
    }
    return -1;
  }
}
```

## <a name='159'>159. 寻找旋转排序数组中的最小值（中等）

**[链接](https://www.lintcode.com/problem/find-minimum-in-rotated-sorted-array/)**

**描述**
假设一个排好序的数组在其某一未知点发生了旋转（比如 0 1 2 4 5 6 7 可能变成 4 5 6 7 0 1 2）。你需要找到其中最小的元素。

**样例**

```
样例 1:

输入：[4, 5, 6, 7, 0, 1, 2]
输出：0
解释：
数组中的最小值为0
样例 2:

输入：[2,1]
输出：1
解释：
数组中的最小值为1
```

```javascript
export class Solution159 {
  /**
   * findMin
   *
   * @param nums: a rotated sorted array
   * @return: the minimum number in the array
   */
  findMin(nums) {
    // write your code here
    let start = 0,
      end = nums.length - 1;
    let mid = 0;

    while (start + 1 < end) {
      mid = start + parseInt((end - start) / 2);

      if (nums[mid] > nums[end]) {
        start = mid;
      } else {
        end = mid;
      }
    }

    if (nums[end] > nums[start]) {
      return nums[start];
    } else {
      return nums[end];
    }
  }
}
```

## <a name='28'>28. 搜索二维矩阵（中等）

**[链接](https://www.lintcode.com/problem/search-a-2d-matrix/)**

**描述**
写出一个高效的算法来搜索 m × n 矩阵中的值。
<br>
这个矩阵具有以下特性：
<br>

- 每行中的整数从左到右是排序的。
- 每行的第一个数大于上一行的最后一个整数。

**样例**

```
样例  1:
	输入: [[5]],2
	输出: false

	样例解释:
  没有包含，返回false。

样例 2:
	输入:
[
  [1, 3, 5, 7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
],3
	输出: true

	样例解释:
	包含则返回true。
```

**笔记**

将 2D Matrix 进行两次二分查找，第一次找出具体的行下标，第二次找出该行具体的下标

```javascript
class Solution28 {
  /**
   * searchMatrix
   *
   * @param matrix: matrix, a list of lists of integers
   * @param target: An integer
   * @return: a boolean, indicate whether matrix contains target
   */
  searchMatrix(matrix, target) {
    // write your code here
    if (!matrix || matrix.length === 0) {
      return false;
    }
    let start = 0,
      end = matrix.length - 1;
    let mid = 0;
    while (start + 1 < end) {
      mid = start + parseInt((end - start) / 2);

      const midLastIndex = matrix[mid].length - 1;
      if (matrix[mid][midLastIndex] > target) {
        end = mid;
      } else {
        start = mid;
      }
    }

    const startLastIndex = matrix[start].length - 1;
    const endLastIndex = matrix[end].length - 1;
    let targetIndex = -1;
    if (matrix[start][0] <= target && matrix[start][startLastIndex] >= target) {
      targetIndex = start;
    }
    if (matrix[end][0] <= target && matrix[end][endLastIndex] >= target) {
      targetIndex = end;
    }

    if (targetIndex < 0) {
      return false;
    }

    start = 0;
    end = matrix[targetIndex].length - 1;
    while (start + 1 < end) {
      mid = start + parseInt((end - start) / 2);

      if (matrix[targetIndex][mid] == target) {
        // end = mid;
        return true;
      } else if (matrix[targetIndex][mid] > target) {
        end = mid;
      } else {
        start = mid;
      }
    }

    if (matrix[targetIndex][start] === target) {
      return true;
    }
    if (matrix[targetIndex][end] === target) {
      return true;
    }
    return false;
  }
}
```

## <a name='61'>61. 搜索区间（中等）

**[链接](https://www.lintcode.com/problem/search-for-a-range/)**

**描述**
给定一个包含 n 个整数的排序数组，找出给定目标值 target 的起始和结束位置。
<br>
如果目标值不在数组中，则返回[-1, -1]

**样例**

```
例1:

输入:
[]
9
输出:
[-1,-1]

例2:

输入:
[5, 7, 7, 8, 8, 10]
8
输出:
[3, 4]
```

```javascript
class Solution61 {
  /**
   * searchRange
   *
   * @param A: an integer sorted array
   * @param target: an integer to be inserted
   * @return: a list of length 2, [index1, index2]
   */
  searchRange(A, target) {
    // write your code here
    if (!A || A.length === 0) {
      return [-1, -1];
    }
    let start = 0,
      end = A.length - 1;
    let mid = 0;

    while (start + 1 < end) {
      mid = start + parseInt((end - start) / 2);

      if (A[mid] === target) {
        let left = mid;
        let right = mid;
        while (left >= start || right <= end) {
          if (A[left] === target) {
            left--;
          }
          if (A[right] === target) {
            right++;
          }
          if (A[left] !== target && A[right] !== target) {
            break;
          }
        }
        start = left + 1;
        end = right - 1;
        return [start, end];
      } else if (A[mid] > target) {
        end = mid;
      } else {
        start = mid;
      }
    }

    if (A[start] === target) {
      return [start, start];
    }
    if (A[end] === target) {
      return [end, end];
    }
    return [-1, -1];
  }
}
```

## <a name='585'>585. 山脉序列中的最大值（中等）

**[链接](https://www.lintcode.com/problem/maximum-number-in-mountain-sequence/)**

**描述**
给 n 个整数的山脉数组，即先增后减的序列，找到山顶（最大值）。

**样例**

```
例1:

输入: nums = [1, 2, 4, 8, 6, 3]
输出: 8
例2:

输入: nums = [10, 9, 8, 7],
输出: 10
```

```javascript
class Solution585 {
  /**
   * mountainSequence
   *
   * @param nums: a mountain sequence which increase firstly and then decrease
   * @return: then mountain top
   */
  mountainSequence(nums) {
    // write your code here
    let start = 0,
      end = nums.length - 1;
    let mid = 0;

    while (start + 1 < end) {
      mid = start + parseInt((end - start) / 2);

      if (nums[mid] > nums[mid - 1] && nums[mid] > nums[mid + 1]) {
        return nums[mid];
      } else if (nums[mid] > nums[mid - 1] && nums[mid] < nums[mid + 1]) {
        start = mid;
      } else {
        end = mid;
      }
    }

    if (nums[start] > nums[end]) {
      return nums[start];
    } else {
      return nums[end];
    }
  }
}
```

## <a name='62'>62. 搜索旋转排序数组（中等）

**[链接](https://www.lintcode.com/problem/search-in-rotated-sorted-array/)**

**描述**
假设有一个排序的按未知的旋转轴旋转的数组(比如，0 1 2 4 5 6 7 可能成为 4 5 6 7 0 1 2)。
<br>
给定一个目标值进行搜索，如果在数组中找到目标值返回数组中的索引位置，否则返回-1。你可以假设数组中不存在重复的元素。

**样例**

```
例1:

输入: [4, 5, 1, 2, 3] and target=1,
输出: 2.
例2:

输入: [4, 5, 1, 2, 3] and target=0,
输出: -1.
```

```javascript
class Solution62 {
  /**
   * search
   *
   * @param A: an integer rotated sorted array
   * @param target: an integer to be searched
   * @return: an integer
   */
  search(A, target) {
    // write your code here
    if (!A || A.length === 0) {
      return -1;
    }
    let start = 0,
      end = A.length - 1;
    let mid = 0;
    while (start + 1 < end) {
      mid = start + parseInt((end - start) / 2);

      if (A[mid] === target) {
        return mid;
      } else if (A[mid] > target) {
        if (A[mid] > A[end] && target <= A[end]) {
          start = mid;
        } else {
          end = mid;
        }
      } else {
        if (A[mid] <= A[end] && target <= A[end]) {
          start = mid;
        } else {
          end = mid;
        }
      }
    }

    if (A[end] === target) {
      return end;
    }
    if (A[start] === target) {
      return start;
    }
    return -1;
  }
}
```

## <a name='75'>75. 寻找峰值（中等）

**[链接](https://www.lintcode.com/problem/find-peak-element/)**

**描述**
你给出一个整数数组(size 为 n)，其具有以下特点：

- 相邻位置的数字是不同的
- A[0] < A[1] 并且 A[n - 2] > A[n - 1]

假定 P 是峰值的位置则满足 A[P] > A[P-1]且 A[P] > A[P+1]，返回数组中任意一个峰值的位置。

**样例**

```
样例 1:
	输入:  [1, 2, 1, 3, 4, 5, 7, 6]
	输出:  1 or 6

	解释:
	返回峰顶元素的下标


样例 2:
	输入: [1,2,3,4,1]
	输出:  3
```

```javascript
class Solution75 {
  /**
   * findPeak
   *
   * @param A: An integers array.
   * @return: return any of peek positions.
   */
  findPeak(A) {
    // write your code here
    if (!A || A.length === 0) {
      return 0;
    }

    let start = 0,
      end = A.length - 1;
    let mid = 0;
    while (start + 1 < end) {
      mid = start + parseInt((end - start) / 2);

      if (A[mid] > A[mid - 1] && A[mid] > A[mid + 1]) {
        return mid;
      } else if (A[mid] > A[mid - 1] && A[mid] < A[mid + 1]) {
        start = mid;
      } else {
        end = mid;
      }
    }
    if (A[start] > A[end]) {
      return start;
    } else {
      return end;
    }
  }
}
```

## <a name='937'>937. 可以完成的题目数量（中等）

**[链接](https://www.lintcode.com/problem/937/)**

**描述**
给定一个正整数 n，表示一场比赛的时间，比赛中题目的难度是递增的，你每完成一个题目，就要花费 k × i 的时间，其中 k 是输入的一个系数，i 表示题目的序号(从 1 开始)。

根据这些信息，返回这场比赛中，你最多能完成几个题目。

**样例**

```
样例1

输入: n = 30 和 k = 1
输出: 7
解释:
因为 1 * 1 + 1 * 2 + 1 * 3 + 1 * 4 + 1 * 5 + 1 * 6 + 1 * 7 = 28 < 30
且   1 * 1 + 1 * 2 + 1 * 3 + 1 * 4 + 1 * 5 + 1 * 6 + 1 * 7 + 1 * 8 = 36 > 30
样例2

输入: n = 31, k = 2
输出: 5
解释:
因为 2 * 1 + 2 * 2 + 2 * 3 + 2 * 4 + 2 * 5 = 30 < 31 且 2 * 1 + 2 * 2 + 2 * 3 + 2 * 4 + 2 * 5 + 2 * 6 = 42 > 31

```

```javascript
public class Solution {
    /**
     * @param n: an integer
     * @param k: an integer
     * @return: how many problem can you accept
     */
    public long canAccept(long n, int k) {
        // Write your code here
        if(n < k) {
          return 0;
        }

        double start = 0;
        double end = n;
        double sum = n / k;
        // double total = 0;
        while(start + 1 < end) {
          double mid = Math.floor(start + (end-start)/2);

          double total = (1+mid)* mid/2;
          if(total == sum) {
            return (long)mid;
          } else if(total < sum) {
            start = mid;
          } else {
            end = mid;
          }
        }

        double endTotal = (1+end)*end /2;
        if(endTotal <= sum) {
          return (long)end;
        }
        return (long)start;
    }

}
```
