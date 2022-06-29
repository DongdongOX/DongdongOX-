## 数组

#### 704. 二分查找

给定一个 `n` 个元素有序的（升序）整型数组 `nums` 和一个目标值 `target` ，写一个函数搜索 `nums` 中的 `target`，如果目标值存在返回下标，否则返回 `-1`。


**示例 1:**

```
输入: nums = [-1,0,3,5,9,12], target = 9
输出: 4
解释: 9 出现在 nums 中并且下标为 4
```

**示例 2:**

```
输入: nums = [-1,0,3,5,9,12], target = 2
输出: -1
解释: 2 不存在 nums 中因此返回 -1
```

```c++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left=0;
        int right=nums.size()-1;
        while(left<=right){
            int mid=(left+right)/2;
            if(nums[mid]<target){
                left=mid+1;
            }
            else if(nums[mid]>target){
                right=mid-1;
            }
            else{
                return mid;
            }
        }
        return -1;
    }
};
```

####  35.搜索插入位置

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

请必须使用时间复杂度为 `O(log n)` 的算法。

 

**示例 1:**

```
输入: nums = [1,3,5,6], target = 5
输出: 2
```

**示例 2:**

```
输入: nums = [1,3,5,6], target = 2
输出: 1
```

**示例 3:**

```
输入: nums = [1,3,5,6], target = 7
输出: 4
```

**示例 4:**

```
输入: nums = [1,3,5,6], target = 0
输出: 0
```

**示例 5:**

```
输入: nums = [1], target = 0
输出: 0
```

```c++
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int left=0;
        int right=nums.size()-1;
        while(left<=right){
            int mid=(left+right)/2;
            if(nums[mid]<target){
                left=mid+1;
            }
            else if(nums[mid]>target){
                right=mid-1;
            }
            else{
                return mid;
            }
        }
        return left;
    }
};
```

#### 34.在排序数组中查找元素的第一个和最后一个位置

给定一个按照升序排列的整数数组 `nums`，和一个目标值 `target`。找出给定目标值在数组中的开始位置和结束位置。

如果数组中不存在目标值 `target`，返回 `[-1, -1]`。

**进阶：**

- 你可以设计并实现时间复杂度为 `O(log n)` 的算法解决此问题吗？

 

**示例 1：**

```
输入：nums = [5,7,7,8,8,10], target = 8
输出：[3,4]
```

**示例 2：**

```
输入：nums = [5,7,7,8,8,10], target = 6
输出：[-1,-1]
```

**示例 3：**

```
输入：nums = [], target = 0
输出：[-1,-1]
```

```c++
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        if(nums.size()==0){
            return {-1,-1};
        }
        int left=0;
        int right=nums.size()-1;
        while(left<right){
            int mid=(left+right)/2;
            if(nums[mid]>=target){
                right=mid;
            }
            else{
                left=mid+1;
            }
        }
        int lf=right;
        if(nums[right]!=target){
            return {-1,-1};
        }
        left=0;
        right=nums.size()-1;
        while(left<right){
            int mid=(left+right+1)/2;
            if(nums[mid]<=target){
                left=mid;
            }
            else{
                right=mid-1;
            }
        }
        return {lf,right};
    }
};
```

#### 69. x 的平方根

给你一个非负整数 `x` ，计算并返回 `x` 的 **算术平方根** 。

由于返回类型是整数，结果只保留 **整数部分** ，小数部分将被 **舍去 。**

**注意：**不允许使用任何内置指数函数和算符，例如 `pow(x, 0.5)` 或者 `x ** 0.5` 。

 

**示例 1：**

```
输入：x = 4
输出：2
```

**示例 2：**

```
输入：x = 8
输出：2
解释：8 的算术平方根是 2.82842..., 由于返回类型是整数，小数部分将被舍去。
```

```c++
class Solution {
public:
    int mySqrt(int x) {
        int left=0;
        int right=x;
        while(left<=right){
            int mid=(left+right)/2;
            if((long long)mid*mid<x){
                left=mid+1;
            }
            else if((long long)mid*mid>x){
                right=mid-1;
            }
            else{
                return mid;
            }
        }
        return right;
    }
};
```

#### 268. 丢失的数字

给定一个包含 `[0, n]` 中 `n` 个数的数组 `nums` ，找出 `[0, n]` 这个范围内没有出现在数组中的那个数。



 

**示例 1：**

```
输入：nums = [3,0,1]
输出：2
解释：n = 3，因为有 3 个数字，所以所有的数字都在范围 [0,3] 内。2 是丢失的数字，因为它没有出现在 nums 中。
```

**示例 2：**

```
输入：nums = [0,1]
输出：2
解释：n = 2，因为有 2 个数字，所以所有的数字都在范围 [0,2] 内。2 是丢失的数字，因为它没有出现在 nums 中。
```

**示例 3：**

```
输入：nums = [9,6,4,2,3,5,7,0,1]
输出：8
解释：n = 9，因为有 9 个数字，所以所有的数字都在范围 [0,9] 内。8 是丢失的数字，因为它没有出现在 nums 中。
```

**示例 4：**

```
输入：nums = [0]
输出：1
解释：n = 1，因为有 1 个数字，所以所有的数字都在范围 [0,1] 内。1 是丢失的数字，因为它没有出现在 nums 中。
```

```c++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        int left=0;
        int right=nums.size()-1;
        while(left<=right){
            int mid=(left+right)/2;
            if(nums[mid]!=mid){
                right=mid-1;
            }
            else{
                left=mid+1;
            }
        }
        return left;
    }
};
```



#### 367.有效的完全平方数

给定一个 **正整数** `num` ，编写一个函数，如果 `num` 是一个完全平方数，则返回 `true` ，否则返回 `false` 。

**进阶：不要** 使用任何内置的库函数，如 `sqrt` 。

 

**示例 1：**

```
输入：num = 16
输出：true
```

**示例 2：**

```
输入：num = 14
输出：false
```

```c++
lass Solution {
public:
    bool isPerfectSquare(int num) {
        int left=0;
        int right=num;
        while(left<=right){
            int mid=(left+right)/2;
            if((long long)mid*mid<num){
                left=mid+1;
            }
            else if((long long)mid*mid>num){
                right=mid-1;
            }
            else{
                return true;
            }
        }
        return false;
    }
};
```

#### 27. 移除元素

给你一个数组 `nums` 和一个值 `val`，你需要 **[原地](https://baike.baidu.com/item/原地算法)** 移除所有数值等于 `val` 的元素，并返回移除后数组的新长度。

不要使用额外的数组空间，你必须仅使用 `O(1)` 额外空间并 **[原地 ](https://baike.baidu.com/item/原地算法)修改输入数组**。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

 

**说明:**

为什么返回数值是整数，但输出的答案是数组呢?

请注意，输入数组是以**「引用」**方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

你可以想象内部操作如下:

```
// nums 是以“引用”方式传递的。也就是说，不对实参作任何拷贝
int len = removeElement(nums, val);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中 该长度范围内 的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

 

**示例 1：**

```
输入：nums = [3,2,2,3], val = 3
输出：2, nums = [2,2]
解释：函数应该返回新的长度 2, 并且 nums 中的前两个元素均为 2。你不需要考虑数组中超出新长度后面的元素。例如，函数返回的新长度为 2 ，而 nums = [2,2,3,3] 或 nums = [2,2,0,0]，也会被视作正确答案。
```

**示例 2：**

```
输入：nums = [0,1,2,2,3,0,4,2], val = 2
输出：5, nums = [0,1,4,0,3]
解释：函数应该返回新的长度 5, 并且 nums 中的前五个元素为 0, 1, 3, 0, 4。注意这五个元素可为任意顺序。你不需要考虑数组中超出新长度后面的元素。
```

```c++
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int slow=0;
        for(int i=0;i<nums.size();i++){
            if(nums[i]!=val){
                nums[slow++]=nums[i];
            }
        }
        return slow;
    }
};
```

#### 26.删除排序数组中的重复项

给你一个有序数组 `nums` ，请你**[ 原地](http://baike.baidu.com/item/原地算法)** 删除重复出现的元素，使每个元素 **只出现一次** ，返回删除后数组的新长度。

不要使用额外的数组空间，你必须在 **[原地 ](https://baike.baidu.com/item/原地算法)修改输入数组** 并在使用 O(1) 额外空间的条件下完成。

 

**说明:**

为什么返回数值是整数，但输出的答案是数组呢?

请注意，输入数组是以**「引用」**方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

你可以想象内部操作如下:

```
// nums 是以“引用”方式传递的。也就是说，不对实参做任何拷贝
int len = removeDuplicates(nums);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中 该长度范围内 的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

**示例 1：**

```
输入：nums = [1,1,2]
输出：2, nums = [1,2]
解释：函数应该返回新的长度 2 ，并且原数组 nums 的前两个元素被修改为 1, 2 。不需要考虑数组中超出新长度后面的元素。
```

**示例 2：**

```
输入：nums = [0,0,1,1,1,2,2,3,3,4]
输出：5, nums = [0,1,2,3,4]
解释：函数应该返回新的长度 5 ， 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4 。不需要考虑数组中超出新长度后面的元素。
```

```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if(nums.size()==0){
            return 0;
        }
        int ans=1;
        for(int i=1;i<nums.size();i++){
            if(nums[i]!=nums[i-1]){
                nums[ans++]=nums[i];
            }
        }
        return ans;
    }
};
```

#### 283.移动零

给定一个数组 `nums`，编写一个函数将所有 `0` 移动到数组的末尾，同时保持非零元素的相对顺序。

**示例:**

```
输入: [0,1,0,3,12]
输出: [1,3,12,0,0]
```

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int slow=0;
        for(int i=0;i<nums.size();i++){
            if(nums[i]!=0){
                swap(nums[slow++],nums[i]);
            }
        }
    }
};
```

#### 844.比较含退格的字符串

给定 `s` 和 `t` 两个字符串，当它们分别被输入到空白的文本编辑器后，请你判断二者是否相等。`#` 代表退格字符。

如果相等，返回 `true` ；否则，返回 `false` 。

**注意：**如果对空文本输入退格字符，文本继续为空。

 

**示例 1：**

```
输入：s = "ab#c", t = "ad#c"
输出：true
解释：S 和 T 都会变成 “ac”。
```

**示例 2：**

```
输入：s = "ab##", t = "c#d#"
输出：true
解释：s 和 t 都会变成 “”。
```

**示例 3：**

```
输入：s = "a##c", t = "#a#c"
输出：true
解释：s 和 t 都会变成 “c”。
```

**示例 4：**

```
输入：s = "a#c", t = "b"
输出：false
解释：s 会变成 “c”，但 t 仍然是 “b”。
```

```c++
class Solution {
public:
    vector<int>func(string s){
        vector<int>v;
        for(auto ch:s){
            if(ch!='#'){
                v.push_back(ch);
            }
            else{
                if(v.size()!=0){
                    v.pop_back();
                }
            }
        }
        return v;
    }
    bool backspaceCompare(string s, string t) {
        if(func(s)==func(t)){
            return true;
        }
        return false;
    }
};
```

#### 977.有序数组的平方

给你一个按 **非递减顺序** 排序的整数数组 `nums`，返回 **每个数字的平方** 组成的新数组，要求也按 **非递减顺序** 排序。

**示例 1：**

```
输入：nums = [-4,-1,0,3,10]
输出：[0,1,9,16,100]
解释：平方后，数组变为 [16,1,0,9,100]
排序后，数组变为 [0,1,9,16,100]
```

**示例 2：**

```
输入：nums = [-7,-3,2,3,11]
输出：[4,9,9,49,121]
```

```c++
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        int left=0;
        int right=nums.size()-1;
        vector<int>ans(nums.size(),0);
        int count=nums.size()-1;
        while(left<=right){
            if((long long)nums[left]*nums[left]<=(long long)nums[right]*nums[right]){
                ans[count--]=nums[right]*nums[right];
                right--;
            }
            else{
                ans[count--]=nums[left]*nums[left];
                left++;
            }
        }
        return ans;
    }
};
```

#### 209.长度最小的子数组

给定一个含有 `n` 个正整数的数组和一个正整数 `target` **。**

找出该数组中满足其和 `≥ target` 的长度最小的 **连续子数组** `[numsl, numsl+1, ..., numsr-1, numsr]` ，并返回其长度**。**如果不存在符合条件的子数组，返回 `0` 。

 

**示例 1：**

```
输入：target = 7, nums = [2,3,1,2,4,3]
输出：2
解释：子数组 [4,3] 是该条件下的长度最小的子数组。
```

**示例 2：**

```
输入：target = 4, nums = [1,4,4]
输出：1
```

**示例 3：**

```
输入：target = 11, nums = [1,1,1,1,1,1,1,1]
输出：0
```

```c++
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int left=0;
        int sum=0;
        int ans=INT_MAX;
        for(int i=0;i<nums.size();i++){
            sum+=nums[i];
            while(sum>=target){
                ans=min(ans,i-left+1);
                sum-=nums[left];
                left++;
            }
            
        }
        return ans==INT_MAX?0:ans;
    }
};
```

#### 904.水果成篮

你正在探访一家农场，农场从左到右种植了一排果树。这些树用一个整数数组 `fruits` 表示，其中 `fruits[i]` 是第 `i` 棵树上的水果 **种类** 。

你想要尽可能多地收集水果。然而，农场的主人设定了一些严格的规矩，你必须按照要求采摘水果：

- 你只有 **两个** 篮子，并且每个篮子只能装 **单一类型** 的水果。每个篮子能够装的水果总量没有限制。
- 你可以选择任意一棵树开始采摘，你必须从 **每棵** 树（包括开始采摘的树）上 **恰好摘一个水果** 。采摘的水果应当符合篮子中的水果类型。每采摘一次，你将会向右移动到下一棵树，并继续采摘。
- 一旦你走到某棵树前，但水果不符合篮子的水果类型，那么就必须停止采摘。

给你一个整数数组 `fruits` ，返回你可以收集的水果的 **最大** 数目。

**示例 1：**

```c++
输入：fruits = [1,2,1]
输出：3
解释：可以采摘全部 3 棵树。
```

**示例 2：**

```c++
输入：fruits = [0,1,2,2]
输出：3
解释：可以采摘 [1,2,2] 这三棵树。
如果从第一棵树开始采摘，则只能采摘 [0,1] 这两棵树。
```

**示例 3：**

```c++
输入：fruits = [1,2,3,2,2]
输出：4
解释：可以采摘 [2,3,2,2] 这四棵树。
如果从第一棵树开始采摘，则只能采摘 [1,2] 这两棵树。
```

```c++
class Solution {
public:
    int totalFruit(vector<int>& fruits) {
        if(fruits.size()==0){
            return 0;
        }
        int left=0;
        int ans=INT_MIN;
        unordered_map<int,int>hashtable;
        for(int i=0;i<fruits.size();i++){
            hashtable[fruits[i]]++;
            while(hashtable.size()>2){
                hashtable[fruits[left]]--;
                if(hashtable[fruits[left]]==0){
                    hashtable.erase(fruits[left]);
                }
                left++;
            }
            ans=max(ans,i-left+1);
        }
        return ans;
    }
};
```

#### 76.最小覆盖子串

你正在探访一家农场，农场从左到右种植了一排果树。这些树用一个整数数组 `fruits` 表示，其中 `fruits[i]` 是第 `i` 棵树上的水果 **种类** 。

你想要尽可能多地收集水果。然而，农场的主人设定了一些严格的规矩，你必须按照要求采摘水果：

- 你只有 **两个** 篮子，并且每个篮子只能装 **单一类型** 的水果。每个篮子能够装的水果总量没有限制。
- 你可以选择任意一棵树开始采摘，你必须从 **每棵** 树（包括开始采摘的树）上 **恰好摘一个水果** 。采摘的水果应当符合篮子中的水果类型。每采摘一次，你将会向右移动到下一棵树，并继续采摘。
- 一旦你走到某棵树前，但水果不符合篮子的水果类型，那么就必须停止采摘。

给你一个整数数组 `fruits` ，返回你可以收集的水果的 **最大** 数目。

 

**示例 1：**

```
输入：fruits = [1,2,1]
输出：3
解释：可以采摘全部 3 棵树。
```

**示例 2：**

```
输入：fruits = [0,1,2,2]
输出：3
解释：可以采摘 [1,2,2] 这三棵树。
如果从第一棵树开始采摘，则只能采摘 [0,1] 这两棵树。
```

**示例 3：**

```
输入：fruits = [1,2,3,2,2]
输出：4
解释：可以采摘 [2,3,2,2] 这四棵树。
如果从第一棵树开始采摘，则只能采摘 [1,2] 这两棵树。
```

**示例 4：**

```
输入：fruits = [3,3,3,1,2,1,1,2,3,3,4]
输出：5
解释：可以采摘 [1,2,1,1,2] 这五棵树。
```

```c++
class Solution {
public:
    unordered_map<int,int>hashtable;
    unordered_map<int,int>hashtable1;
    bool check(){
        for(auto s:hashtable1){
            if(hashtable[s.first]<s.second){
                return false;
            }
        }
        return true;
    }
    string minWindow(string s, string t) {
        int count=INT_MAX;
        int left=0;
        int index=0;
        for(auto ch:t){
            hashtable1[ch]++;
        }
        for(int i=0;i<s.size();i++){
            hashtable[s[i]]++;
            while(check()){
                if(i-left+1<count){
                    count=i-left+1;
                    index=left;
                }
                hashtable[s[left]]--;
                if(hashtable[s[left]]==0){
                    hashtable.erase(s[left]);
                }
                left++;

            }
        }
        return count==INT_MAX?string():s.substr(index,count);
    }
};
```

#### 59.螺旋矩阵II

给你一个正整数 `n` ，生成一个包含 `1` 到 `n2` 所有元素，且元素按顺时针顺序螺旋排列的 `n x n` 正方形矩阵 `matrix` 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiraln.jpg)

```
输入：n = 3
输出：[[1,2,3],[8,9,4],[7,6,5]]
```

**示例 2：**

```
输入：n = 1
输出：[[1]]
```

```c++
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        int top=0;
        int down=n-1;
        int left=0;
        int right=n-1;
        int count=1;
        vector<vector<int>>ans(n,vector<int>(n));
        while(1){
            for(int i=left;i<=right;i++){
                ans[top][i]=count++;
            }
            top++;
            if(top>down){
                break;
            }
            for(int i=top;i<=down;i++){
                ans[i][right]=count++;
            }
            right--;
            if(right<left){
                break;
            }
            for(int i=right;i>=left;i--){
                ans[down][i]=count++;
            }
            down--;
            if(down<top){
                break;
            }
            for(int i=down;i>=top;i--){
                ans[i][left]=count++;
            }
            left++;
            if(left>right){
                break;
            }
            
        }
        return ans;
    }
};
```

#### 54.螺旋矩阵

给你一个 `m` 行 `n` 列的矩阵 `matrix` ，请按照 **顺时针螺旋顺序** ，返回矩阵中的所有元素。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiral1.jpg)

```
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiral.jpg)

```
输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]
```

```c++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {

        vector<int>ans;
        int top=0;
        int down=matrix.size()-1;
        int left=0;
        int right=matrix[0].size()-1;
        while(1){
            for(int i=left;i<=right;i++){
                ans.push_back(matrix[top][i]);
            }
            top++;
            if(top>down){
                break;
            }
            for(int i=top;i<=down;i++){
                ans.push_back(matrix[i][right]);
            }
            right--;
            if(right<left){
                break;
            }
            for(int i=right;i>=left;i--){
                ans.push_back(matrix[down][i]);
            }
            down--;
            if(down<top){
                break;
            }
            for(int i=down;i>=top;i--){
                ans.push_back(matrix[i][left]);
            }
            left++;
            if(left>right){
                break;
            }
        }       
        return ans;
    }
    
};
```

#### 剑指 Offer 29. 顺时针打印矩阵

难度简单369收藏分享切换为英文接收动态反馈

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

**示例 1：**

```
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]
```

**示例 2：**

```
输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]
```

```c++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int>ans;
        if(matrix.empty()){
            return ans;
        }
        int left=0;
        int right=matrix[0].size()-1;
        int top=0;
        int down=matrix.size()-1;
        while(1){
            for(int i=left;i<=right;i++){
                ans.push_back(matrix[top][i]);
            }
            top++;
            if(top>down){
                break;
            }
            for(int i=top;i<=down;i++){
                ans.push_back(matrix[i][right]);
            }
            right--;
            if(right<left){
                break;
            }
            for(int i=right;i>=left;i--){
                ans.push_back(matrix[down][i]);
            }
            down--;
            if(down<top){
                break;
            }
            for(int i=down;i>=top;i--){
                ans.push_back(matrix[i][left]);
            }
            left++;
            if(left>right){
                break;
            }
        }
        return ans;
    }
};
```

#### 1365. 有多少小于当前数字的数字

给你一个数组 `nums`，对于其中每个元素 `nums[i]`，请你统计数组中比它小的所有数字的数目。

换而言之，对于每个 `nums[i]` 你必须计算出有效的 `j` 的数量，其中 `j` 满足 `j != i` **且** `nums[j] < nums[i]` 。

以数组形式返回答案。

**示例 1：**

```
输入：nums = [8,1,2,2,3]
输出：[4,0,1,1,3]
解释： 
对于 nums[0]=8 存在四个比它小的数字：（1，2，2 和 3）。 
对于 nums[1]=1 不存在比它小的数字。
对于 nums[2]=2 存在一个比它小的数字：（1）。 
对于 nums[3]=2 存在一个比它小的数字：（1）。 
对于 nums[4]=3 存在三个比它小的数字：（1，2 和 2）。
```

**示例 2：**

```
输入：nums = [6,5,4,8]
输出：[2,1,0,3]
```

**示例 3：**

```
输入：nums = [7,7,7,7]
输出：[0,0,0,0]
```

```c++
class Solution {
public:
    vector<int> smallerNumbersThanCurrent(vector<int>& nums) {
        vector<int>temp=nums;
        sort(nums.begin(),nums.end());
        int hash[101];
        for(int i=nums.size()-1;i>=0;i--){
            hash[nums[i]]=i;
        }
        vector<int>ans;
        for(int i=0;i<temp.size();i++){
            ans.push_back(hash[temp[i]]);
        }
        return ans;
    }
};
```

#### 941. 有效的山脉数组

给定一个整数数组 `arr`，如果它是有效的山脉数组就返回 `true`，否则返回 `false`。

让我们回顾一下，如果 `arr` 满足下述条件，那么它是一个山脉数组：

- `arr.length >= 3`

- 在 

  ```
  0 < i < arr.length - 1
  ```

   条件下，存在 

  ```
  i
  ```

   使得：

  - `arr[0] < arr[1] < ... arr[i-1] < arr[i]`
  - `arr[i] > arr[i+1] > ... > arr[arr.length - 1]`

 

![img](https://assets.leetcode.com/uploads/2019/10/20/hint_valid_mountain_array.png)

 

**示例 1：**

```
输入：arr = [2,1]
输出：false
```

**示例 2：**

```
输入：arr = [3,5,5]
输出：false
```

**示例 3：**

```
输入：arr = [0,3,2,1]
输出：true
```

```c++
class Solution {
public:
    bool validMountainArray(vector<int>& arr) {
        if(arr.size()<3){
            return false;
        }
        int left=0;
        int right=arr.size()-1;
        while(left<arr.size()-1&&arr[left]<arr[left+1]){
            left++;
        }
        while(right>0&&arr[right-1]>arr[right]){
            right--;
        }
        if(left==right&&left!=0&&right!=arr.size()-1){
            return true;
        }
        return false;
    }
};
```

#### 1207. 独一无二的出现次数

给你一个整数数组 `arr`，请你帮忙统计数组中每个数的出现次数。

如果每个数的出现次数都是独一无二的，就返回 `true`；否则返回 `false`。

**示例 1：**

```
输入：arr = [1,2,2,1,1,3]
输出：true
解释：在该数组中，1 出现了 3 次，2 出现了 2 次，3 只出现了 1 次。没有两个数的出现次数相同。
```

**示例 2：**

```
输入：arr = [1,2]
输出：false
```

**示例 3：**

```
输入：arr = [-3,0,1,-3,1,1,1,-3,10,0]
输出：true
```

```c++
class Solution {
public:
    bool uniqueOccurrences(vector<int>& arr) {
        vector<int>v;
        sort(arr.begin(),arr.end());
        int count=1;
        for(int i=0;i<arr.size()-1;i++){
            if(arr[i]==arr[i+1]){
                count++;
            }
            else{
                v.push_back(count);
                count=1;
            }
        }
        v.push_back(count);
        sort(v.begin(),v.end());
        for(int i=1;i<v.size();i++){
            if(v[i]==v[i-1]){
                return false;
            }
        }

        return true;
    }
};
```

#### 189. 轮转数组

给你一个数组，将数组中的元素向右轮转 `k` 个位置，其中 `k` 是非负数。

**示例 1:**

```
输入: nums = [1,2,3,4,5,6,7], k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右轮转 1 步: [7,1,2,3,4,5,6]
向右轮转 2 步: [6,7,1,2,3,4,5]
向右轮转 3 步: [5,6,7,1,2,3,4]
```

**示例 2:**

```
输入：nums = [-1,-100,3,99], k = 2
输出：[3,99,-1,-100]
解释: 
向右轮转 1 步: [99,-1,-100,3]
向右轮转 2 步: [3,99,-1,-100]
```

```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int count=k%(nums.size());
        reverse(nums.begin(),nums.end()-count);
        reverse(nums.end()-count,nums.end());
        reverse(nums.begin(),nums.end());
    }
};
```

#### 724. 寻找数组的中心下标

给你一个整数数组 `nums` ，请计算数组的 **中心下标** 。

数组 **中心下标** 是数组的一个下标，其左侧所有元素相加的和等于右侧所有元素相加的和。

如果中心下标位于数组最左端，那么左侧数之和视为 `0` ，因为在下标的左侧不存在元素。这一点对于中心下标位于数组最右端同样适用。

如果数组有多个中心下标，应该返回 **最靠近左边** 的那一个。如果数组不存在中心下标，返回 `-1` 。

**示例 1：**

```
输入：nums = [1, 7, 3, 6, 5, 6]
输出：3
解释：
中心下标是 3 。
左侧数之和 sum = nums[0] + nums[1] + nums[2] = 1 + 7 + 3 = 11 ，
右侧数之和 sum = nums[4] + nums[5] = 5 + 6 = 11 ，二者相等。
```

**示例 2：**

```
输入：nums = [1, 2, 3]
输出：-1
解释：
数组中不存在满足此条件的中心下标。
```

**示例 3：**

```
输入：nums = [2, 1, -1]
输出：0
解释：
中心下标是 0 。
左侧数之和 sum = 0 ，（下标 0 左侧不存在元素），
右侧数之和 sum = nums[1] + nums[2] = 1 + -1 = 0 。
```

```c++
class Solution {
public:
    int pivotIndex(vector<int>& nums) {
        int sum=0;
        for(int i=0;i<nums.size();i++){
            sum+=nums[i];
        }
        int s=0;
        for(int i=0;i<nums.size();i++){
            if(2*s+nums[i]==sum){
                return i;
            }
            s+=nums[i];
        }
        return -1;



    }
};
```

#### 922. 按奇偶排序数组 II

给定一个非负整数数组 `nums`， `nums` 中一半整数是 **奇数** ，一半整数是 **偶数** 。

对数组进行排序，以便当 `nums[i]` 为奇数时，`i` 也是 **奇数** ；当 `nums[i]` 为偶数时， `i` 也是 **偶数** 。

你可以返回 *任何满足上述条件的数组作为答案* 。

**示例 1：**

```
输入：nums = [4,2,5,7]
输出：[4,5,2,7]
解释：[4,7,2,5]，[2,5,4,7]，[2,7,4,5] 也会被接受。
```

**示例 2：**

```
输入：nums = [2,3]
输出：[2,3]
```

```c++
class Solution {
public:
    vector<int> sortArrayByParityII(vector<int>& nums) {
        int odd=1;
        int even=0;
        while(odd<nums.size()&&even<nums.size()){
            if(nums[odd]%2){
                odd+=2;
            }
            if(nums[even]%2==0){
                even+=2;
            }
            if(odd<nums.size()&&even<nums.size()&&nums[odd]%2==0&&nums[even]%2==1){
                swap(nums[odd],nums[even]);
                odd+=2;
                even+=2;
            }
        }
        return nums;

    }
};
```

#### 136. 只出现一次的数字

给定一个**非空**整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

**说明：**

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

**示例 1:**

```
输入: [2,2,1]
输出: 1
```

**示例 2:**

```c++
输入: [4,1,2,1,2]
输出: 4
```

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int ans=0;
        for(auto i:nums){
            ans^=i;
        }
        return ans;
    }
};
```

#### 169. 多数元素

给定一个大小为 `n` 的数组 `nums` ，返回其中的多数元素。多数元素是指在数组中出现次数 **大于** `⌊ n/2 ⌋` 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

 

**示例 1：**

```
输入：nums = [3,2,3]
输出：3
```

**示例 2：**

```
输入：nums = [2,2,1,1,1,2,2]
输出：2
```

```c++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        return nums[nums.size()/2];
    }
};
```

#### 338. 比特位计数

给你一个整数 `n` ，对于 `0 <= i <= n` 中的每个 `i` ，计算其二进制表示中 **`1` 的个数** ，返回一个长度为 `n + 1` 的数组 `ans` 作为答案。

 

**示例 1：**

```
输入：n = 2
输出：[0,1,1]
解释：
0 --> 0
1 --> 1
2 --> 10
```

**示例 2：**

```
输入：n = 5
输出：[0,1,1,2,1,2]
解释：
0 --> 0
1 --> 1
2 --> 10
3 --> 11
4 --> 100
5 --> 101
```

```c++
class Solution {
public:
    vector<int> countBits(int n) {
        vector<int>ans(n+1);
        for(int i=0;i<=n;i++){
            int cur=i;
            while(cur){
                ans[i]+=cur&1;
                cur>>=1;
            }
        }
        return ans;
    }
};
```

#### 448. 找到所有数组中消失的数字

给你一个含 `n` 个整数的数组 `nums` ，其中 `nums[i]` 在区间 `[1, n]` 内。请你找出所有在 `[1, n]` 范围内但没有出现在 `nums` 中的数字，并以数组的形式返回结果。

 

**示例 1：**

```
输入：nums = [4,3,2,7,8,2,3,1]
输出：[5,6]
```

**示例 2：**

```
输入：nums = [1,1]
输出：[2]
```

```c++
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        vector<int>ans;
        int count=1;
        sort(nums.begin(),nums.end());
        for(int i=0;i<nums.size();i++){
            if(i>0&&nums[i]==nums[i-1]){
                continue;
            }
            while(nums[i]!=count){
                ans.push_back(count);
                count++;
            }
            if(nums[i]==count){
                count++;
            }
        }
        while(count<=nums.size()){
            ans.push_back(count);
            count++;
        }
        return ans;
    }
};
```

#### 461. 汉明距离

两个整数之间的 [汉明距离](https://baike.baidu.com/item/汉明距离) 指的是这两个数字对应二进制位不同的位置的数目。

给你两个整数 `x` 和 `y`，计算并返回它们之间的汉明距离。

 

**示例 1：**

```
输入：x = 1, y = 4
输出：2
解释：
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑
上面的箭头指出了对应二进制位不同的位置。
```

**示例 2：**

```
输入：x = 3, y = 1
输出：1
```

```c++
class Solution {
public:
    int hammingDistance(int x, int y) {
        x^=y;
        int ans=0;
        while(x){
            ans+=(x&1);
            x>>=1;
        }
        return ans;
    }
};
```

#### 11. 盛最多水的容器

给定一个长度为 `n` 的整数数组 `height` 。有 `n` 条垂线，第 `i` 条线的两个端点是 `(i, 0)` 和 `(i, height[i])` 。

找出其中的两条线，使得它们与 `x` 轴共同构成的容器可以容纳最多的水。

返回容器可以储存的最大水量。

**说明：**你不能倾斜容器。

 

**示例 1：**

![img](https://aliyun-lc-upload.oss-cn-hangzhou.aliyuncs.com/aliyun-lc-upload/uploads/2018/07/25/question_11.jpg)

```
输入：[1,8,6,2,5,4,8,3,7]
输出：49 
解释：图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。
```

**示例 2：**

```
输入：height = [1,1]
输出：1
```

```c++
class Solution {
public:
    int maxArea(vector<int>& height) {
        int left=0;
        int right=height.size()-1;
        int ans=0;
        while(left<right){
            if(height[left]<height[right]){
                ans=max(ans,(right-left)*height[left++]);
            }
            else{
                ans=max(ans,(right-left)*height[right--]);
            }
        }
        return ans;
    }
};
```

#### 33. 搜索旋转排序数组

整数数组 `nums` 按升序排列，数组中的值 **互不相同** 。

在传递给函数之前，`nums` 在预先未知的某个下标 `k`（`0 <= k < nums.length`）上进行了 **旋转**，使数组变为 `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]`（下标 **从 0 开始** 计数）。例如， `[0,1,2,4,5,6,7]` 在下标 `3` 处经旋转后可能变为 `[4,5,6,7,0,1,2]` 。

给你 **旋转后** 的数组 `nums` 和一个整数 `target` ，如果 `nums` 中存在这个目标值 `target` ，则返回它的下标，否则返回 `-1` 。

你必须设计一个时间复杂度为 `O(log n)` 的算法解决此问题。

 

**示例 1：**

```
输入：nums = [4,5,6,7,0,1,2], target = 0
输出：4
```

**示例 2：**

```
输入：nums = [4,5,6,7,0,1,2], target = 3
输出：-1
```

**示例 3：**

```
输入：nums = [1], target = 0
输出：-1
```

```c++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int ans=0;
        if(nums[ans]<target){
            
            while(ans<nums.size()-1&&nums[ans]<target){
                ans++;
            }
        }
        else if(nums[ans]>target){
            ans=nums.size()-1;
            while(ans>0&&nums[ans]>target){
                ans--;
            }
        }
        return nums[ans]==target?ans:-1;
    }
};
```

#### 48. 旋转图像

给定一个 *n* × *n* 的二维矩阵 `matrix` 表示一个图像。请你将图像顺时针旋转 90 度。

你必须在**[ 原地](https://baike.baidu.com/item/原地算法)** 旋转图像，这意味着你需要直接修改输入的二维矩阵。**请不要** 使用另一个矩阵来旋转图像。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/08/28/mat1.jpg)

```
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[[7,4,1],[8,5,2],[9,6,3]]
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/08/28/mat2.jpg)

```
输入：matrix = [[5,1,9,11],[2,4,8,10],[13,3,6,7],[15,14,12,16]]
输出：[[15,13,2,5],[14,3,4,1],[12,6,8,9],[16,7,10,11]]
```

```c++
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        for(int i=0;i<matrix.size()/2;i++){
            swap(matrix[i],matrix[matrix.size()-1-i]);
        }
        for(int i=0;i<matrix.size();i++){
            for(int j=i;j<matrix.size();j++){
                swap(matrix[i][j],matrix[j][i]);
            }
        }

    }
};
```

#### 75. 颜色分类

给定一个包含红色、白色和蓝色、共 `n` 个元素的数组 `nums` ，**[原地](https://baike.baidu.com/item/原地算法)**对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

我们使用整数 `0`、 `1` 和 `2` 分别表示红色、白色和蓝色。



必须在不使用库的sort函数的情况下解决这个问题。

 

**示例 1：**

```
输入：nums = [2,0,2,1,1,0]
输出：[0,0,1,1,2,2]
```

**示例 2：**

```
输入：nums = [2,0,1]
输出：[0,1,2]
```

```c++
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int left=0;
        int right=nums.size()-1;
        int a=0;
        while(a<=right){
            if(nums[a]==0){
                swap(nums[a],nums[left]);
                left++;
                a++;
            }
            else if(nums[a]==1){
                a++;
            }
            else{
                swap(nums[a],nums[right]);
                right--;
            }

        }
    }
};
```

#### 128. 最长连续序列

给定一个未排序的整数数组 `nums` ，找出数字连续的最长序列（不要求序列元素在原数组中连续）的长度。

请你设计并实现时间复杂度为 `O(n)` 的算法解决此问题。

 

**示例 1：**

```
输入：nums = [100,4,200,1,3,2]
输出：4
解释：最长数字连续序列是 [1, 2, 3, 4]。它的长度为 4。
```

**示例 2：**

```
输入：nums = [0,3,7,2,5,8,4,6,0,1]
输出：9
```

```c++
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        int ans=0;
        unordered_map<int,int>hashtable;
        for(int i=0;i<nums.size();i++){
            hashtable[nums[i]]=1;
        }
        for(int i=0;i<nums.size();i++){
            if(hashtable[nums[i]]!=1){
                continue;
            }
            else{
                int count=nums[i];
                while(hashtable.find(count-1)!=hashtable.end()){
                    if(hashtable[count-1]==1){
                        hashtable[nums[i]]++;
                        hashtable[count-1]=0;
                        count--;
                    }
                    else{
                        hashtable[nums[i]]+=hashtable[count-1];
                        break;
                    }
                }
            }
            ans=max(ans,hashtable[nums[i]]);
        }
        return ans;
    }
};
```

#### 118. 杨辉三角

给定一个非负整数 *`numRows`，*生成「杨辉三角」的前 *`numRows`* 行。

在「杨辉三角」中，每个数是它左上方和右上方的数的和。

![img](https://pic.leetcode-cn.com/1626927345-DZmfxB-PascalTriangleAnimated2.gif)

 

**示例 1:**

```
输入: numRows = 5
输出: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
```

**示例 2:**

```
输入: numRows = 1
输出: [[1]]
```

```c++
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>>ans;
        for(int i=0;i<numRows;i++){
            vector<int>v;
            for(int j=0;j<i+1;j++){
                if(j==0){
                    v.push_back(1);
                }
                else if(i==j){
                    v.push_back(1);
                }
                else{
                    v.push_back(ans[i-1][j]+ans[i-1][j-1]);
                }
            }
            ans.push_back(v);
        }
        return ans;
    }
};
```



## 字符串

#### 344. 反转字符串

编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 `s` 的形式给出。

不要给另外的数组分配额外的空间，你必须**[原地](https://baike.baidu.com/item/原地算法)修改输入数组**、使用 O(1) 的额外空间解决这一问题。

**示例 1：**

```
输入：s = ["h","e","l","l","o"]
输出：["o","l","l","e","h"]
```

**示例 2：**

```
输入：s = ["H","a","n","n","a","h"]
输出：["h","a","n","n","a","H"]
```

```c++
class Solution {
public:
    void reverseString(vector<char>& s) {
        for(int i=0,j=s.size()-1;i<j;i++,j--){
            swap(s[i],s[j]);
        }
    }
};
```

#### 541. 反转字符串II

给定一个字符串 `s` 和一个整数 `k`，从字符串开头算起，每计数至 `2k` 个字符，就反转这 `2k` 字符中的前 `k` 个字符。

- 如果剩余字符少于 `k` 个，则将剩余字符全部反转。
- 如果剩余字符小于 `2k` 但大于或等于 `k` 个，则反转前 `k` 个字符，其余字符保持原样。

 

**示例 1：**

```
输入：s = "abcdefg", k = 2
输出："bacdfeg"
```

**示例 2：**

```
输入：s = "abcd", k = 2
输出："bacd"
```

```c++
class Solution {
public:
    string reverseStr(string s, int k) {
        for(int i=0;i<s.size();i+=2*k){
            if(s.size()-1-i>=k){
                reverse(s.begin()+i,s.begin()+i+k);
            }
            else{
                reverse(s.begin()+i,s.end());
            }
        }
        return s;
    }
};
```

#### 剑指Offer 05.替换空格

请实现一个函数，把字符串 `s` 中的每个空格替换成"%20"。

 

**示例 1：**

```
输入：s = "We are happy."
输出："We%20are%20happy."
```

```c++
class Solution {
public:
    string replaceSpace(string s) {
        int count=0;
        for(auto &ch:s){
            if(ch==' '){
                count++;
            }
        }
        int b=s.size()-1;
        s.resize(s.size()+2*count);  
        int a=s.size()-1;
        for(int i=b;i>=0;i--){
            if(s[i]==' '){
                s[a--]='0';
                s[a--]='2';
                s[a--]='%';
            }
            else{
                s[a--]=s[i];
            }
        }
        return s;
    }
};
```

#### 151.翻转字符串里的单词

给你一个字符串 `s` ，逐个翻转字符串中的所有 **单词** 。

**单词** 是由非空格字符组成的字符串。`s` 中使用至少一个空格将字符串中的 **单词** 分隔开。

请你返回一个翻转 `s` 中单词顺序并用单个空格相连的字符串。

**说明：**

- 输入字符串 `s` 可以在前面、后面或者单词间包含多余的空格。
- 翻转后单词间应当仅用一个空格分隔。
- 翻转后的字符串中不应包含额外的空格。

 

**示例 1：**

```
输入：s = "the sky is blue"
输出："blue is sky the"
```

**示例 2：**

```
输入：s = "  hello world  "
输出："world hello"
解释：输入字符串可以在前面或者后面包含多余的空格，但是翻转后的字符不能包括。
```

**示例 3：**

```
输入：s = "a good   example"
输出："example good a"
解释：如果两个单词间有多余的空格，将翻转后单词间的空格减少到只含一个。
```

**示例 4：**

```
输入：s = "  Bob    Loves  Alice   "
输出："Alice Loves Bob"
```

**示例 5：**

```
输入：s = "Alice does not even like bob"
输出："bob like even not does Alice"
```

```c++
class Solution {
public:
    string reverseWords(string s) {
        reverse(s.begin(),s.end());
        for(int i=s.size()-1;i>0;i--){
            if(s[i]==s[i-1]&&s[i]==' '){
                s.erase(s.begin()+i);
            }
        }
        if(s[0]==' '){
            s.erase(s.begin());
        }
        if(s[s.size()-1]!=' '){
            s.push_back(' ');
        }
        int count=0;
        for(int i=0;i<s.size();i++){
            if(s[i]==' '){
                reverse(s.begin()+count,s.begin()+i);
                count=i+1;
            }
        }
        s.pop_back();
        return s;
    }
};
```

#### 剑指Offer58-II.左旋转字符串

字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

 

**示例 1：**

```
输入: s = "abcdefg", k = 2
输出: "cdefgab"
```

**示例 2：**

```
输入: s = "lrloseumgh", k = 6
输出: "umghlrlose"
```

```c++
class Solution {
public:
    string reverseLeftWords(string s, int n) {
        reverse(s.begin(),s.begin()+n);
        reverse(s.begin(),s.end());
        reverse(s.begin(),s.end()-n);
        return s;
    }
};
```

#### >>28. 实现 strStr()

实现 [strStr()](https://baike.baidu.com/item/strstr/811469) 函数。

给你两个字符串 `haystack` 和 `needle` ，请你在 `haystack` 字符串中找出 `needle` 字符串出现的第一个位置（下标从 0 开始）。如果不存在，则返回 `-1` 。

**说明：**

当 `needle` 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 `needle` 是空字符串时我们应当返回 0 。这与 C 语言的 [strstr()](https://baike.baidu.com/item/strstr/811469) 以及 Java 的 [indexOf()](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#indexOf(java.lang.String)) 定义相符。

**示例 1：**

```
输入：haystack = "hello", needle = "ll"
输出：2
```

**示例 2：**

```
输入：haystack = "aaaaa", needle = "bba"
输出：-1
```

**示例 3：**

```
输入：haystack = "", needle = ""
输出：0
```

```c++
class Solution {
public:
    void func(int *next,string &needle){
        int j=0;
        next[0]=0;
        for(int i=1;i<needle.size();i++){
            while(j>0&&needle[i]!=needle[j]){
                j=next[j-1];
            }
            if(needle[i]==needle[j]){
                j++;
            }
            next[i]=j;
        }
    }
    int strStr(string haystack, string needle) {
        if(needle.size()==0){
            return 0;
        }
        int next[needle.size()];
        func(next,needle);
        int j=0;
        for(int i=0;i<haystack.size();i++){
            while(j>0&&haystack[i]!=needle[j]){
                j=next[j-1];
            }
            if(needle[j]==haystack[i]){
                j++;
            }
            if(j==needle.size()){
                return i-needle.size()+1;
            }
        }
        return -1;
    }
};
```

#### >>459.重复的子字符串

给定一个非空的字符串，判断它是否可以由它的一个子串重复多次构成。给定的字符串只含有小写英文字母，并且长度不超过10000。

**示例 1:**

```
输入: "abab"

输出: True

解释: 可由子字符串 "ab" 重复两次构成。
```

**示例 2:**

```
输入: "aba"

输出: False
```

**示例 3:**

```
输入: "abcabcabcabc"

输出: True

解释: 可由子字符串 "abc" 重复四次构成。 (或者子字符串 "abcabc" 重复两次构成。)
```

```
class Solution {
public:
    void func(int *next,string s){
        int j=0;
        next[0]=0;
        for(int i=1;i<s.size();i++){
            while(j>0&&s[i]!=s[j]){
                j=next[j-1];
            }
            if(s[i]==s[j]){
                j++;
            }
            next[i]=j;
        }
    }
    bool repeatedSubstringPattern(string s) {
        if(s.size()==0){
            return false;
        }
        int next[s.size()];
        func(next,s);
        int len=s.size();
        if(next[len-1]!=0 &&(len%(len-next[len-1]))==0){
            return true;
        }
        return false;
    }
};
```

#### 205. 同构字符串

给定两个字符串 `s` 和 `t` ，判断它们是否是同构的。

如果 `s` 中的字符可以按某种映射关系替换得到 `t` ，那么这两个字符串是同构的。

每个出现的字符都应当映射到另一个字符，同时不改变字符的顺序。不同字符不能映射到同一个字符上，相同字符只能映射到同一个字符上，字符可以映射到自己本身。

**示例 1:**

```
输入：s = "egg", t = "add"
输出：true
```

**示例 2：**

```
输入：s = "foo", t = "bar"
输出：false
```

**示例 3：**

```
输入：s = "paper", t = "title"
输出：true
```

```c++
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        if(s.size()!=t.size()){
            return false;
        }
        unordered_map<char,char>hashtable,hashtable1;
        for(int i=0;i<s.size();i++){
            if(hashtable.find(s[i])!=hashtable.end()){
                if(hashtable[s[i]]!=t[i]){
                    return false;
                }
            }
            else{
                if(hashtable1.find(t[i])!=hashtable1.end()){
                    return false;
                }
                hashtable.emplace(s[i],t[i]);
                hashtable1.emplace(t[i],s[i]);
            }
        }
        return true;
    }
};
```

#### 925. 长按键入

你的朋友正在使用键盘输入他的名字 `name`。偶尔，在键入字符 `c` 时，按键可能会被*长按*，而字符可能被输入 1 次或多次。

你将会检查键盘输入的字符 `typed`。如果它对应的可能是你的朋友的名字（其中一些字符可能被长按），那么就返回 `True`。

**示例 1：**

```
输入：name = "alex", typed = "aaleex"
输出：true
解释：'alex' 中的 'a' 和 'e' 被长按。
```

**示例 2：**

```
输入：name = "saeed", typed = "ssaaedd"
输出：false
解释：'e' 一定需要被键入两次，但在 typed 的输出中不是这样。
```

```c++
class Solution {
public:
    bool isLongPressedName(string name, string typed) {
        int slow=0;
        for(int i=0;i<typed.size();i++){
            if(slow<name.size()){
                if(typed[i]!=name[slow]&&(i==0 || typed[i]!=typed[i-1])){
                    return false;
                }
                if(typed[i]==name[slow]){
                    slow++;
                }
            }
            else{
                if(typed[i]!=typed[i-1]){
                    return false;
                }
            }           
        }
        if(slow!=name.size()){
            return false;
        }
        
        return true;
    }
};
```

#### 3. 无重复字符的最长子串

给定一个字符串 `s` ，请你找出其中不含有重复字符的 **最长子串** 的长度。

 

**示例 1:**

```
输入: s = "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

**示例 2:**

```
输入: s = "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

**示例 3:**

```
输入: s = "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int left=0;
        unordered_map<char,int>hashtable;
        int ans=0;
        for(int i=0;i<s.size();i++){
            if(hashtable.find(s[i])!=hashtable.end()){
                left=max(left,hashtable[s[i]]+1);
            }
            hashtable[s[i]]=i;
            if(i-left+1>ans){
                ans=i-left+1;
            }
        }

        return ans;
    }
};
```

#### 13. 罗马数字转整数

罗马数字包含以下七种字符: `I`， `V`， `X`， `L`，`C`，`D` 和 `M`。

```
字符          数值
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

例如， 罗马数字 `2` 写做 `II` ，即为两个并列的 1 。`12` 写做 `XII` ，即为 `X` + `II` 。 `27` 写做 `XXVII`, 即为 `XX` + `V` + `II` 。

通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做 `IIII`，而是 `IV`。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为 `IX`。这个特殊的规则只适用于以下六种情况：

- `I` 可以放在 `V` (5) 和 `X` (10) 的左边，来表示 4 和 9。
- `X` 可以放在 `L` (50) 和 `C` (100) 的左边，来表示 40 和 90。 
- `C` 可以放在 `D` (500) 和 `M` (1000) 的左边，来表示 400 和 900。

给定一个罗马数字，将其转换成整数。

 

**示例 1:**

```
输入: s = "III"
输出: 3
```

**示例 2:**

```
输入: s = "IV"
输出: 4
```

**示例 3:**

```
输入: s = "IX"
输出: 9
```

**示例 4:**

```
输入: s = "LVIII"
输出: 58
解释: L = 50, V= 5, III = 3.
```

**示例 5:**

```
输入: s = "MCMXCIV"
输出: 1994
解释: M = 1000, CM = 900, XC = 90, IV = 4.
```

```C++
class Solution {
public:
    int romanToInt(string s) {
        int ans=0;
        for(int i=0;i<s.size();i++){
            switch(s[i]){
            case 'I': 
                ans+=1;
                break;
            case 'V':
                ans+=5;
                if(i>0&&s[i-1]=='I'){
                    ans-=2;
                }
                break;
            case 'X':
                ans+=10;
                if(i>0&&s[i-1]=='I'){
                    ans-=2;
                }
                break;
            case 'L':
                ans+=50;
                if(i>0&&s[i-1]=='X'){
                    ans-=20;
                }
                break;
            case 'C':
                ans+=100;
                if(i>0&&s[i-1]=='X'){
                    ans-=20;
                }
                break;
            case 'D':
                ans+=500;
                if(i>0&&s[i-1]=='C'){
                    ans-=200;
                }
                break;
            case 'M':   
                ans+=1000;
                if(i>0&&s[i-1]=='C'){
                    ans-=200;
                }
                break;
            }      
        }
        return ans;
    }
};
```

#### 14. 最长公共前缀

编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 `""`。

 

**示例 1：**

```
输入：strs = ["flower","flow","flight"]
输出："fl"
```

**示例 2：**

```
输入：strs = ["dog","racecar","car"]
输出：""
解释：输入不存在公共前缀。
```

```c++
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        string str;
        int count=0;
        char c;
        for(int i=0;i<strs[0].size();i++){
            for(int j=0;j<strs.size();j++){
                c=strs[0][i];
                if(i>=strs[j].size() || strs[j][i]!=c){
                    return str;
                }
                
            }
            str+=c;
        }
        return str;
    }
};
```

#### 125. 验证回文串

给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。

**说明：**本题中，我们将空字符串定义为有效的回文串。

 

**示例 1:**

```
输入: "A man, a plan, a canal: Panama"
输出: true
解释："amanaplanacanalpanama" 是回文串
```

**示例 2:**

```
输入: "race a car"
输出: false
解释："raceacar" 不是回文串
```

```c++
class Solution {
public:
    bool isPalindrome(string s) {
        int left=0;
        int right=s.size()-1;
        while(left<right){
            while(left<right&&!((s[left]>='a'&&s[left]<='z') ||(s[left]>='A'&&s[left]<='Z') ||(s[left]>='0'&&s[left]<='9'))){
                left++;
            }
            while(left<right&&!((s[right]>='a'&&s[right]<='z') ||(s[right]>='A'&&s[right]<='Z')||(s[right]>='0'&&s[right]<='9') )){
                right--;
            }
            if(s[left]>='A'&&s[left]<='Z'){
                s[left]='a'+s[left]-'A';
            }
            if(s[right]>='A'&&s[right]<='Z'){
                s[right]='a'+s[right]-'A';
            }
            if(s[left]!=s[right]){
                return false;
            }
            left++;
            right--;

        }
        return true;
    }
};
```

#### 171. Excel 表列序号

给你一个字符串 `columnTitle` ，表示 Excel 表格中的列名称。返回 *该列名称对应的列序号* 。

例如：

```
A -> 1
B -> 2
C -> 3
...
Z -> 26
AA -> 27
AB -> 28 
...
```

 

**示例 1:**

```
输入: columnTitle = "A"
输出: 1
```

**示例 2:**

```
输入: columnTitle = "AB"
输出: 28
```

**示例 3:**

```
输入: columnTitle = "ZY"
输出: 701
```

```C++
class Solution {
public:
    int titleToNumber(string columnTitle) {
        int ans=0;
        int a=columnTitle.size();
        for(int i=a-1;i>=0;i--){

            ans+=(columnTitle[i]-'A'+1)*pow(26,(a-i-1));
        }
        return ans;
    }
};
```



## 哈希表

#### 242. 有效的字母异位词

给定两个字符串 `*s*` 和 `*t*` ，编写一个函数来判断 `*t*` 是否是 `*s*` 的字母异位词。

**注意：**若 `*s*` 和 `*t*` 中每个字符出现的次数都相同，则称 `*s*` 和 `*t*` 互为字母异位词。

 

**示例 1:**

```
输入: s = "anagram", t = "nagaram"
输出: true
```

**示例 2:**

```
输入: s = "rat", t = "car"
输出: false
```

```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        if(s.size()!=t.size()){
            return false;
        }
        unordered_map<char,int>hashtable;
        for(auto ch:t){
            hashtable[ch]++;
        }
        for(auto ch:s){
            hashtable[ch]--;
            if(hashtable[ch]<0){
                return false;
            }
        }
        return true;
    }
};
```

#### 383.赎金信

给你两个字符串：`ransomNote` 和 `magazine` ，判断 `ransomNote` 能不能由 `magazine` 里面的字符构成。

如果可以，返回 `true` ；否则返回 `false` 。

`magazine` 中的每个字符只能在 `ransomNote` 中使用一次。

 

**示例 1：**

```
输入：ransomNote = "a", magazine = "b"
输出：false
```

**示例 2：**

```
输入：ransomNote = "aa", magazine = "ab"
输出：false
```

**示例 3：**

```
输入：ransomNote = "aa", magazine = "aab"
输出：true
```

```c++
class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
        unordered_map<char,int>hashtable;
        for(auto ch:magazine){
            hashtable[ch]++;
        }
        for(auto ch:ransomNote){
            hashtable[ch]--;
            if(hashtable[ch]<0){
                return false;
            }
        }
        return true;
    }
};
```

#### 49.字母异位词分组

给你一个字符串数组，请你将 **字母异位词** 组合在一起。可以按任意顺序返回结果列表。

**字母异位词** 是由重新排列源单词的字母得到的一个新单词，所有源单词中的字母通常恰好只用一次。

 

**示例 1:**

```
输入: strs = ["eat", "tea", "tan", "ate", "nat", "bat"]
输出: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

**示例 2:**

```
输入: strs = [""]
输出: [[""]]
```

**示例 3:**

```
输入: strs = ["a"]
输出: [["a"]]
```

```c++
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        vector<vector<string>>ans;
        unordered_map<string,vector<string>>hashtable;
        for(auto s:strs){
            string str=s;
            sort(str.begin(),str.end());
            hashtable[str].push_back(s);
        }
        for(auto h:hashtable){
            ans.push_back(h.second);
        }
        return ans;
    }
};
```

#### 438.找到字符串中所有字母异位词

给定两个字符串 `s` 和 `p`，找到 `s` 中所有 `p` 的 **异位词** 的子串，返回这些子串的起始索引。不考虑答案输出的顺序。

**异位词** 指由相同字母重排列形成的字符串（包括相同的字符串）。

 

**示例 1:**

```
输入: s = "cbaebabacd", p = "abc"
输出: [0,6]
解释:
起始索引等于 0 的子串是 "cba", 它是 "abc" 的异位词。
起始索引等于 6 的子串是 "bac", 它是 "abc" 的异位词。
```

 **示例 2:**

```
输入: s = "abab", p = "ab"
输出: [0,1,2]
解释:
起始索引等于 0 的子串是 "ab", 它是 "ab" 的异位词。
起始索引等于 1 的子串是 "ba", 它是 "ab" 的异位词。
起始索引等于 2 的子串是 "ab", 它是 "ab" 的异位词。
```

```c++
class Solution {
public:
    unordered_map<char,int>hashtable,hashtable1;
    bool check(){
        for(auto h:hashtable){
            if(hashtable1[h.first]!=h.second){
                return false;
            }
        }
        return true;
    }
    vector<int> findAnagrams(string s, string p) {
        vector<int>ans;
        for(auto ch:p){
            hashtable[ch]++;
        }
        int count=p.size();
        for(int i=0;i<s.size();i++){
            if(i<count-1){
                hashtable1[s[i]]++;
                continue;
            }
            hashtable1[s[i]]++;
            if(check()){
                ans.push_back(i-count+1);
            }
            hashtable1[s[i-count+1]]--;
        }
        return ans;
    }
};
```

#### 349. 两个数组的交集

给定两个数组，编写一个函数来计算它们的交集。

 

**示例 1：**

```
输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2]
```

**示例 2：**

```
输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[9,4]
```

 

```c++
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int>s,s1;
        for(auto i:nums1)
        {
            s.insert(i);
        }
        for(auto i:nums2)
        {
            if(s.find(i)!=s.end())
            {
                s1.insert(i);
            }
        }
        vector<int>ans;
        for(auto it=s1.begin();it!=s1.end();it++)
        {
            ans.push_back(*it);
        }
        return ans;
    }
};
```

#### 350.两个数组的交集 II

给你两个整数数组 `nums1` 和 `nums2` ，请你以数组形式返回两数组的交集。返回结果中每个元素出现的次数，应与元素在两个数组中都出现的次数一致（如果出现次数不一致，则考虑取较小值）。可以不考虑输出结果的顺序。

 

**示例 1：**

```
输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2,2]
```

**示例 2:**

```
输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[4,9]
```

 

```c++
class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        unordered_map<int,int>hashtable;
        vector<int>ans;
        for(auto i:nums1){
            hashtable[i]++;
        }
        for(auto i:nums2){
            if(hashtable.find(i)!=hashtable.end()){
                hashtable[i]--;
                ans.push_back(i);
                if(hashtable[i]==0){
                    hashtable.erase(i);
                }
            }
        }
        return ans;
    }
};
```

#### 202. 快乐数

编写一个算法来判断一个数 `n` 是不是快乐数。

「快乐数」定义为：

- 对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和。
- 然后重复这个过程直到这个数变为 1，也可能是 **无限循环** 但始终变不到 1。
- 如果 **可以变为** 1，那么这个数就是快乐数。

如果 `n` 是快乐数就返回 `true` ；不是，则返回 `false` 。

 

**示例 1：**

```
输入：n = 19
输出：true
解释：
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```

**示例 2：**

```
输入：n = 2
输出：false
```

```c++
class Solution {
public:
    bool isHappy(int n) {
        unordered_set<int>st;
        int sum=0;
        while(n!=1){
            while(n){
                sum+=(n%10)*(n%10);
                n=n/10;
            }
            if(st.find(sum)!=st.end()){
                return false;
            }
            st.insert(sum);
            n=sum;
            sum=0;
        }
        return true;
    }
};
```

#### 1. 两数之和

给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **和为目标值** *`target`* 的那 **两个** 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

 

**示例 1：**

```
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
```

**示例 2：**

```
输入：nums = [3,2,4], target = 6
输出：[1,2]
```

**示例 3：**

```
输入：nums = [3,3], target = 6
输出：[0,1]
```

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int>ans;
        unordered_map<int,int>hashtable;
        for(int i=0;i<nums.size();i++){
            auto it=hashtable.find(target-nums[i]);
            if(it!=hashtable.end()){
                return {it->second,i};
            }
            hashtable.insert({nums[i],i});
        }
        return ans;
    }
};
```

#### 454.四数相加II

给你四个整数数组 `nums1`、`nums2`、`nums3` 和 `nums4` ，数组长度都是 `n` ，请你计算有多少个元组 `(i, j, k, l)` 能满足：

- `0 <= i, j, k, l < n`
- `nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0`

 

**示例 1：**

```
输入：nums1 = [1,2], nums2 = [-2,-1], nums3 = [-1,2], nums4 = [0,2]
输出：2
解释：
两个元组如下：
1. (0, 0, 0, 1) -> nums1[0] + nums2[0] + nums3[0] + nums4[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> nums1[1] + nums2[1] + nums3[0] + nums4[0] = 2 + (-1) + (-1) + 0 = 0
```

**示例 2：**

```
输入：nums1 = [0], nums2 = [0], nums3 = [0], nums4 = [0]
输出：1
```

```c++
class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
        int ans=0;
        unordered_map<int,int>hashtable;
        for(auto i:nums1){
            for(auto a:nums2){
                hashtable[i+a]++;
            }
        }
        for(auto i:nums3){
            for(auto a:nums4){
                auto it=hashtable.find(0-i-a);
                if(it!=hashtable.end()){
                    ans+=it->second;
                }
            }
        }
        return ans;
    }
};
```

#### 15. 三数之和

难度中等4429收藏分享切换为英文接收动态反馈

给你一个包含 `n` 个整数的数组 `nums`，判断 `nums` 中是否存在三个元素 *a，b，c ，*使得 *a + b + c =* 0 ？请你找出所有和为 `0` 且不重复的三元组。

**注意：**答案中不可以包含重复的三元组。

 

**示例 1：**

```
输入：nums = [-1,0,1,2,-1,-4]
输出：[[-1,-1,2],[-1,0,1]]
```

**示例 2：**

```
输入：nums = []
输出：[]
```

**示例 3：**

```
输入：nums = [0]
输出：[]
```

```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>>ans;
        sort(nums.begin(),nums.end());
        for(int i=0;i<nums.size();i++){
            if(i>0&&nums[i]==nums[i-1]){
                continue;
            }
            int left=i+1;
            int right=nums.size()-1;
            while(left<right){
                if(nums[i]+nums[left]+nums[right]<0){
                    left++;
                }
                else if(nums[i]+nums[left]+nums[right]>0){
                    right--;
                }
                else{
                    ans.push_back({nums[i],nums[left],nums[right]});
                    left++;
                    right--;
                    while(left<right&&nums[left]==nums[left-1]){
                        left++;
                    }
                    while(left<right&&nums[right]==nums[right+1]){
                        right--;
                    }
                }
            }
        }
        return ans;
    }
};
```

#### 18. 四数之和

难度中等1272收藏分享切换为英文接收动态反馈

给你一个由 `n` 个整数组成的数组 `nums` ，和一个目标值 `target` 。请你找出并返回满足下述全部条件且**不重复**的四元组 `[nums[a], nums[b], nums[c], nums[d]]` （若两个四元组元素一一对应，则认为两个四元组重复）：

- `0 <= a, b, c, d < n`
- `a`、`b`、`c` 和 `d` **互不相同**
- `nums[a] + nums[b] + nums[c] + nums[d] == target`

你可以按 **任意顺序** 返回答案 。

 

**示例 1：**

```
输入：nums = [1,0,-1,0,-2,2], target = 0
输出：[[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
```

**示例 2：**

```
输入：nums = [2,2,2,2,2], target = 8
输出：[[2,2,2,2]]
```

```c++
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>>ans;
        sort(nums.begin(),nums.end());
        for(int i=0;i<nums.size()-1;i++){
            if(i>0&&nums[i]==nums[i-1]){
                continue;
            }
            for(int j=i+1;j<nums.size();j++){
                if(j>i+1&&nums[j]==nums[j-1]){
                    continue;
                }
                int left=j+1;
                int right=nums.size()-1;
                while(left<right){
                    if(target-nums[i]-nums[j]<nums[left]+nums[right]){
                        right--;
                    }
                    else if(target-nums[i]-nums[j]>nums[left]+nums[right]){
                        left++;
                    }
                    else{
                        ans.push_back({nums[i],nums[j],nums[left],nums[right]});
                        left++;
                        right--;
                        while(left<right&&nums[left]==nums[left-1]){
                            left++;
                        }
                        while(left<right&&nums[right]==nums[right+1]){
                            right--;
                        }
                    }
                }
            }
            
        }
        
        return ans;
        
    }
};
```



## 链表

#### 707.设计链表

设计链表的实现。您可以选择使用单链表或双链表。单链表中的节点应该具有两个属性：`val` 和 `next`。`val` 是当前节点的值，`next` 是指向下一个节点的指针/引用。如果要使用双向链表，则还需要一个属性 `prev` 以指示链表中的上一个节点。假设链表中的所有节点都是 0-index 的。

在链表类中实现这些功能：

- get(index)：获取链表中第 `index` 个节点的值。如果索引无效，则返回`-1`。
- addAtHead(val)：在链表的第一个元素之前添加一个值为 `val` 的节点。插入后，新节点将成为链表的第一个节点。
- addAtTail(val)：将值为 `val` 的节点追加到链表的最后一个元素。
- addAtIndex(index,val)：在链表中的第 `index` 个节点之前添加值为 `val` 的节点。如果 `index` 等于链表的长度，则该节点将附加到链表的末尾。如果 `index` 大于链表长度，则不会插入节点。如果`index`小于0，则在头部插入节点。
- deleteAtIndex(index)：如果索引 `index` 有效，则删除链表中的第 `index` 个节点。

 

**示例：**

```
MyLinkedList linkedList = new MyLinkedList();
linkedList.addAtHead(1);
linkedList.addAtTail(3);
linkedList.addAtIndex(1,2);   //链表变为1-> 2-> 3
linkedList.get(1);            //返回2
linkedList.deleteAtIndex(1);  //现在链表是1-> 3
linkedList.get(1);            //返回3
```

```c++
class MyLinkedList {
public:
    struct LinkedList{
        LinkedList*next;
        int val;
        LinkedList(int val):val(val),next(NULL){}
    };
    MyLinkedList() {
        count=0;
        cur=new LinkedList(0);
    }
    
    int get(int index) {
        if(index>count-1 || index<0){
            return -1;
        }
        LinkedList*temp=cur->next;
        while(index--){
            temp=temp->next;
        }
        return temp->val;
    }
    
    void addAtHead(int val) {
        LinkedList*temp=new LinkedList(val);
        temp->next=cur->next;
        cur->next=temp;
        count++;
    }
    
    void addAtTail(int val) {
        LinkedList*temp=new LinkedList(val);
        LinkedList*temp1=cur;
        while(temp1->next!=NULL){
            temp1=temp1->next;
        }
        temp1->next=temp;
        count++;
    }
    
    void addAtIndex(int index, int val) {
        LinkedList*temp=new LinkedList(val);
        if(index>count){
            return;
        }
        LinkedList*temp1=cur;
        while(index--){
            temp1=temp1->next;
        }
        temp->next=temp1->next;
        temp1->next=temp;
        count++;
    }
    
    void deleteAtIndex(int index) {
        if(index>=count || index<0){
            return;
        }
        LinkedList*temp=cur;
        while(index--){
            temp=temp->next;
        }
        temp->next=temp->next->next;
        count--;
    }
private:
    int count;
    LinkedList*cur;
};
```

#### 203.移除链表元素

给你一个链表的头节点 `head` 和一个整数 `val` ，请你删除链表中所有满足 `Node.val == val` 的节点，并返回 **新的头节点** 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/03/06/removelinked-list.jpg)

```
输入：head = [1,2,6,3,4,5,6], val = 6
输出：[1,2,3,4,5]
```

**示例 2：**

```
输入：head = [], val = 1
输出：[]
```

**示例 3：**

```
输入：head = [7,7,7,7], val = 7
输出：[]
```

```c++
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        ListNode*cur=new ListNode(0);
        cur->next=head;
        ListNode*temp=cur;
        while(temp->next!=NULL){
            if(temp->next->val==val){
                temp->next=temp->next->next;
            }
            else{
                temp=temp->next; 
            }

        }
        return cur->next;
    }
};
```

#### 206.反转链表

给你单链表的头节点 head ，请你反转链表，并返回反转后的链表。

示例 1：

![img](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

```
输入：head = [1,2,3,4,5]
输出：[5,4,3,2,1]
```

示例 2：

![img](https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg)

```
输入：head = [1,2]
输出：[2,1]
示例 3：

输入：head = []
输出：[]
```



```c++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode*cur=head;
        ListNode*pre=NULL;
        ListNode*temp;
        while(cur){
            temp=cur;
            cur=cur->next;
            temp->next=pre;
            pre=temp;
        }
        return pre;

    }
};
```

#### 24. 两两交换链表中的节点

给你一个链表，两两交换其中相邻的节点，并返回交换后链表的头节点。你必须在不修改节点内部的值的情况下完成本题（即，只能进行节点交换）。

 

示例 1：

![img](https://assets.leetcode.com/uploads/2020/10/03/swap_ex1.jpg)

```
输入：head = [1,2,3,4]
输出：[2,1,4,3]
示例 2：

输入：head = []
输出：[]
示例 3：

输入：head = [1]
输出：[1]
```



```c++
lass Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode*cur=new ListNode(0);
        cur->next=head;
        ListNode*temp=cur;
        while(temp->next&&temp->next->next){
            ListNode*temp1=temp->next;
            ListNode*temp2=temp->next->next;
            ListNode*temp3=temp->next->next->next;
            temp->next=temp2;
            temp->next->next=temp1;
            temp->next->next->next=temp3;
            temp=temp->next->next;
        }
        return cur->next;
    }
};
```

#### 19.删除链表的倒数第N个节点

给你一个链表，删除链表的倒数第 n 个结点，并且返回链表的头结点。

 ![img](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

示例 1：

```
输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]
示例 2：

输入：head = [1], n = 1
输出：[]
示例 3：

输入：head = [1,2], n = 1
输出：[1]
```



```c++
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode*cur=new ListNode(0);
        cur->next=head;
        ListNode*fast=cur;
        ListNode*slow=cur;
        while(n--){
            fast=fast->next;
        }
        while(fast->next){
            fast=fast->next;
            slow=slow->next;
        }
        slow->next=slow->next->next;
        return cur->next;
    }
};
```

#### 面试题 02.07. 链表相交

给你两个单链表的头节点 headA 和 headB ，请你找出并返回两个单链表相交的起始节点。如果两个链表没有交点，返回 null 。

图示两个链表在节点 c1 开始相交：



题目数据 保证 整个链式结构中不存在环。

注意，函数返回结果后，链表必须 保持其原始结构 。



示例 1：

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_statement.png)

```c++
输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Intersected at '8'
```

解释：相交节点的值为 8 （注意，如果两个链表相交则不能为 0）。
从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。
在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。
示例 2：

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_example_2.png)



```c++
输入：intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
输出：Intersected at '2'
```

解释：相交节点的值为 2 （注意，如果两个链表相交则不能为 0)。
从各自的表头开始算起，链表 A 为 [0,9,1,2,4]，链表 B 为 [3,2,4]。
在 A 中，相交节点前有 3 个节点；在 B 中，相交节点前有 1 个节点。
示例 3：

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_example_3.png)

```c++
输入：intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
输出：null
```

解释：从各自的表头开始算起，链表 A 为 [2,6,4]，链表 B 为 [1,5]。
由于这两个链表不相交，所以 intersectVal 必须为 0，而 skipA 和 skipB 可以是任意值。
这两个链表不相交，因此返回 null 。

```c++
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode*heeadA=headA;
        ListNode*heeadB=headB;
        int len_A=0;
        int len_B=0;
        while(heeadA){
            len_A++;
            heeadA=heeadA->next;
        }
        while(heeadB){
            len_B++;
            heeadB=heeadB->next;
        }
        if(len_A>len_B){
            while(len_A-len_B!=0){
                headA=headA->next;
                len_B++;
            }
        }
        else if(len_A<len_B){
            while(len_B-len_A){
                headB=headB->next;
                len_A++;
            }
        }
        while(headA&&headB){
            if(headA==headB){
                return headA;
            }
            else{
                headA=headA->next;
                headB=headB->next;
            }
        }      
        return NULL;
    }
};
```

#### 141. 环形链表

给你一个链表的头节点 `head` ，判断链表中是否有环。

如果链表中有某个节点，可以通过连续跟踪 `next` 指针再次到达，则链表中存在环。 为了表示给定链表中的环，评测系统内部使用整数 `pos` 来表示链表尾连接到链表中的位置（索引从 0 开始）。**注意：`pos` 不作为参数进行传递** 。仅仅是为了标识链表的实际情况。

*如果链表中存在环* ，则返回 `true` 。 否则，返回 `false` 。

 

**示例 1：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist.png)

```
输入：head = [3,2,0,-4], pos = 1
输出：true
解释：链表中有一个环，其尾部连接到第二个节点。
```

**示例 2：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test2.png)

```
输入：head = [1,2], pos = 0
输出：true
解释：链表中有一个环，其尾部连接到第一个节点。
```

**示例 3：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test3.png)

```
输入：head = [1], pos = -1
输出：false
解释：链表中没有环。
```

 

```c++
class Solution {
public:
    bool hasCycle(ListNode *head) {
        ListNode*n1=head;
        ListNode*n2=head;
        while(n1&&n1->next){
            n1=n1->next->next;
            n2=n2->next;
            if(n1==NULL){
                return false;
            }
            if(n1==n2){
                return true;
            }
            
        }
        return false;
    }
};
```



####  142.环形链表II

给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

如果链表中有某个节点，可以通过连续跟踪 next 指针再次到达，则链表中存在环。 为了表示给定链表中的环，评测系统内部使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。如果 pos 是 -1，则在该链表中没有环。注意：pos 不作为参数进行传递，仅仅是为了标识链表的实际情况。

不允许修改 链表。

 ![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist.png)

```
输入：head = [3,2,0,-4], pos = 1
输出：返回索引为 1 的链表节点
解释：链表中有一个环，其尾部连接到第二个节点。
```

示例 2：

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test2.png)

```
输入：head = [1,2], pos = 0
输出：返回索引为 0 的链表节点
解释：链表中有一个环，其尾部连接到第一个节点。
```

示例 3：

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test3.png)

```
输入：head = [1], pos = -1
输出：返回 null
解释：链表中没有环。
```



```c++
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode*slow=head;
        ListNode*fast=head;
        while(fast!=NULL&&fast->next!=NULL){
            fast=fast->next->next;
            slow=slow->next;
            if(slow==fast){
                ListNode*index1=fast;
                ListNode*index2=head;
                while(index1!=index2){
                    index1=index1->next;
                    index2=index2->next;
                }
                return index1;
            }
        }       
        return NULL;
    }
};
```

#### 234. 回文链表

给你一个单链表的头节点 `head` ，请你判断该链表是否为回文链表。如果是，返回 `true` ；否则，返回 `false` 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg)

```
输入：head = [1,2,2,1]
输出：true
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg)

```
输入：head = [1,2]
输出：false
```

```c++
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        vector<int>v;
        while(head){
            v.push_back(head->val);
            head=head->next;
        }
        int left=0;
        int right=v.size()-1;
        while(left<right){
            if(v[left]==v[right]){
                left++;
                right--;
            }
            else{
                return false;
            }
        }
        return true;
    }
};
```

#### 143. 重排链表

给定一个单链表 `L` 的头节点 `head` ，单链表 `L` 表示为：

```
L0 → L1 → … → Ln - 1 → Ln
```

请将其重新排列后变为：

```
L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
```

不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

 

**示例 1：**

![img](https://pic.leetcode-cn.com/1626420311-PkUiGI-image.png)

```
输入：head = [1,2,3,4]
输出：[1,4,2,3]
```

**示例 2：**

![img](https://pic.leetcode-cn.com/1626420320-YUiulT-image.png)

```
输入：head = [1,2,3,4,5]
输出：[1,5,2,4,3]
```

```c++
class Solution {
public:
    ListNode* func(ListNode*head){
        ListNode*temp=NULL;
        ListNode*cur=head;
        while(cur){
            ListNode*temp1=cur->next;
            cur->next=temp;
            temp=cur;
            cur=temp1;
        }
        return temp;
    }
    void reorderList(ListNode* head) {
        ListNode*temp=head;
        while(temp->next){
            temp->next=func(temp->next);
            temp=temp->next;
        }
    }
};
```

#### 21. 合并两个有序链表

将两个升序链表合并为一个新的 **升序** 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg)

```
输入：l1 = [1,2,4], l2 = [1,3,4]
输出：[1,1,2,3,4,4]
```

**示例 2：**

```
输入：l1 = [], l2 = []
输出：[]
```

**示例 3：**

```
输入：l1 = [], l2 = [0]
输出：[0]
```

 

```c++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        ListNode*ans=new ListNode(0);
        ListNode*cur=ans;
        while(list1 && list2){
            if(list1->val>list2->val){
                ListNode*temp=new ListNode(list2->val);
                cur->next=temp;
                cur=cur->next;
                list2=list2->next;
            }
            else{
                ListNode*temp=new ListNode(list1->val);
                cur->next=temp;
                cur=cur->next;
                list1=list1->next;
            
            }
        }
        if(list1){
            cur->next=list1;
        }
        if(list2){
            cur->next=list2;
        }
        return ans->next;
    }
};
```

#### 2. 两数相加

给你两个 **非空** 的链表，表示两个非负的整数。它们每位数字都是按照 **逆序** 的方式存储的，并且每个节点只能存储 **一位** 数字。

请你将两个数相加，并以相同形式返回一个表示和的链表。

你可以假设除了数字 0 之外，这两个数都不会以 0 开头。

 

**示例 1：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2021/01/02/addtwonumber1.jpg)

```
输入：l1 = [2,4,3], l2 = [5,6,4]
输出：[7,0,8]
解释：342 + 465 = 807.
```

**示例 2：**

```
输入：l1 = [0], l2 = [0]
输出：[0]
```

**示例 3：**

```
输入：l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
输出：[8,9,9,9,0,0,0,1]
```

```c++
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode*cur=new ListNode(0);
        ListNode*ans=cur;
        int num=0;
        while(l1 || l2 || num!=0){
            if(l1){
                num+=l1->val;
                l1=l1->next;
            }
            if(l2){
                num+=l2->val;
                l2=l2->next;
            }
            ListNode*temp=new ListNode(num%10);
            cur->next=temp;
            cur=cur->next;
            num=num/10;
        }
        return ans->next;
    }
};
```

#### 237. 删除链表中的节点

请编写一个函数，用于 **删除单链表中某个特定节点** 。在设计函数时需要注意，你无法访问链表的头节点 `head` ，只能直接访问 **要被删除的节点** 。

题目数据保证需要删除的节点 **不是末尾节点** 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/09/01/node1.jpg)

```
输入：head = [4,5,1,9], node = 5
输出：[4,1,9]
解释：指定链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/09/01/node2.jpg)

```
输入：head = [4,5,1,9], node = 1
输出：[4,5,9]
解释：指定链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9
```

```c++
class Solution {
public:
    void deleteNode(ListNode* node) {
        node->val=node->next->val;
        node->next=node->next->next;
    }
};
```

#### >>148. 排序链表(并归排序)

给你链表的头结点 `head` ，请将其按 **升序** 排列并返回 **排序后的链表** 。



 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/09/14/sort_list_1.jpg)

```
输入：head = [4,2,1,3]
输出：[1,2,3,4]
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/09/14/sort_list_2.jpg)

```
输入：head = [-1,5,3,4,0]
输出：[-1,0,3,4,5]
```

**示例 3：**

```
输入：head = []
输出：[]
```

```c++
class Solution {
public:
    ListNode* sortList(ListNode* head) {
        vector<int>v;
        while(head){
            v.push_back(head->val);
            head=head->next;
        }
        sort(v.begin(),v.end());
        ListNode*root=new ListNode(0);
        ListNode*cur=root;
        for(int i=0;i<v.size();i++){
            ListNode*temp=new ListNode(v[i]);
            cur->next=temp;
            cur=cur->next;
        }
        return root->next;
    }
};
```

#### 61. 旋转链表

给你一个链表的头节点 `head` ，旋转链表，将链表每个节点向右移动 `k` 个位置。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/13/rotate1.jpg)

```
输入：head = [1,2,3,4,5], k = 2
输出：[4,5,1,2,3]
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/11/13/roate2.jpg)

```
输入：head = [0,1,2], k = 4
输出：[2,0,1]
```

```c++
class Solution {
public:
    ListNode* rotateRight(ListNode* head, int k) {
        if(head==NULL){
            return head;
        }
        ListNode*cur=new ListNode(0);
        cur->next=head;
        ListNode*temp=cur;
        ListNode*temp1=cur;
        int count=0;
        while(temp&&temp->next){
            count++;
            temp=temp->next;
        }
        int a=k%count;
        if(a==0){
            return head;
        }
        count-=a;
        while(count--){
            temp1=temp1->next;
        }
        ListNode*ans=temp1->next;
        temp1->next=NULL;
        ListNode*ans1=ans;
        while(ans1&&ans1->next){
            ans1=ans1->next;
        }
        ans1->next=cur->next;
        return ans;

    }
};
```



## 栈和队列

#### 232.用栈实现队列

请你仅使用两个栈实现先入先出队列。队列应当支持一般队列支持的所有操作（push、pop、peek、empty）：

实现 MyQueue 类：

void push(int x) 将元素 x 推到队列的末尾
int pop() 从队列的开头移除并返回元素
int peek() 返回队列开头的元素
boolean empty() 如果队列为空，返回 true ；否则，返回 false


说明：

你只能使用标准的栈操作 —— 也就是只有 push to top, peek/pop from top, size, 和 is empty 操作是合法的。
你所使用的语言也许不支持栈。你可以使用 list 或者 deque（双端队列）来模拟一个栈，只要是标准的栈操作即可。


进阶：

你能否实现每个操作均摊时间复杂度为 O(1) 的队列？换句话说，执行 n 个操作的总时间复杂度为 O(n) ，即使其中一个操作可能花费较长时间。


示例：

```
输入：
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]
输出：
[null, null, null, 1, 1, false]

解释：
MyQueue myQueue = new MyQueue();
myQueue.push(1); // queue is: [1]
myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
myQueue.peek(); // return 1
myQueue.pop(); // return 1, queue is [2]
myQueue.empty(); // return false
```



```c++
lass MyQueue {
public:
    stack<int>stk,stk1;
    MyQueue() {

    }
    
    void push(int x) {
        stk.push(x);
    }
    
    int pop() {
        int ans;
        if(!stk1.empty()){
            ans=stk1.top();
            stk1.pop();
        }
        else{
            while(!stk.empty()){
                stk1.push(stk.top());
                stk.pop();
            }
            ans=stk1.top();
            stk1.pop();
        }
        return ans;
    }
    
    int peek() {
        int ans=pop();
        stk1.push(ans);
        return ans;
    }
    
    bool empty() {
        if(stk.empty()&&stk1.empty()){
            return true;
        }
        return false;
    }
};

```

#### 225. 用队列实现栈

请你仅使用两个队列实现一个后入先出（LIFO）的栈，并支持普通栈的全部四种操作（push、top、pop 和 empty）。

实现 MyStack 类：

void push(int x) 将元素 x 压入栈顶。
int pop() 移除并返回栈顶元素。
int top() 返回栈顶元素。
boolean empty() 如果栈是空的，返回 true ；否则，返回 false 。


注意：

你只能使用队列的基本操作 —— 也就是 push to back、peek/pop from front、size 和 is empty 这些操作。
你所使用的语言也许不支持队列。 你可以使用 list （列表）或者 deque（双端队列）来模拟一个队列 , 只要是标准的队列操作即可。


示例：

```
输入：
["MyStack", "push", "push", "top", "pop", "empty"]
[[], [1], [2], [], [], []]
输出：
[null, null, null, 2, 2, false]

解释：
MyStack myStack = new MyStack();
myStack.push(1);
myStack.push(2);
myStack.top(); // 返回 2
myStack.pop(); // 返回 2
myStack.empty(); // 返回 False
```

```c++
class MyStack {
public:
    queue<int>que,que1;
    MyStack() {

    }
    
    void push(int x) {
        que.push(x);
    }
    
    int pop() {
        int count=que.size()-1;
        while(count--){
            que1.push(que.front());
            que.pop();
        }
        int ans=que.front();
        que.pop();
        swap(que,que1);
        return ans;
    }
    
    int top() {
        int ans=pop();
        que.push(ans);
        return ans;
    }
    
    bool empty() {
        if(que.empty()&&que1.empty()){
            return true;
        }
        return false;
    }
};
```

#### 155. 最小栈

设计一个支持 `push` ，`pop` ，`top` 操作，并能在常数时间内检索到最小元素的栈。

实现 `MinStack` 类:

- `MinStack()` 初始化堆栈对象。
- `void push(int val)` 将元素val推入堆栈。
- `void pop()` 删除堆栈顶部的元素。
- `int top()` 获取堆栈顶部的元素。
- `int getMin()` 获取堆栈中的最小元素。

 

**示例 1:**

```
输入：
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

输出：
[null,null,null,null,-3,null,0,-2]

解释：
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.getMin();   --> 返回 -2.
```

```c++
class MinStack {
public:
    stack<int>stk1;
    stack<int>stk2;
    MinStack() {

    }
    
    void push(int val) {
        if(stk1.empty()){
            stk1.push(val);
            stk2.push(val);
        }
        else{
            stk1.push(val);
            if(stk2.top()>val){
                stk2.push(val);
            }
            else{
                stk2.push(stk2.top());
            }
        }
    }
    
    void pop() {
        if(stk1.empty()){
            return ;
        }
        stk1.pop();
        stk2.pop();
    }
    
    int top() {
        if(stk1.empty()){
            return -1;
        }
        return stk1.top();
    }
    
    int getMin() {
        if(stk1.empty()){
            return -1;
        }
        return stk2.top();
    }
};

```



#### 20. 有效的括号

给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串 s ，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。


示例 1：

```
输入：s = "()"
输出：true
示例 2：

输入：s = "()[]{}"
输出：true
示例 3：

输入：s = "(]"
输出：false
示例 4：

输入：s = "([)]"
输出：false
示例 5：

输入：s = "{[]}"
输出：true
```



```c++
class Solution {
public:
    bool isValid(string s) {
        stack<char>stk;
        for(auto ch:s){
            if(ch=='('){
                stk.push(')');
            }
            else if(ch=='['){
                stk.push(']');

            }
            else if(ch=='{'){
                stk.push('}');
            }
            else if(stk.empty() || stk.top()!=ch){
                return false;
            }
            else{
                stk.pop();
            }
            
        }
        if(!stk.empty()){
            return false;
        }
        return true;
    }
};
```

#### 1047. 删除字符串中的所有相邻重复项

给出由小写字母组成的字符串 S，重复项删除操作会选择两个相邻且相同的字母，并删除它们。

在 S 上反复执行重复项删除操作，直到无法继续删除。

在完成所有重复项删除操作后返回最终的字符串。答案保证唯一。

示例：

```
输入："abbaca"
输出："ca"
```

解释：
例如，在 "abbaca" 中，我们可以删除 "bb" 由于两字母相邻且相同，这是此时唯一可以执行删除操作的重复项。之后我们得到字符串 "aaca"，其中又只有 "aa" 可以执行重复项删除操作，所以最后的字符串为 "ca"。

```c++
class Solution {
public:
    string removeDuplicates(string s) {
        string st="";
        for(char c:s){
            if(st.empty() ||c!=st.back()){
                st+=c;
            }
            else{
                st.pop_back();
            }
        }
        return st;
    }
};
```

#### 150. 逆波兰表达式求值

**说明：**

- 整数除法只保留整数部分。
- 给定逆波兰表达式总是有效的。换句话说，表达式总会得出有效数值且不存在除数为 0 的情况。

 

**示例 1：**

```
输入：tokens = ["2","1","+","3","*"]
输出：9
解释：该算式转化为常见的中缀算术表达式为：((2 + 1) * 3) = 9
```

**示例 2：**

```
输入：tokens = ["4","13","5","/","+"]
输出：6
解释：该算式转化为常见的中缀算术表达式为：(4 + (13 / 5)) = 6
```

**示例 3：**

```
输入：tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
输出：22
解释：
该算式转化为常见的中缀算术表达式为：
  ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```

```c++
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int>stk;
        for(auto s:tokens){
            if(s=="+" ||s=="-" || s=="*" || s=="/"){
                int num1=stk.top();
                stk.pop();
                int num2=stk.top();
                stk.pop();
                if(s=="+"){
                    stk.push(num1+num2);
                }
                else if(s=="-"){
                    stk.push(num2-num1);
                }
                else if(s=="*"){
                    stk.push(num2*num1);
                }
                else if(s=="/"){
                    stk.push(num2/num1);
                }
            }
            else{
                stk.push(stoi(s));
            }
        }
        return stk.top();
    }
};
```

#### >>239. 滑动窗口最大值

给你一个整数数组 `nums`，有一个大小为 `k` 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 `k` 个数字。滑动窗口每次只向右移动一位。

返回滑动窗口中的最大值。

 

**示例 1：**

```
输入：nums = [1,3,-1,-3,5,3,6,7], k = 3
输出：[3,3,5,5,6,7]
解释：
滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

**示例 2：**

```
输入：nums = [1], k = 1
输出：[1]
```

**示例 3：**

```
输入：nums = [1,-1], k = 1
输出：[1,-1]
```

**示例 4：**

```
输入：nums = [9,11], k = 2
输出：[11]
```

**示例 5：**

```c++
输入：nums = [4,-2], k = 2
输出：[4]
```

```c++
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        vector<int>ans;
        priority_queue<pair<int,int>>que;
        for(int i=0;i<nums.size();i++){
            if(i<k-1){
                que.emplace(nums[i],i);
                continue;
            }
            que.emplace(nums[i],i);
            while(que.top().second<=i-k){
                que.pop();
            }
            ans.push_back(que.top().first);
        }
        return ans;
    }
};
```

#### 347. 前 K 个高频元素

难度中等959收藏分享切换为英文接收动态反馈

给你一个整数数组 `nums` 和一个整数 `k` ，请你返回其中出现频率前 `k` 高的元素。你可以按 **任意顺序** 返回答案。

 

**示例 1:**

```
输入: nums = [1,1,1,2,2,3], k = 2
输出: [1,2]
```

**示例 2:**

```
输入: nums = [1], k = 1
输出: [1]
```

```c++
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int,int>hashtable;
        priority_queue<pair<int,int>>que;
        vector<int>ans;
        for(auto i:nums){
            hashtable[i]++;
        }    
        for(auto p:hashtable){
            que.emplace(p.second,p.first);
        }
        while(k--){
            ans.push_back(que.top().second);
            que.pop();
        }
        return ans;
    }
};
```

## 贪心算法

#### 455.分发饼干

假设你是一位很棒的家长，想要给你的孩子们一些小饼干。但是，每个孩子最多只能给一块饼干。

对每个孩子 `i`，都有一个胃口值 `g[i]`，这是能让孩子们满足胃口的饼干的最小尺寸；并且每块饼干 `j`，都有一个尺寸 `s[j]` 。如果 `s[j] >= g[i]`，我们可以将这个饼干 `j` 分配给孩子 `i` ，这个孩子会得到满足。你的目标是尽可能满足越多数量的孩子，并输出这个最大数值。

**示例 1:**

```
输入: g = [1,2,3], s = [1,1]
输出: 1
解释: 
你有三个孩子和两块小饼干，3个孩子的胃口值分别是：1,2,3。
虽然你有两块小饼干，由于他们的尺寸都是1，你只能让胃口值是1的孩子满足。
所以你应该输出1。
```

**示例 2:**

```
输入: g = [1,2], s = [1,2,3]
输出: 2
解释: 
你有两个孩子和三块小饼干，2个孩子的胃口值分别是1,2。
你拥有的饼干数量和尺寸都足以让所有孩子满足。
所以你应该输出2.
```

```c++
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        sort(g.begin(),g.end());
        sort(s.begin(),s.end());
        int count=0;
        for(int i=0;i<s.size();i++){
            if(s[i]>=g[count]){
                count++;
            }
            if(count>=g.size()){
                break;
            }
        }
        return count;
    }
};
```

#### 376. 摆动序列

如果连续数字之间的差严格地在正数和负数之间交替，则数字序列称为 **摆动序列 。**第一个差（如果存在的话）可能是正数或负数。仅有一个元素或者含两个不等元素的序列也视作摆动序列。

- 例如， `[1, 7, 4, 9, 2, 5]` 是一个 **摆动序列** ，因为差值 `(6, -3, 5, -7, 3)` 是正负交替出现的。
- 相反，`[1, 4, 7, 2, 5]` 和 `[1, 7, 4, 5, 5]` 不是摆动序列，第一个序列是因为它的前两个差值都是正数，第二个序列是因为它的最后一个差值为零。

**子序列** 可以通过从原始序列中删除一些（也可以不删除）元素来获得，剩下的元素保持其原始顺序。

给你一个整数数组 `nums` ，返回 `nums` 中作为 **摆动序列** 的 **最长子序列的长度** 。

 

**示例 1：**

```
输入：nums = [1,7,4,9,2,5]
输出：6
解释：整个序列均为摆动序列，各元素之间的差值为 (6, -3, 5, -7, 3) 。
```

**示例 2：**

```
输入：nums = [1,17,5,10,13,15,10,5,16,8]
输出：7
解释：这个序列包含几个长度为 7 摆动序列。
其中一个是 [1, 17, 10, 13, 10, 16, 8] ，各元素之间的差值为 (16, -7, 3, -3, 6, -8) 。
```

**示例 3：**

```
输入：nums = [1,2,3,4,5,6,7,8,9]
输出：2
```

```c++
class Solution {
public:
    int wiggleMaxLength(vector<int>& nums) {
        int count=1;
        int pre=0;
        for(int i=1;i<nums.size();i++){
            if(pre>=0&&nums[i]-nums[i-1]<0 || pre<=0&&nums[i]-nums[i-1]>0){
                pre=nums[i]-nums[i-1];
                count++;
            }
        }
        return count;
    }
};
```

#### 53. 最大子数组和

给你一个整数数组 `nums` ，请你找出一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

**子数组** 是数组中的一个连续部分。

**示例 1：**

```
输入：nums = [-2,1,-3,4,-1,2,1,-5,4]
输出：6
解释：连续子数组 [4,-1,2,1] 的和最大，为 6 。
```

**示例 2：**

```
输入：nums = [1]
输出：1
```

**示例 3：**

```
输入：nums = [5,4,-1,7,8]
输出：23
```

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        if(nums.size()==0){
            return 0;
        }
        vector<int>dp(nums.size(),0);
        int ans=nums[0];
        dp[0]=nums[0];
        for(int i=1;i<nums.size();i++){
            dp[i]=max(nums[i],dp[i-1]+nums[i]);
            ans=max(ans,dp[i]);
        }
        return ans;
    }
};
```

#### 122. 买卖股票的最佳时机 II

给定一个数组 `prices` ，其中 `prices[i]` 是一支给定股票第 `i` 天的价格。

设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。

**注意：**你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

 

**示例 1:**

```
输入: prices = [7,1,5,3,6,4]
输出: 7
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 。
```

**示例 2:**

```
输入: prices = [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
```

**示例 3:**

```
输入: prices = [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        vector<vector<int>>dp(prices.size(),vector<int>(2));
        dp[0][0]=-prices[0];
        dp[0][1]=0;
        for(int i=1;i<prices.size();i++){
            dp[i][0]=max(dp[i-1][0],dp[i-1][1]-prices[i]);
            dp[i][1]=max(dp[i-1][1],dp[i-1][0]+prices[i]);
        }
        return dp[prices.size()-1][1];
    }
};
```

#### 55. 跳跃游戏

给定一个非负整数数组 `nums` ，你最初位于数组的 **第一个下标** 。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

判断你是否能够到达最后一个下标。

 

**示例 1：**

```
输入：nums = [2,3,1,1,4]
输出：true
解释：可以先跳 1 步，从下标 0 到达下标 1, 然后再从下标 1 跳 3 步到达最后一个下标。
```

**示例 2：**

```
输入：nums = [3,2,1,0,4]
输出：false
解释：无论怎样，总会到达下标为 3 的位置。但该下标的最大跳跃长度是 0 ， 所以永远不可能到达最后一个下标。
```

```c++
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int pre=0;
        for(int i=0;i<nums.size();i++){
            pre=max(pre,i+nums[i]);
            if(i==pre&&nums[i]==0&&i!=nums.size()-1){
                return false;
            }
        }
        return true;
    }
};
```

#### 45. 跳跃游戏 II

给你一个非负整数数组 `nums` ，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

你的目标是使用最少的跳跃次数到达数组的最后一个位置。

假设你总是可以到达数组的最后一个位置。

 

**示例 1:**

```
输入: nums = [2,3,1,1,4]
输出: 2
解释: 跳到最后一个位置的最小跳跃数是 2。
     从下标为 0 跳到下标为 1 的位置，跳 1 步，然后跳 3 步到达数组的最后一个位置。
```

**示例 2:**

```
输入: nums = [2,3,0,1,4]
输出: 2
```

```c++
class Solution {
public:
    int jump(vector<int>& nums) {
        int count=0;
        int pre=0;
        int cur=0;
        for(int i=0;i<nums.size();i++){
            cur=max(cur,i+nums[i]);

            if(i==pre&&i!=nums.size()-1){
                count++;
                pre=cur;
            }
        }
        return count;
    }
};
```

#### 1005. K 次取反后最大化的数组和

给你一个整数数组 `nums` 和一个整数 `k` ，按以下方法修改该数组：

- 选择某个下标 `i` 并将 `nums[i]` 替换为 `-nums[i]` 。

重复这个过程恰好 `k` 次。可以多次选择同一个下标 `i` 。

以这种方式修改数组后，返回数组 **可能的最大和** 。

 

**示例 1：**

```
输入：nums = [4,2,3], k = 1
输出：5
解释：选择下标 1 ，nums 变为 [4,-2,3] 。
```

**示例 2：**

```
输入：nums = [3,-1,0,2], k = 3
输出：6
解释：选择下标 (1, 2, 2) ，nums 变为 [3,1,0,2] 。
```

**示例 3：**

```
输入：nums = [2,-3,-1,5,-4], k = 2
输出：13
解释：选择下标 (1, 4) ，nums 变为 [2,3,-1,5,4] 。
```

```c++
class Solution {
public:
    int largestSumAfterKNegations(vector<int>& nums, int k) {
        sort(nums.begin(),nums.end());
        int sum=0;
        for(int i=0;i<nums.size();i++){
            if(nums[i]<0&&k>0){
                k--;
                nums[i]*=-1;
            }
            sum+=nums[i];
        }
        if(k%2==0){
            return sum;
        }
        sort(nums.begin(),nums.end());
        return sum-=2*nums[0];
    }
};
```

#### >>135. 分发糖果

`n` 个孩子站成一排。给你一个整数数组 `ratings` 表示每个孩子的评分。

你需要按照以下要求，给这些孩子分发糖果：

- 每个孩子至少分配到 `1` 个糖果。
- 相邻两个孩子评分更高的孩子会获得更多的糖果。

请你给每个孩子分发糖果，计算并返回需要准备的 **最少糖果数目** 。

 

**示例 1：**

```
输入：ratings = [1,0,2]
输出：5
解释：你可以分别给第一个、第二个、第三个孩子分发 2、1、2 颗糖果。
```

**示例 2：**

```
输入：ratings = [1,2,2]
输出：4
解释：你可以分别给第一个、第二个、第三个孩子分发 1、2、1 颗糖果。
     第三个孩子只得到 1 颗糖果，这满足题面中的两个条件。
```

```c++
class Solution {
public:
     int candy(vector<int>& ratings) {
        vector<int> candyVec(ratings.size(), 1);
        for (int i = 1; i < ratings.size(); i++) {
            if (ratings[i] > ratings[i - 1]) candyVec[i] = candyVec[i - 1] + 1;
        }
        for (int i = ratings.size() - 2; i >= 0; i--) {
            if (ratings[i] > ratings[i + 1] ) {
                candyVec[i] = max(candyVec[i], candyVec[i + 1] + 1);
            }
        }
        int result = 0;
        for (int i = 0; i < candyVec.size(); i++) result += candyVec[i];
        return result;
    }
};

```

#### 134. 加油站

在一条环路上有 *N* 个加油站，其中第 *i* 个加油站有汽油 `gas[i]` 升。

你有一辆油箱容量无限的的汽车，从第 *i* 个加油站开往第 *i+1* 个加油站需要消耗汽油 `cost[i]` 升。你从其中的一个加油站出发，开始时油箱为空。

如果你可以绕环路行驶一周，则返回出发时加油站的编号，否则返回 -1。

**说明:** 

- 如果题目有解，该答案即为唯一答案。
- 输入数组均为非空数组，且长度相同。
- 输入数组中的元素均为非负数。

**示例 1:**

```
输入: 
gas  = [1,2,3,4,5]
cost = [3,4,5,1,2]

输出: 3

解释:
从 3 号加油站(索引为 3 处)出发，可获得 4 升汽油。此时油箱有 = 0 + 4 = 4 升汽油
开往 4 号加油站，此时油箱有 4 - 1 + 5 = 8 升汽油
开往 0 号加油站，此时油箱有 8 - 2 + 1 = 7 升汽油
开往 1 号加油站，此时油箱有 7 - 3 + 2 = 6 升汽油
开往 2 号加油站，此时油箱有 6 - 4 + 3 = 5 升汽油
开往 3 号加油站，你需要消耗 5 升汽油，正好足够你返回到 3 号加油站。
因此，3 可为起始索引。
```

```c++
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int sum=0;
        int count=0;
        for(int i=0;i<gas.size();i++){
            sum+=gas[i]-cost[i];
        }
        if(sum<0){
            return -1;
        }
        sum=0;
        for(int i=0;i<gas.size();i++){
            sum+=gas[i]-cost[i];
            if(sum<0){
                sum=0;
                count=i+1;
            }
        }    
        return count;
    }
};
```

#### 860. 柠檬水找零

在柠檬水摊上，每一杯柠檬水的售价为 `5` 美元。顾客排队购买你的产品，（按账单 `bills` 支付的顺序）一次购买一杯。

每位顾客只买一杯柠檬水，然后向你付 `5` 美元、`10` 美元或 `20` 美元。你必须给每个顾客正确找零，也就是说净交易是每位顾客向你支付 `5` 美元。

注意，一开始你手头没有任何零钱。

给你一个整数数组 `bills` ，其中 `bills[i]` 是第 `i` 位顾客付的账。如果你能给每位顾客正确找零，返回 `true` ，否则返回 `false` 。

 

**示例 1：**

```
输入：bills = [5,5,5,10,20]
输出：true
解释：
前 3 位顾客那里，我们按顺序收取 3 张 5 美元的钞票。
第 4 位顾客那里，我们收取一张 10 美元的钞票，并返还 5 美元。
第 5 位顾客那里，我们找还一张 10 美元的钞票和一张 5 美元的钞票。
由于所有客户都得到了正确的找零，所以我们输出 true。
```

**示例 2：**

```
输入：bills = [5,5,10,10,20]
输出：false
解释：
前 2 位顾客那里，我们按顺序收取 2 张 5 美元的钞票。
对于接下来的 2 位顾客，我们收取一张 10 美元的钞票，然后返还 5 美元。
对于最后一位顾客，我们无法退回 15 美元，因为我们现在只有两张 10 美元的钞票。
由于不是每位顾客都得到了正确的找零，所以答案是 false。
```

```c++
class Solution {
public:
    bool lemonadeChange(vector<int>& bills) {
        unordered_map<int,int>hashtable;
        for(int i=0;i<bills.size();i++){
            if(bills[i]==5){
                hashtable[5]++;
            }
            else if(bills[i]==10){
                hashtable[5]--;
                hashtable[10]++;
            }
            else{
                if(hashtable.find(10)!=hashtable.end()){
                    hashtable[10]--;
                    hashtable[5]--;
                }
                else{
                    hashtable[5]-=3;
                }
            }
            if(hashtable[5]<0){
                return false;
            }
            if(hashtable[5]==0){
                hashtable.erase(5);
            }
            if(hashtable[10]==0){
                hashtable.erase(10);
            }
        }
        return true;
    }
};
```

#### 406. 根据身高重建队列

假设有打乱顺序的一群人站成一个队列，数组 `people` 表示队列中一些人的属性（不一定按顺序）。每个 `people[i] = [hi, ki]` 表示第 `i` 个人的身高为 `hi` ，前面 **正好** 有 `ki` 个身高大于或等于 `hi` 的人。

请你重新构造并返回输入数组 `people` 所表示的队列。返回的队列应该格式化为数组 `queue` ，其中 `queue[j] = [hj, kj]` 是队列中第 `j` 个人的属性（`queue[0]` 是排在队列前面的人）。

**示例 1：**

```
输入：people = [[7,0],[4,4],[7,1],[5,0],[6,1],[5,2]]
输出：[[5,0],[7,0],[5,2],[6,1],[4,4],[7,1]]
解释：
编号为 0 的人身高为 5 ，没有身高更高或者相同的人排在他前面。
编号为 1 的人身高为 7 ，没有身高更高或者相同的人排在他前面。
编号为 2 的人身高为 5 ，有 2 个身高更高或者相同的人排在他前面，即编号为 0 和 1 的人。
编号为 3 的人身高为 6 ，有 1 个身高更高或者相同的人排在他前面，即编号为 1 的人。
编号为 4 的人身高为 4 ，有 4 个身高更高或者相同的人排在他前面，即编号为 0、1、2、3 的人。
编号为 5 的人身高为 7 ，有 1 个身高更高或者相同的人排在他前面，即编号为 1 的人。
因此 [[5,0],[7,0],[5,2],[6,1],[4,4],[7,1]] 是重新构造后的队列。
```

**示例 2：**

```
输入：people = [[6,0],[5,0],[4,0],[3,2],[2,2],[1,4]]
输出：[[4,0],[5,0],[2,2],[3,2],[1,4],[6,0]]
```

```c++
class Solution {
public:
    static bool cmp(vector<int>&a,vector<int>&b){
        if(a[0]==b[0]){
            return a[1]<b[1];
        }
        return a[0]>b[0];
    }
    vector<vector<int>> reconstructQueue(vector<vector<int>>& people) {
        sort(people.begin(),people.end(),cmp);
        vector<vector<int>>ans;
        for(int i=0;i<people.size();i++){
            ans.insert(ans.begin()+people[i][1],people[i]);
        }
        return ans;
    }
};
```

#### 452. 用最少数量的箭引爆气球

在二维空间中有许多球形的气球。对于每个气球，提供的输入是水平方向上，气球直径的开始和结束坐标。由于它是水平的，所以纵坐标并不重要，因此只要知道开始和结束的横坐标就足够了。开始坐标总是小于结束坐标。

一支弓箭可以沿着 x 轴从不同点完全垂直地射出。在坐标 x 处射出一支箭，若有一个气球的直径的开始和结束坐标为 `x``start`，`x``end`， 且满足  `xstart ≤ x ≤ x``end`，则该气球会被引爆。可以射出的弓箭的数量没有限制。 弓箭一旦被射出之后，可以无限地前进。我们想找到使得所有气球全部被引爆，所需的弓箭的最小数量。

给你一个数组 `points` ，其中 `points [i] = [xstart,xend]` ，返回引爆所有气球所必须射出的最小弓箭数。

**示例 1：**

```
输入：points = [[10,16],[2,8],[1,6],[7,12]]
输出：2
解释：对于该样例，x = 6 可以射爆 [2,8],[1,6] 两个气球，以及 x = 11 射爆另外两个气球
```

**示例 2：**

```
输入：points = [[1,2],[3,4],[5,6],[7,8]]
输出：4
```

```c++
class Solution {
public:
    static bool cmp(vector<int>&a,vector<int>&b){
        return a[0]<b[0];
    }
    int findMinArrowShots(vector<vector<int>>& points) {
        sort(points.begin(),points.end(),cmp);
        int ans=0;
        for(int i=1;i<points.size();i++){
            if(points[i][0]<=points[i-1][1]){
                ans++;
                points[i][1]=min(points[i-1][1],points[i][1]);
            }
        }

        return points.size()-ans;
    }
};
```

#### 435. 无重叠区间

给定一个区间的集合，找到需要移除区间的最小数量，使剩余区间互不重叠。

**注意:**

1. 可以认为区间的终点总是大于它的起点。
2. 区间 [1,2] 和 [2,3] 的边界相互“接触”，但没有相互重叠。

**示例 1:**

```
输入: [ [1,2], [2,3], [3,4], [1,3] ]

输出: 1

解释: 移除 [1,3] 后，剩下的区间没有重叠。
```

**示例 2:**

```
输入: [ [1,2], [1,2], [1,2] ]

输出: 2

解释: 你需要移除两个 [1,2] 来使剩下的区间没有重叠。
```

```c++
class Solution {
public:
    static bool cmp(vector<int>&a,vector<int>&b){
        return a[1]<b[1];
    }
    int eraseOverlapIntervals(vector<vector<int>>& intervals) {
        sort(intervals.begin(),intervals.end(),cmp);
        int count=1;
        int end=intervals[0][1];
        for(int i=0;i<intervals.size();i++){
            if(end<=intervals[i][0]){
                count++;
                end=intervals[i][1];
            }
        }
        return intervals.size()-count;
    }
};
```

#### 763. 划分字母区间

字符串 `S` 由小写字母组成。我们要把这个字符串划分为尽可能多的片段，同一字母最多出现在一个片段中。返回一个表示每个字符串片段的长度的列表。

**示例：**

```
输入：S = "ababcbacadefegdehijhklij"
输出：[9,7,8]
解释：
划分结果为 "ababcbaca", "defegde", "hijhklij"。
每个字母最多出现在一个片段中。
像 "ababcbacadefegde", "hijhklij" 的划分是错误的，因为划分的片段数较少。
```

```c++
class Solution {
public:
    vector<int> partitionLabels(string s) {
        vector<int>ans;
        int pre=0;
        int hash[26]={0};
        int max_count=0;
        for(int i=0;i<s.size();i++){
            hash[s[i]-'a']=i;
        }
        for(int i=0;i<s.size();i++){
            max_count=max(max_count,hash[s[i]-'a']);
            if(i==max_count){
                ans.push_back(i-pre+1);
                pre=i+1;
            }
        }
        return ans;
    }
};
```

#### 56. 合并区间

以数组 `intervals` 表示若干个区间的集合，其中单个区间为 `intervals[i] = [starti, endi]` 。请你合并所有重叠的区间，并返回一个不重叠的区间数组，该数组需恰好覆盖输入中的所有区间。

**示例 1：**

```
输入：intervals = [[1,3],[2,6],[8,10],[15,18]]
输出：[[1,6],[8,10],[15,18]]
解释：区间 [1,3] 和 [2,6] 重叠, 将它们合并为 [1,6].
```

**示例 2：**

```
输入：intervals = [[1,4],[4,5]]
输出：[[1,5]]
解释：区间 [1,4] 和 [4,5] 可被视为重叠区间。
```

```c++
class Solution {
public:
    static bool cmp(vector<int>&a,vector<int>&b){
        return a[0]<b[0];
    }
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
       vector<vector<int>>ans;
        sort(intervals.begin(),intervals.end(),cmp);
        for(int i=0;i<intervals.size()-1;i++){
            if(intervals[i+1][0]<=intervals[i][1]){
                intervals[i+1][0]=intervals[i][0];
                intervals[i+1][1]=max(intervals[i][1],intervals[i+1][1]);
            }
            else{
                ans.push_back(intervals[i]);
            }
        }
        ans.push_back(intervals[intervals.size()-1]);
        return ans;
    }
};
```

#### 738. 单调递增的数字

给定一个非负整数 `N`，找出小于或等于 `N` 的最大的整数，同时这个整数需要满足其各个位数上的数字是单调递增。

（当且仅当每个相邻位数上的数字 `x` 和 `y` 满足 `x <= y` 时，我们称这个整数是单调递增的。）

**示例 1:**

```
输入: N = 10
输出: 9
```

**示例 2:**

```
输入: N = 1234
输出: 1234
```

**示例 3:**

```
输入: N = 332
输出: 299
```

```c++
class Solution {
public:
    int monotoneIncreasingDigits(int n) {
        string str=to_string(n);
        int count=str.size();
        for(int i=str.size()-1;i>0;i--){
            if(str[i]<str[i-1]){
                str[i-1]--;
                count=i;
            }
        }
        for(int i=count;i<str.size();i++){
            str[i]='9';
        }
        return stoi(str);

    }
};
```

#### 714. 买卖股票的最佳时机含手续费

给定一个整数数组 `prices`，其中第 `i` 个元素代表了第 `i` 天的股票价格 ；整数 `fee` 代表了交易股票的手续费用。

你可以无限次地完成交易，但是你每笔交易都需要付手续费。如果你已经购买了一个股票，在卖出它之前你就不能再继续购买股票了。

返回获得利润的最大值。

**注意：**这里的一笔交易指买入持有并卖出股票的整个过程，每笔交易你只需要为支付一次手续费。 

**示例 1：**

```
输入：prices = [1, 3, 2, 8, 4, 9], fee = 2
输出：8
解释：能够达到的最大利润:  
在此处买入 prices[0] = 1
在此处卖出 prices[3] = 8
在此处买入 prices[4] = 4
在此处卖出 prices[5] = 9
总利润: ((8 - 1) - 2) + ((9 - 4) - 2) = 8
```

**示例 2：**

```
输入：prices = [1,3,7,5,10,3], fee = 3
输出：6
```

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices, int fee) {
        int ans=0;
        int min_price=INT_MAX;
        for(int i=0;i<prices.size();i++){
            min_price=min(min_price,prices[i]);
            if(prices[i]-min_price-fee<=0){
                continue;
            }
            else{
                ans+=prices[i]-min_price-fee;
                min_price=prices[i]-fee;
            }
        }
        return ans;
    }
};
```

#### >>968. 监控二叉树

难度困难413收藏分享切换为英文接收动态反馈

给定一个二叉树，我们在树的节点上安装摄像头。

节点上的每个摄影头都可以监视**其父对象、自身及其直接子对象。**

计算监控树的所有节点所需的最小摄像头数量。

 

**示例 1：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/29/bst_cameras_01.png)

```c++
输入：[0,0,null,0,0]
输出：1
解释：如图所示，一台摄像头足以监控所有节点。
```

**示例 2：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/29/bst_cameras_02.png)

```c++
输入：[0,0,null,0,null,0,null,null,0]
输出：2
解释：需要至少两个摄像头来监视树的所有节点。 上图显示了摄像头放置的有效位置之一。
```

```c++

```

#### >>649. Dota2 参议院

Dota2 的世界里有两个阵营：`Radiant`(天辉)和 `Dire`(夜魇)

Dota2 参议院由来自两派的参议员组成。现在参议院希望对一个 Dota2 游戏里的改变作出决定。他们以一个基于轮为过程的投票进行。在每一轮中，每一位参议员都可以行使两项权利中的`**一**`项：

1. `禁止一名参议员的权利`：

   参议员可以让另一位参议员在这一轮和随后的几轮中丧失**所有的权利**。

2. `宣布胜利`：

​     如果参议员发现有权利投票的参议员都是**同一个阵营的**，他可以宣布胜利并决定在游戏中的有关变化。

 

给定一个字符串代表每个参议员的阵营。字母 “R” 和 “D” 分别代表了 `Radiant`（天辉）和 `Dire`（夜魇）。然后，如果有 `n` 个参议员，给定字符串的大小将是 `n`。

以轮为基础的过程从给定顺序的第一个参议员开始到最后一个参议员结束。这一过程将持续到投票结束。所有失去权利的参议员将在过程中被跳过。

假设每一位参议员都足够聪明，会为自己的政党做出最好的策略，你需要预测哪一方最终会宣布胜利并在 Dota2 游戏中决定改变。输出应该是 `Radiant` 或 `Dire`。

 

**示例 1：**

```
输入："RD"
输出："Radiant"
解释：第一个参议员来自 Radiant 阵营并且他可以使用第一项权利让第二个参议员失去权力，因此第二个参议员将被跳过因为他没有任何权利。然后在第二轮的时候，第一个参议员可以宣布胜利，因为他是唯一一个有投票权的人
```

**示例 2：**

```
输入："RDD"
输出："Dire"
解释：
第一轮中,第一个来自 Radiant 阵营的参议员可以使用第一项权利禁止第二个参议员的权利
第二个来自 Dire 阵营的参议员会被跳过因为他的权利被禁止
第三个来自 Dire 阵营的参议员可以使用他的第一项权利禁止第一个参议员的权利
因此在第二轮只剩下第三个参议员拥有投票的权利,于是他可以宣布胜利
```

```c++
class Solution {
public:
    string predictPartyVictory(string senate) {
        bool R=true;
        bool D=true;
        int flag=0;
        while(R&&D){
            R=false;
            D=false;
            for(int i=0;i<senate.size();i++){
                if(senate[i]=='R'){
                    if(flag<0){
                        senate[i]='0';
                    }
                    else{
                        R=true;
                    }
                    flag++;
                }
                if(senate[i]=='D'){
                    if(flag>0){
                        senate[i]='0';
                    }
                    else{
                        D=true;
                    }
                    flag--;
                }
            }
        }
        return R==true?"Radiant":"Dire";
    }
};
```

#### 1221. 分割平衡字符串

在一个 **平衡字符串** 中，`'L'` 和 `'R'` 字符的数量是相同的。

给你一个平衡字符串 `s`，请你将它分割成尽可能多的平衡字符串。

**注意：**分割得到的每个字符串都必须是平衡字符串，且分割得到的平衡字符串是原平衡字符串的连续子串。

返回可以通过分割得到的平衡字符串的 **最大数量** **。**

**示例 1：**

```
输入：s = "RLRRLLRLRL"
输出：4
解释：s 可以分割为 "RL"、"RRLL"、"RL"、"RL" ，每个子字符串中都包含相同数量的 'L' 和 'R' 。
```

**示例 2：**

```
输入：s = "RLLLLRRRLR"
输出：3
解释：s 可以分割为 "RL"、"LLLRRR"、"LR" ，每个子字符串中都包含相同数量的 'L' 和 'R' 。
```

**示例 3：**

```
输入：s = "LLLLRRRR"
输出：1
解释：s 只能保持原样 "LLLLRRRR".
```

**示例 4：**

```
输入：s = "RLRRRLLRLL"
输出：2
解释：s 可以分割为 "RL"、"RRRLLRLL" ，每个子字符串中都包含相同数量的 'L' 和 'R' 。
```

```c++
class Solution {
public:
    int balancedStringSplit(string s) {
        int flag=0;
        int count=0;
        for(int i=0;i<s.size();i++){
            if(s[i]=='R'){
                flag++;
                if(flag==0){
                    count++;
                }
            }
            if(s[i]=='L'){
                flag--;
                if(flag==0){
                    count++;
                }
            }
        }
        return count;
    }
};
```



## 二叉树

#### 144. 二叉树的前序遍历

给你二叉树的根节点 `root` ，返回它节点值的 **前序** 遍历。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

```c++
输入：root = [1,null,2,3]
输出：[1,2,3]
```

**示例 2：**

```c++
输入：root = []
输出：[]
```

```c++
//递归
class Solution {
public:
    void func(TreeNode*tr,vector<int>&vc){
        if(tr==NULL){
            return;
        }
        vc.push_back(tr->val);
        func(tr->left,vc);
        func(tr->right,vc);
    }
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int>ans;
        func(root,ans);
        return ans;        
    }
};
//迭代
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        stack<TreeNode*>st;
        st.push(root); 
        vector<int>ans;
        if(root==NULL){
            return ans;
        }
        while(!st.empty()){
            TreeNode* pre=st.top();
            ans.push_back(pre->val);
            st.pop();
            if(pre->right){
                st.push(pre->right);
            }
            if(pre->left){
                st.push(pre->left);
            }

        } 
        return ans;   
    }
};
```

#### 145. 二叉树的后序遍历

给定一个二叉树，返回它的 *后序* 遍历。

**示例:**

```
输入: [1,null,2,3]  
   1
    \
     2
    /
   3 

输出: [3,2,1]
```

```c++
//递归
class Solution {
public:
    void func(TreeNode*tr,vector<int>&vc){
        if(tr==NULL){
            return ;
        }
        func(tr->left,vc);
        func(tr->right,vc);
        vc.push_back(tr->val);
    }
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int>ans;
        func(root,ans);
        return ans;
    }
};
//迭代
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        stack<TreeNode*>st;
        vector<int>vc;
        if (root == NULL) return vc;
        st.push(root);
        while(!st.empty()){
            TreeNode*tr=st.top();
            st.pop();
            vc.push_back(tr->val);
            if(tr->left){
                st.push(tr->left);
            }
            if(tr->right){
                st.push(tr->right);
            }
        }
        reverse(vc.begin(),vc.end());
        return vc;
    }
};
```

#### >>94. 二叉树的中序遍历

给定一个二叉树的根节点 `root` ，返回它的 **中序** 遍历。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

```
输入：root = [1,null,2,3]
输出：[1,3,2]
```

```c++
//递归
class Solution {
public:
    void func(TreeNode*tr,vector<int>&vc){
        if(tr==NULL){
            return;
        }
        func(tr->left,vc);
        vc.push_back(tr->val);
        func(tr->right,vc);
    }
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int>ans;
        func(root,ans);
        return ans;
    }
};
//迭代
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int>ans;
        stack<TreeNode*>stk;
        TreeNode*cur=root;
        while(cur!=NULL|| !stk.empty()){
            if(cur!=NULL){
                stk.push(cur);
                cur=cur->left;
            }
            else{
                cur=stk.top();
                stk.pop();
                ans.push_back(cur->val);
                cur=cur->right;
            }
        }
        return ans;
    }
};
```

#### 102. 二叉树的层序遍历

给你一个二叉树，请你返回其按 **层序遍历** 得到的节点值。 （即逐层地，从左到右访问所有节点）。

 

**示例：**
二叉树：`[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层序遍历结果：

```
[
  [3],
  [9,20],
  [15,7]
]
```

```c++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>>ans;
        queue<TreeNode*>qu;
        if(root==NULL){
            return ans;
        }
        qu.push(root);
        while(!qu.empty()){
            int count=qu.size();
            vector<int>vc;
            for(int i=0;i<count;i++){
                TreeNode*pre=qu.front();
                vc.push_back(pre->val);
                qu.pop();
                if(pre->left){
                    qu.push(pre->left);
                }
                if(pre->right){
                    qu.push(pre->right);
                }
            }
            ans.push_back(vc);
        }
        return ans;
    }
};

//递归
class Solution {
public:
    vector<vector<int>>ans;
    void func(TreeNode*root,int l){
        if(root==NULL){
            return ;
        }
        if(l>=ans.size()){
            ans.push_back({});
        }
        ans[l].push_back(root->val);
        func(root->left,l+1);
        func(root->right,l+1);
    }
    vector<vector<int>> levelOrder(TreeNode* root) {
        func(root,0);
        return ans;
    }
};
```

#### 107. 二叉树的层序遍历 II

给定一个二叉树，返回其节点值自底向上的层序遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

例如：
给定二叉树 `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其自底向上的层序遍历为：

```
[
  [15,7],
  [9,20],
  [3]
]
```

```c++
class Solution {
public:
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        vector<vector<int>>ans;
        TreeNode*cur=root;
        queue<TreeNode*>qu;
        if(root==NULL){
            return ans;
        }  
        qu.push(cur);      
        while(!qu.empty()){
            int count=qu.size();
            vector<int>vc;
            for(int i=0;i<count;i++){
                TreeNode*pre=qu.front();
                vc.push_back(pre->val);
                qu.pop();
                if(pre->left){
                    qu.push(pre->left);
                }
                if(pre->right){
                    qu.push(pre->right);
                }
            }
            ans.push_back(vc);
        }
        reverse(ans.begin(),ans.end());
        return ans;
    }
};

//递归
class Solution {
public:
    vector<vector<int>>ans;
    void func(TreeNode*root,int l){
        if(root==NULL){
            return ;
        }
        if(l>=ans.size()){
            ans.push_back({});
        }
        ans[l].push_back(root->val);
        func(root->left,l+1);
        func(root->right,l+1);
    }
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        func(root,0);
        reverse(ans.begin(),ans.end());
        return ans;
    }
};
```

#### 103. 二叉树的锯齿形层序遍历

给你二叉树的根节点 `root` ，返回其节点值的 **锯齿形层序遍历** 。（即先从左往右，再从右往左进行下一层遍历，以此类推，层与层之间交替进行）。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

```
输入：root = [3,9,20,null,null,15,7]
输出：[[3],[20,9],[15,7]]
```

**示例 2：**

```
输入：root = [1]
输出：[[1]]
```

**示例 3：**

```
输入：root = []
输出：[]
```

```c++
class Solution {
public:
    vector<vector<int>>ans;
    vector<int>v;
    void func(TreeNode*root,int l){
        if(root==NULL){
            return ;
        }
        if(l>=ans.size()){
            ans.push_back({});
        }
        ans[l].push_back(root->val);
        func(root->left,l+1);
        func(root->right,l+1);
    }
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        func(root,0);
        for(int i=0;i<ans.size();i++){
            if(i%2){
                reverse(ans[i].begin(),ans[i].end());
            }
        }
        return ans;
    }
};
```



#### 199. 二叉树的右视图

给定一个二叉树的 **根节点** `root`，想象自己站在它的右侧，按照从顶部到底部的顺序，返回从右侧所能看到的节点值。

 

**示例 1:**

![img](https://assets.leetcode.com/uploads/2021/02/14/tree.jpg)

```
输入: [1,2,3,null,5,null,4]
输出: [1,3,4]
```

**示例 2:**

```
输入: [1,null,3]
输出: [1,3]
```

**示例 3:**

```
输入: []
输出: []
```

```c++
class Solution {
public:
    vector<int> rightSideView(TreeNode* root) {
        vector<int>ans;
        queue<TreeNode*>qu;
        if(root==NULL){
            return ans;
        }
        qu.push(root);
        while(!qu.empty()){
            int count=qu.size();
            for(int i=0;i<count;i++){
                TreeNode*pre=qu.front();
                qu.pop();
                if(i==count-1){
                    ans.push_back(pre->val);
                }
                if(pre->left){
                    qu.push(pre->left);
                }
                if(pre->right){
                    qu.push(pre->right);
                }
            }
        }
        return ans;
    }
};

//递归
class Solution {
public:
    vector<vector<int>>ans;
    void func(TreeNode*root,int l){
        if(root==NULL){
            return ;
        }
        if(l>=ans.size()){
            ans.push_back({});
        }
        ans[l].push_back(root->val);
        func(root->left,l+1);
        func(root->right,l+1);
    }
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        func(root,0);
        reverse(ans.begin(),ans.end());
        return ans;
    }
};
```

#### 637. 二叉树的层平均值

给定一个非空二叉树, 返回一个由每层节点平均值组成的数组。

 

**示例 1：**

```
输入：
    3
   / \
  9  20
    /  \
   15   7
输出：[3, 14.5, 11]
解释：
第 0 层的平均值是 3 ,  第1层是 14.5 , 第2层是 11 。因此返回 [3, 14.5, 11] 。
```

```c++
class Solution {
public:
    vector<double> averageOfLevels(TreeNode* root) {
        queue<TreeNode*>qu;
        vector<double>vc;
        if(root==NULL){
            return vc;
        }
        qu.push(root);
        while(!qu.empty()){
            int _size=qu.size();
            double sum=0;
            for(int i=0;i<_size;i++){
                TreeNode*tr=qu.front();
                qu.pop();
                
                
                sum+=tr->val;
                
                if(tr->left){
                    qu.push(tr->left);
                }
                if(tr->right){
                    qu.push(tr->right);
                }
                
            }
           
            vc.push_back(sum/_size);
        }
        return vc;
    }
};

//递归
class Solution {
public:
    vector<double>ans;
    vector<double>count;
    void func(TreeNode*root,int l){
        if(root==NULL){
            return ;
        }
        if(l>=ans.size()){
            ans.push_back(0);
            count.push_back(0);
        }
        ans[l]+=root->val;
        count[l]++;
        func(root->left,l+1);
        func(root->right,l+1);
    }
    vector<double> averageOfLevels(TreeNode* root) {
        func(root,0);
        for(int i=0;i<ans.size();i++){
            ans[i]=ans[i]/count[i];
        }
        return ans;
    }
};
```

#### 429. N 叉树的层序遍历

给定一个 N 叉树，返回其节点值的*层序遍历*。（即从左到右，逐层遍历）。

树的序列化输入是用层序遍历，每组子节点都由 null 值分隔（参见示例）。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2018/10/12/narytreeexample.png)

```
输入：root = [1,null,3,2,4,null,5,6]
输出：[[1],[3,2,4],[5,6]]
```

```c++
class Solution {
public:
    vector<vector<int>> levelOrder(Node* root) {
        vector<vector<int>>ans;
        queue<Node*>qu;
        if(root==NULL){
            return ans;
        }
        qu.push(root);
        while(!qu.empty()){
            int count=qu.size();
            vector<int>vc;
            for(int i=0;i<count;i++){
                Node*nd=qu.front();
                vc.push_back(nd->val);
                qu.pop();
                for(int i=0;i<nd->children.size();i++){
                    if(nd->children[i]){
                        qu.push(nd->children[i]);
                    }
                }
            }
            ans.push_back(vc);
        }
        return ans;
    }
};

//递归
class Solution {
public:
    vector<vector<int>>ans;
    void func(Node*root,int l){
        if(root==NULL){
            return ;
        }
        if(l>=ans.size()){
            ans.push_back({});

        }
        ans[l].push_back(root->val);
        for(int i=0;i<root->children.size();i++){
            func(root->children[i],l+1);
        }
    }
    vector<vector<int>> levelOrder(Node* root) {
       func(root,0);
       return ans;
    }
};
```

#### 515. 在每个树行中找最大值

给定一棵二叉树的根节点 `root` ，请找出该二叉树中每一层的最大值。

 

**示例1：**

```
输入: root = [1,3,2,5,3,null,9]
输出: [1,3,9]
解释:
          1
         / \
        3   2
       / \   \  
      5   3   9 
```

**示例2：**

```
输入: root = [1,2,3]
输出: [1,3]
解释:
          1
         / \
        2   3
```



```c++
class Solution {
public:
    vector<int> largestValues(TreeNode* root) {
        vector<int>ans;
        queue<TreeNode*>qu;
        if(root==NULL){
            return ans;
        }
        qu.push(root);
        while(!qu.empty()){          
            int max_num=INT_MIN;
            int count=qu.size();
            for(int i=0;i<count;i++){
                TreeNode*tr=qu.front();
                qu.pop();
                max_num=max(max_num,tr->val);
                if(tr->left){
                    qu.push(tr->left);
                }
                if(tr->right){
                    qu.push(tr->right);
                }
            }
            
            ans.push_back(max_num);
            
        }
        return ans;
    }
};

//递归
class Solution {
public:
    vector<int>ans;
    void func(TreeNode*root,int l){
        if(root==NULL){
            return ;
        }
        if(l>=ans.size()){
            ans.push_back(INT_MIN);
        }
        ans[l]=max(ans[l],root->val);
        func(root->left,l+1);
        func(root->right,l+1);
    }
    vector<int> largestValues(TreeNode* root) {
        func(root,0);
        return ans;
    }
};

```

#### 116. 填充每个节点的下一个右侧节点指针

给定一个 **完美二叉树** ，其所有叶子节点都在同一层，每个父节点都有两个子节点。二叉树定义如下：

```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```

填充它的每个 next 指针，让这个指针指向其下一个右侧节点。如果找不到下一个右侧节点，则将 next 指针设置为 `NULL`。

初始状态下，所有 next 指针都被设置为 `NULL`。

 

**进阶：**

- 你只能使用常量级额外空间。
- 使用递归解题也符合要求，本题中递归程序占用的栈空间不算做额外的空间复杂度。

 

**示例：**

![img](https://assets.leetcode.com/uploads/2019/02/14/116_sample.png)

```
输入：root = [1,2,3,4,5,6,7]
输出：[1,#,2,3,#,4,5,6,7,#]
解释：给定二叉树如图 A 所示，你的函数应该填充它的每个 next 指针，以指向其下一个右侧节点，如图 B 所示。序列化的输出按层序遍历排列，同一层节点由 next 指针连接，'#' 标志着每一层的结束。
```

```C++
class Solution {
public:
    Node* connect(Node* root) {
        queue<Node*>qu;
        if(root==NULL){
            return root;
        }        
        qu.push(root);
        while(!qu.empty()){
            int count=qu.size();
            Node*pre;
            Node*cur;
            for(int i=0;i<count;i++){
                Node*nd=qu.front();
                qu.pop();
                if(i==0){
                    pre=nd;
                }
                else if(i<count-1){
                    pre->next=nd;
                    pre=nd;                   
                }
                else{
                    nd->next=NULL;
                    pre->next=nd;
                }
                if(nd->left){
                    qu.push(nd->left);
                }
                if(nd->right){
                    qu.push(nd->right);
                }
            }
        }
        return root;
    }
};

//递归
class Solution {
public:
    void func(Node*l,Node*r){
        if(l==NULL ){
            return;
        }
        l->next=r;
        func(l->left,l->right);
        func(l->right,r->left);
        func(r->left,r->right);

    }
    Node* connect(Node* root) {
        if(root==NULL){
            return root;
        }
        func(root->left,root->right);
        return root;
    }
};
```

#### 117. 填充每个节点的下一个右侧节点指针 II

给定一个二叉树

```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```

填充它的每个 next 指针，让这个指针指向其下一个右侧节点。如果找不到下一个右侧节点，则将 next 指针设置为 `NULL`。

初始状态下，所有 next 指针都被设置为 `NULL`。

 

**进阶：**

- 你只能使用常量级额外空间。
- 使用递归解题也符合要求，本题中递归程序占用的栈空间不算做额外的空间复杂度。

 

**示例：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/02/15/117_sample.png)

```
输入：root = [1,2,3,4,5,null,7]
输出：[1,#,2,3,#,4,5,7,#]
解释：给定二叉树如图 A 所示，你的函数应该填充它的每个 next 指针，以指向其下一个右侧节点，如图 B 所示。序列化输出按层序遍历顺序（由 next 指针连接），'#' 表示每层的末尾。
```

```C++
class Solution {
public:
    Node* connect(Node* root) {
        queue<Node*>qu;
        if(root==NULL){
            return root;
        }        
        qu.push(root);
        while(!qu.empty()){
            int count=qu.size();
            Node*pre;
            Node*cur;
            for(int i=0;i<count;i++){
                Node*nd=qu.front();
                qu.pop();
                if(i==0){
                    pre=nd;
                }
                else if(i<count-1){
                    pre->next=nd;
                    pre=nd;                   
                }
                else{
                    nd->next=NULL;
                    pre->next=nd;
                }
                if(nd->left){
                    qu.push(nd->left);
                }
                if(nd->right){
                    qu.push(nd->right);
                }
            }
        }
        return root;
    }
};

//递归
class Solution {
public:
    vector<Node*>ans;
    void func(Node*root,int l){
        if(root==NULL){
            return;
        }
        if(l>=ans.size()){
            ans.push_back(root);
        }
        else{
            ans[l]->next=root;
            ans[l]=ans[l]->next;
        }
        func(root->left,l+1);
        func(root->right,l+1);
    }
    Node* connect(Node* root) {
        func(root,0);
        return root;
    }
};
```

#### 104. 二叉树的最大深度

给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

**说明:** 叶子节点是指没有子节点的节点。

**示例：**
给定二叉树 `[3,9,20,null,null,15,7]`，

```
    3
   / \
  9  20
    /  \
   15   7
```

```C++
//递归
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(root==NULL){
            return 0;
        }
        int maxleft_len=maxDepth(root->left);
        int maxright_len=maxDepth(root->right);
        int max_len=max(maxleft_len,maxright_len);
        return max_len+1;
    }
};
//迭代
class Solution {
public:
    int maxDepth(TreeNode* root) {
        queue<TreeNode*>qu;
        int count=0;
        if(root==NULL){
            return count;
        }
        qu.push(root);
        while(!qu.empty()){
            int size=qu.size();
            count++;
            for(int i=0;i<size;i++){
                TreeNode*tr=qu.front();
                qu.pop();
                if(tr->left){
                    qu.push(tr->left);
                }
                if(tr->right){
                    qu.push(tr->right);
                }
            }
        }
        return count;
    }
};
```

#### 111. 二叉树的最小深度

给定一个二叉树，找出其最小深度。

最小深度是从根节点到最近叶子节点的最短路径上的节点数量。

**说明：**叶子节点是指没有子节点的节点。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/12/ex_depth.jpg)

```
输入：root = [3,9,20,null,null,15,7]
输出：2
```

**示例 2：**

```
输入：root = [2,null,3,null,4,null,5,null,6]
输出：5
```

```c++
//递归
class Solution {
public:
    int minDepth(TreeNode* root) {
        if(root==NULL){
            return  0;
        }
        int leftd=minDepth(root->left);
        int rightd=minDepth(root->right);
        if(root->left==NULL &&root->right!=NULL){
            return 1+rightd;
        }
        if(root->right==NULL &&root->left!=NULL){
            return 1+leftd;
        }
        int mind=min(leftd,rightd);
        return  mind+1;
    }
};
//迭代
class Solution {
public:
    int minDepth(TreeNode* root) {
         queue<TreeNode*>qu;
        int count=0;
        if(root==NULL){
            return count;
        }
        qu.push(root);
        while(!qu.empty()){
            int size=qu.size();
            
            count++;
            for(int i=0;i<size;i++){
                TreeNode*tr=qu.front();
                qu.pop();
                if(tr->left){
                    qu.push(tr->left);
                }
                if(tr->right){
                    qu.push(tr->right);
                }
                if(!tr->left && !tr->right){
                    return count;
                }
            }
        }
        return count;
    }
};
```

#### 226. 翻转二叉树

翻转一棵二叉树。

**示例：**

输入：

```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

输出：

```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

```c++
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if(root==NULL){
            return root;
        }
        swap(root->left,root->right);
        invertTree(root->left);
        invertTree(root->right);
        return root;
    }
};
```

#### 101. 对称二叉树

给定一个二叉树，检查它是否是镜像对称的。

例如，二叉树 `[1,2,2,3,4,4,3]` 是对称的。

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

但是下面这个 `[1,2,2,null,3,null,3]` 则不是镜像对称的:

```
    1
   / \
  2   2
   \   \
   3    3
```

```c++
//迭代
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        queue<TreeNode*>qu;
        if(root==NULL){
            return true;
        }
        qu.push(root->left);
        qu.push(root->right);
        while(!qu.empty()){
            TreeNode*tr1=qu.front();
            qu.pop();
            TreeNode*tr2=qu.front();
            qu.pop();
            if(tr1==NULL&&tr2==NULL){
                continue;
            }
            if(!tr1 ||!tr2 ||  tr1->val!=tr2->val){
                return false;
            }
            
            qu.push(tr1->left);
            qu.push(tr2->right);
            qu.push(tr1->right);
            qu.push(tr2->left);
            
        }
        return true;
    }
};
//递归
class Solution {
public:
    bool cmp(TreeNode*tr1,TreeNode*tr){
        if(tr1==NULL &&tr!=NULL){
            return false;
        }
        else if(tr1!=NULL &&tr==NULL){
            return false;
        }
        else if(tr1==NULL && tr==NULL){
            return true;
        }
        else if(tr1->val!=tr->val){
            return false;
        }
        bool cm=cmp(tr1->left,tr->right);
        bool cm1=cmp(tr1->right,tr->left);
        return cm&&cm1;
    }
    bool isSymmetric(TreeNode* root) {
        if(root==NULL){
            return true;
        }
        return cmp(root->left,root->right);

    }
};
```

#### [100. 相同的树](https://leetcode.cn/problems/same-tree/)

难度简单849

给你两棵二叉树的根节点 `p` 和 `q` ，编写一个函数来检验这两棵树是否相同。

如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/12/20/ex1.jpg)

```
输入：p = [1,2,3], q = [1,2,3]
输出：true
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/12/20/ex2.jpg)

```
输入：p = [1,2], q = [1,null,2]
输出：false
```

**示例 3：**

![img](https://assets.leetcode.com/uploads/2020/12/20/ex3.jpg)

```
输入：p = [1,2,1], q = [1,1,2]
输出：false
```

```c++
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if(p==NULL&&q!=NULL){
            return false;
        }
        if(p!=NULL&&q==NULL){
            return false;
        }
        if(p==NULL&&q==NULL){
            return true;
        }
        if(p->val!=q->val){
            return false;
        }
        bool l=isSameTree(p->left,q->left);
        bool r=isSameTree(p->right,q->right);
        return l&&r;
    }
};
```

#### 572. 另一棵树的子树

给你两棵二叉树 `root` 和 `subRoot` 。检验 `root` 中是否包含和 `subRoot` 具有相同结构和节点值的子树。如果存在，返回 `true` ；否则，返回 `false` 。

二叉树 `tree` 的一棵子树包括 `tree` 的某个节点和这个节点的所有后代节点。`tree` 也可以看做它自身的一棵子树。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/04/28/subtree1-tree.jpg)

```
输入：root = [3,4,5,1,2], subRoot = [4,1,2]
输出：true
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/04/28/subtree2-tree.jpg)

```
输入：root = [3,4,5,1,2,null,null,null,null,0], subRoot = [4,1,2]
输出：false
```

```c++
class Solution {
public:
    bool issame(TreeNode* root, TreeNode* subRoot){
        if(root==NULL&&subRoot!=NULL){
            return false;
        }
        if(root!=NULL&&subRoot==NULL){
            return false;
        }
        if(root==NULL&&subRoot==NULL){
            return true;
        }
        if(root->val!=subRoot->val){
            return false;
        }
        return issame(root->left,subRoot->left)&&issame(root->right,subRoot->right);
    }
    bool isSubtree(TreeNode* root, TreeNode* subRoot) {
        if(root==NULL){
            return false;
        }
        if(issame(root,subRoot)){
            return true;
        }
        bool l=isSubtree(root->left,subRoot);
        bool r=isSubtree(root->right,subRoot);
        return l ||r;
    }
};
```



#### 222. 完全二叉树的节点个数

给你一棵 **完全二叉树** 的根节点 `root` ，求出该树的节点个数。

[完全二叉树](https://baike.baidu.com/item/完全二叉树/7773232?fr=aladdin) 的定义如下：在完全二叉树中，除了最底层节点可能没填满外，其余每层节点数都达到最大值，并且最下面一层的节点都集中在该层最左边的若干位置。若最底层为第 `h` 层，则该层包含 `1~ 2h` 个节点。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/01/14/complete.jpg)

```
输入：root = [1,2,3,4,5,6]
输出：6
```

**示例 2：**

```
输入：root = []
输出：0
```

```C++
class Solution {
public:
    int countNodes(TreeNode* root) {
        if(root==NULL){
            return 0;
        }
        return countNodes(root->left)+countNodes(root->right)+1;
    }
};
```

#### 110. 平衡二叉树

给定一个二叉树，判断它是否是高度平衡的二叉树。

本题中，一棵高度平衡二叉树定义为：

> 一个二叉树*每个节点* 的左右两个子树的高度差的绝对值不超过 1 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/06/balance_1.jpg)

```
输入：root = [3,9,20,null,null,15,7]
输出：true
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/10/06/balance_2.jpg)

```
输入：root = [1,2,2,3,3,null,null,4,4]
输出：false
```

```c++
class Solution {
public:
    int func(TreeNode*root){
        if(root==NULL){
            return 0; 
        }
        return max(func(root->left),func(root->right))+1;
    }
    bool isBalanced(TreeNode* root) {
        if(root==NULL){
            return true;
        }
        return abs(func(root->left)-func(root->right))<2&&isBalanced(root->left)&&isBalanced(root->right);
    }
};
```

#### >>257. 二叉树的所有路径

给你一个二叉树的根节点 `root` ，按 **任意顺序** ，返回所有从根节点到叶子节点的路径。

**叶子节点** 是指没有子节点的节点。

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/03/12/paths-tree.jpg)

```
输入：root = [1,2,3,null,5]
输出：["1->2->5","1->3"]
```

**示例 2：**

```
输入：root = [1]
输出：["1"]
```

```c++
class Solution {
public:
    vector<string>ans;
    void func(TreeNode*root,string str)
    {
        str+=to_string(root->val);
        if(root->left==NULL&&root->right==NULL){
            ans.push_back(str);
        }
        if(root->left){
            func(root->left,str+"->");
        }
        if(root->right){
            func(root->right,str+"->");
        }
    }
    vector<string> binaryTreePaths(TreeNode* root) {
        func(root,"");
        return ans;
    }
};

```

#### >>404. 左叶子之和

计算给定二叉树的所有左叶子之和。

**示例：**

```
    3
   / \
  9  20
    /  \
   15   7

在这个二叉树中，有两个左叶子，分别是 9 和 15，所以返回 24
```

```c++
class Solution {
public:
    int sumOfLeftLeaves(TreeNode* root) {
        if(root==NULL){
            return 0;
        }
        int l=sumOfLeftLeaves(root->left);
        int r=sumOfLeftLeaves(root->right);
        int m=0;
        if(root->left&&root->left->left==NULL&&root->left->right==NULL){
            m=root->left->val;
        }
        return l+r+m;
    }
};
```

#### 513. 找树左下角的值

给定一个二叉树的 **根节点** `root`，请找出该二叉树的 **最底层 最左边** 节点的值。

假设二叉树中至少有一个节点。

 

**示例 1:**

![img](https://assets.leetcode.com/uploads/2020/12/14/tree1.jpg)

```
输入: root = [2,1,3]
输出: 1
```

**示例 2:**

![img](https://assets.leetcode.com/uploads/2020/12/14/tree2.jpg)

```
输入: [1,2,3,4,null,5,6,null,null,7]
输出: 7
```

```c++
class Solution {
public:
    int len=0;
    int max_len=0;
    int ans=0;
    void func(TreeNode*root){
        if(root->left==NULL&&root->right==NULL&&len>max_len){
            max_len=len;
            ans=root->val;
            return ;
        }
        if(root->left){
            len+=1;
            func(root->left);
            len-=1;
        }
        if(root->right){
            len+=1;
            func(root->right);
            len-=1;
        }

    }
    int findBottomLeftValue(TreeNode* root) {
        ans=root->val;
        func(root);
        return ans;
    }
};
```

#### >>112. 路径总和

给你二叉树的根节点 `root` 和一个表示目标和的整数 `targetSum` 。判断该树中是否存在 **根节点到叶子节点** 的路径，这条路径上所有节点值相加等于目标和 `targetSum` 。如果存在，返回 `true` ；否则，返回 `false` 。

**叶子节点** 是指没有子节点的节点。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/01/18/pathsum1.jpg)

```
输入：root = [5,4,8,11,null,13,4,7,2,null,null,null,1], targetSum = 22
输出：true
解释：等于目标和的根节点到叶节点路径如上图所示。
```

```c++
class Solution {
public:
    bool func(TreeNode*root,int m){
        if(root->left==NULL&&root->right==NULL&&m==0){
            return true;
        }
        if(root->left==NULL&&root->right==NULL){
            return false;
        }
        if(root->left){
            m-=root->left->val;
            if(func(root->left,m))
            {
                return true;
            }
            m+=root->left->val;
        }
        if(root->right){
            m-=root->right->val;
            if(func(root->right,m))
            {
                return true;
            }
            m+=root->right->val;
        }
        return false;

    }
    bool hasPathSum(TreeNode* root, int targetSum) {
        if(root==NULL){
            return false;
        }
        int m=targetSum;
        return func(root,m-root->val);
    }
};
```

#### 113. 路径总和 II

给你二叉树的根节点 `root` 和一个整数目标和 `targetSum` ，找出所有 **从根节点到叶子节点** 路径总和等于给定目标和的路径。

**叶子节点** 是指没有子节点的节点。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/01/18/pathsumii1.jpg)

```
输入：root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
输出：[[5,4,11,2],[5,8,4,5]]
```

```c++
class Solution {
public:
    vector<vector<int>>ans;
    vector<int>v;
    void func(TreeNode*root,int sum){
        if(root->left==NULL&&root->right==NULL&&sum==0){
            ans.push_back(v);
        }
        if(root->left){
            v.push_back(root->left->val);
            sum-=root->left->val;
            func(root->left,sum);
            v.pop_back();
            sum+=root->left->val;
        }
        if(root->right){
            v.push_back(root->right->val);
            sum-=root->right->val;
            func(root->right,sum);
            v.pop_back();
            sum+=root->right->val;
        }
    }
    vector<vector<int>> pathSum(TreeNode* root, int targetSum) {
        if(root==NULL){
            return ans;
        }
        v.push_back(root->val);
        func(root,targetSum-root->val);
        return ans;
    }
};
```

#### 437. 路径总和 III

给定一个二叉树的根节点 `root` ，和一个整数 `targetSum` ，求该二叉树里节点值之和等于 `targetSum` 的 **路径** 的数目。

**路径** 不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/04/09/pathsum3-1-tree.jpg)

```
输入：root = [10,5,-3,3,2,null,11,3,-2,null,1], targetSum = 8
输出：3
解释：和等于 8 的路径有 3 条，如图所示。
```

**示例 2：**

```
输入：root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
输出：3
```

```c++
class Solution {
public:
    int count = 0;
    int pathSum(TreeNode* root, int sum) {
        if (!root) return 0;
        dfs(root, sum) ;
        pathSum(root->left, sum) ;
        pathSum(root->right, sum);
        return count;
    }
    void dfs(TreeNode* root, long sum) {
        if (!root) return;
        if (sum - root->val == 0) count++;
        dfs(root->left, sum - root->val);
        dfs(root->right, sum - root->val);
    }
};
```



#### 106. 从中序与后序遍历序列构造二叉树

根据一棵树的中序遍历与后序遍历构造二叉树。

**注意:**
你可以假设树中没有重复的元素。

例如，给出

```
中序遍历 inorder = [9,3,15,20,7]
后序遍历 postorder = [9,15,7,20,3]
```

返回如下的二叉树：

```
    3
   / \
  9  20
    /  \
   15   7
```

```c++
class Solution {
public:
    TreeNode* func(vector<int>& inorder, vector<int>& postorder){
        if(postorder.size()==0){
            return NULL;
        }
        TreeNode*root=new TreeNode(0);
        root->val=postorder[postorder.size()-1];
        int count;
        for(count=0;count<inorder.size();count++){
            if(inorder[count]==root->val){

                break;
            }
        }
        vector<int>leftinorder(inorder.begin(),inorder.begin()+count);
        vector<int>rightinorder(inorder.begin()+count+1,inorder.end());
        postorder.resize(postorder.size()-1);
        vector<int>leftpostorder(postorder.begin(),postorder.begin()+leftinorder.size());
        vector<int>rightpostorder(postorder.begin()+leftinorder.size(),postorder.end());
        root->left=func(leftinorder,leftpostorder);
        root->right=func(rightinorder,rightpostorder);
        return root;
    }
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        if(inorder.size()==0 || postorder.size()==0){
            return NULL;
        }
        return func(inorder,postorder);
    }
};
```

#### 105. 从前序与中序遍历序列构造二叉树

给定一棵树的前序遍历 `preorder` 与中序遍历 `inorder`。请构造二叉树并返回其根节点。

 

**示例 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```

**示例 2:**

```
Input: preorder = [-1], inorder = [-1]
Output: [-1]
```

```c++
class Solution {
public:
    TreeNode*func(vector<int>& preorder, vector<int>& inorder){
        if(preorder.size()==0){
            return NULL;
        }
        TreeNode*root=new TreeNode(preorder[0]);
        int count=0;
        for(int i=0;i<inorder.size();i++){
            if(inorder[i]==preorder[0]){
                count=i;
            }
        }
        vector<int>p_left(preorder.begin()+1,preorder.begin()+count+1);
        vector<int>p_right(preorder.begin()+count+1,preorder.end());
        vector<int>i_left(inorder.begin(),inorder.begin()+count);
        vector<int>i_right(inorder.begin()+count+1,inorder.end());
        root->left=func(p_left,i_left);
        root->right=func(p_right,i_right);
        return  root;

    }
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        if(preorder.size()==0){
            return NULL;
        }
        return func(preorder,inorder);
    }
};
```

#### 654. 最大二叉树

给定一个不含重复元素的整数数组 `nums` 。一个以此数组直接递归构建的 **最大二叉树** 定义如下：

1. 二叉树的根是数组 `nums` 中的最大元素。
2. 左子树是通过数组中 **最大值左边部分** 递归构造出的最大二叉树。
3. 右子树是通过数组中 **最大值右边部分** 递归构造出的最大二叉树。

返回有给定数组 `nums` 构建的 **最大二叉树** 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/12/24/tree1.jpg)

```
输入：nums = [3,2,1,6,0,5]
输出：[6,3,5,null,2,0,null,null,1]
解释：递归调用如下所示：
- [3,2,1,6,0,5] 中的最大值是 6 ，左边部分是 [3,2,1] ，右边部分是 [0,5] 。
    - [3,2,1] 中的最大值是 3 ，左边部分是 [] ，右边部分是 [2,1] 。
        - 空数组，无子节点。
        - [2,1] 中的最大值是 2 ，左边部分是 [] ，右边部分是 [1] 。
            - 空数组，无子节点。
            - 只有一个元素，所以子节点是一个值为 1 的节点。
    - [0,5] 中的最大值是 5 ，左边部分是 [0] ，右边部分是 [] 。
        - 只有一个元素，所以子节点是一个值为 0 的节点。
        - 空数组，无子节点。
```

```c++
class Solution {
public:

    TreeNode* constructMaximumBinaryTree(vector<int>& nums) {
        TreeNode*root=new TreeNode(0);
        if(nums.size()==0){
            return root;
        }
        int max_num=0;
        int max_count=0;
        for(int i=0;i<nums.size();i++){
            if(nums[i]>max_num){
                max_num=nums[i];
                max_count=i;
            }
        }
        root->val=max_num;
        if(max_count>0){
            vector<int>l(nums.begin(),nums.begin()+max_count);
            root->left=constructMaximumBinaryTree(l);
        }
        if(max_count<nums.size()-1){
            vector<int>r(nums.begin()+max_count+1,nums.end());
            root->right=constructMaximumBinaryTree(r);
        }
        return root;
    }
};

```

#### 617. 合并二叉树

给定两个二叉树，想象当你将它们中的一个覆盖到另一个上时，两个二叉树的一些节点便会重叠。

你需要将他们合并为一个新的二叉树。合并的规则是如果两个节点重叠，那么将他们的值相加作为节点合并后的新值，否则**不为** NULL 的节点将直接作为新二叉树的节点。

**示例 1:**

```
输入: 
	Tree 1                     Tree 2                  
          1                         2                             
         / \                       / \                            
        3   2                     1   3                        
       /                           \   \                      
      5                             4   7                  
输出: 
合并后的树:
	     3
	    / \
	   4   5
	  / \   \ 
	 5   4   7
```

```c++
class Solution {
public:
    TreeNode* mergeTrees(TreeNode* root1, TreeNode* root2) {
        if(root1==NULL&&root2!=NULL){
            return root2;
        }
        if(root1!=NULL&&root2==NULL){
            return root1;
        }
        if(root1==NULL&&root2==NULL){
            return root1;
        }
        root1->val=root1->val+root2->val;
        root1->left=mergeTrees(root1->left,root2->left);
        root1->right=mergeTrees(root1->right,root2->right);
        return root1;
    }
};
```

#### 700. 二叉搜索树中的搜索

给定二叉搜索树（BST）的根节点和一个值。 你需要在BST中找到节点值等于给定值的节点。 返回以该节点为根的子树。 如果节点不存在，则返回 NULL。

例如，

```
给定二叉搜索树:

        4
       / \
      2   7
     / \
    1   3

和值: 2
```

你应该返回如下子树:

```
      2     
     / \   
    1   3
```

```c++
class Solution {
public:
    TreeNode* searchBST(TreeNode* root, int val) {
        if(root==NULL){
            return NULL;
        }
        if(root->val>val){
            return searchBST(root->left,val);
        }
        if(root->val<val){
            return searchBST(root->right,val);
        }
        if(root->val==val){
            return root;
        }
        return NULL;
    }
};

```

#### >>98. 验证二叉搜索树

给你一个二叉树的根节点 `root` ，判断其是否是一个有效的二叉搜索树。

**有效** 二叉搜索树定义如下：

- 节点的左子树只包含 **小于** 当前节点的数。
- 节点的右子树只包含 **大于** 当前节点的数。
- 所有左子树和右子树自身必须也是二叉搜索树。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/12/01/tree1.jpg)

```
输入：root = [2,1,3]
输出：true
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/12/01/tree2.jpg)

```
输入：root = [5,1,4,null,null,3,6]
输出：false
解释：根节点的值是 5 ，但是右子节点的值是 4 。
```

```c++
class Solution {
public:
    long long num=LONG_MIN;
    bool isValidBST(TreeNode* root) {
        if(root==NULL){
            return true;
        }
        bool l=isValidBST(root->left);
        if(root->val>num){
            num=root->val;
        }
        else{
            return false;
        }
        bool r=isValidBST(root->right);
        
        return l&&r;
    }
};
```

#### 501. 二叉搜索树中的众数

给定一个有相同值的二叉搜索树（BST），找出 BST 中的所有众数（出现频率最高的元素）。

假定 BST 有如下定义：

- 结点左子树中所含结点的值小于等于当前结点的值
- 结点右子树中所含结点的值大于等于当前结点的值
- 左子树和右子树都是二叉搜索树

例如：
给定 BST `[1,null,2,2]`,

```
   1
    \
     2
    /
   2
```

```c++
class Solution {
public:
    unordered_map<int,int>hashtable;
    void func(TreeNode*root){
        if(root==NULL){
            return ;
        }
        func(root->left);
        func(root->right);
        hashtable[root->val]++;
    }
    static bool cmp(vector<int>&a,vector<int>&b){
        return a[0]>b[0];
    }
    vector<int> findMode(TreeNode* root) {
        func(root);
        vector<vector<int>>v;
        for(auto p:hashtable){
            v.push_back({p.second,p.first});
        }
        sort(v.begin(),v.end(),cmp);
        vector<int>ans;
        int a=v[0][0];
        for(auto c:v){
            if(c[0]==a){
                ans.push_back(c[1]);
            }
            else{
                break;
            }
        }


        return ans;
    }
};
```

#### >>530. 二叉搜索树的最小绝对差

给你一个二叉搜索树的根节点 `root` ，返回 **树中任意两不同节点值之间的最小差值** 。

差值是一个正数，其数值等于两值之差的绝对值。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/02/05/bst1.jpg)

```C++
输入：root = [4,2,6,1,3]
输出：1
```

```C++
class Solution {
public:
    long long num=-1;
    int min_ans=INT_MAX;
    int getMinimumDifference(TreeNode* root) {
        if(root==NULL){
            return 0;
        }
        getMinimumDifference(root->left);
        if(num!=-1){
            if(root->val-num<min_ans){
                min_ans=root->val-num;
            }
        }
        num=root->val;
        getMinimumDifference(root->right);
        return min_ans;
    }
};
```

#### 236. 二叉树的最近公共祖先

给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

[百度百科](https://baike.baidu.com/item/最近公共祖先/8918834?fr=aladdin)中最近公共祖先的定义为：“对于有根树 T 的两个节点 p、q，最近公共祖先表示为一个节点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（**一个节点也可以是它自己的祖先**）。”

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```
输入：root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
输出：3
解释：节点 5 和节点 1 的最近公共祖先是节点 3 。
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```
输入：root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
输出：5
解释：节点 5 和节点 4 的最近公共祖先是节点 5 。因为根据定义最近公共祖先节点可以为节点本身。
```

```C++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root==p || root==q || root==NULL){
            return root;
        }
        TreeNode*l= lowestCommonAncestor(root->left,p,q);
        TreeNode*r= lowestCommonAncestor(root->right,p,q);
        if(l&&r){
            return root;
        }
        if(l&&!r){
            return l;
        }
        if(!l&&r){
            return r;
        }
        return NULL;
    }
};
```

#### 235. 二叉搜索树的最近公共祖先

给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。

[百度百科](https://baike.baidu.com/item/最近公共祖先/8918834?fr=aladdin)中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（**一个节点也可以是它自己的祖先**）。”

例如，给定如下二叉搜索树: root = [6,2,8,0,4,7,9,null,null,3,5]

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/binarysearchtree_improved.png)

 

**示例 1:**

```
输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
输出: 6 
解释: 节点 2 和节点 8 的最近公共祖先是 6。
```

```C++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root==p||root==q||root==NULL){
            return root;
        }
        TreeNode* left=lowestCommonAncestor(root->left,p,q);
        TreeNode* right=lowestCommonAncestor(root->right,p,q);
        if(left!=NULL&&right!=NULL){
            return root;
        }
        if(left!=NULL&&right==NULL){
            return left;
        }
        else if(left==NULL&&right!=NULL){
            return right;
        }
        else{
            return  NULL;
        }
    }
};
```

#### >>701. 二叉搜索树中的插入操作

难度中等251收藏分享切换为英文接收动态反馈

给定二叉搜索树（BST）的根节点和要插入树中的值，将值插入二叉搜索树。 返回插入后二叉搜索树的根节点。 输入数据 **保证** ，新值和原始二叉搜索树中的任意节点值都不同。

**注意**，可能存在多种有效的插入方式，只要树在插入后仍保持为二叉搜索树即可。 你可以返回 **任意有效的结果** 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/05/insertbst.jpg)

```C++
输入：root = [4,2,7,1,3], val = 5
输出：[4,2,7,1,3,5]
```

```C++
class Solution {
public:
    TreeNode* insertIntoBST(TreeNode* root, int val) {
        if(root==NULL)
        {
            TreeNode*tr=new TreeNode(val);
            return tr;
        }
        if(root->val<val)
        {
            root->right=insertIntoBST(root->right,val);
        }
        if(root->val>val)
        {
            root->left=insertIntoBST(root->left,val);
        }
        return root;
    }
};
```

#### >>450. 删除二叉搜索树中的节点

给定一个二叉搜索树的根节点 **root** 和一个值 **key**，删除二叉搜索树中的 **key** 对应的节点，并保证二叉搜索树的性质不变。返回二叉搜索树（有可能被更新）的根节点的引用。

一般来说，删除节点可分为两个步骤：

1. 首先找到需要删除的节点；
2. 如果找到了，删除它。

 

**示例 1:**

![img](https://assets.leetcode.com/uploads/2020/09/04/del_node_1.jpg)

```C++
输入：root = [5,3,6,2,4,null,7], key = 3
输出：[5,4,6,2,null,null,7]
解释：给定需要删除的节点值是 3，所以我们首先找到 3 这个节点，然后删除它。
一个正确的答案是 [5,4,6,2,null,null,7], 如下图所示。
另一个正确答案是 [5,2,6,null,4,null,7]。
```

```C++
class Solution {
public:
    TreeNode* deleteNode(TreeNode* root, int key) {
        if(root==NULL){
            return root;
        }
        if(root->val==key){
            if(root->left==NULL&&root->right==NULL){
                delete root;
                return NULL;
            }
            else if(root->left==NULL){
                TreeNode*temp=root->right;
                delete root;
                return temp;
            }
            else if(root->right==NULL){
                TreeNode*temp=root->left;
                delete root;
                return temp;
            }
            else{
                TreeNode*cur=root->right;
                while(cur->left!=NULL){
                    cur=cur->left;
                }
                cur->left=root->left;
                
                TreeNode*temp=root->right;
                delete root;
                return temp;
            }

        }
        if(root->val<key){
            root->right=deleteNode(root->right,key);
        }
        if(root->val>key){
            root->left=deleteNode(root->left,key);
        }
        return root;
        
    }
};
```

#### >>669. 修剪二叉搜索树

给你二叉搜索树的根节点 `root` ，同时给定最小边界`low` 和最大边界 `high`。通过修剪二叉搜索树，使得所有节点的值在`[low, high]`中。修剪树不应该改变保留在树中的元素的相对结构（即，如果没有被移除，原有的父代子代关系都应当保留）。 可以证明，存在唯一的答案。

所以结果应当返回修剪好的二叉搜索树的新的根节点。注意，根节点可能会根据给定的边界发生改变。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/09/09/trim1.jpg)

```
输入：root = [1,0,2], low = 1, high = 2
输出：[1,null,2]
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/09/09/trim2.jpg)

```c++
输入：root = [3,0,4,null,2,null,null,1], low = 1, high = 3
输出：[3,2,null,1]
```

```C++
class Solution {
public:
    TreeNode* trimBST(TreeNode* root, int low, int high) {
        if(root==NULL){
            return root;
        }
        if(root->val>high ){
            return trimBST(root->left,low,high);
        }
        if(root->val<low){
            return trimBST(root->right,low,high);
        }
        root->left=trimBST(root->left,low,high);
        root->right=trimBST(root->right,low,high);
        return root;

    }
};
```

#### 108. 将有序数组转换为二叉搜索树

给你一个整数数组 `nums` ，其中元素已经按 **升序** 排列，请你将其转换为一棵 **高度平衡** 二叉搜索树。

**高度平衡** 二叉树是一棵满足「每个节点的左右两个子树的高度差的绝对值不超过 1 」的二叉树。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/02/18/btree1.jpg)

```C++
输入：nums = [-10,-3,0,5,9]
输出：[0,-3,9,-10,null,5]
解释：[0,-10,5,null,-3,null,9] 也将被视为正确答案：
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/02/18/btree.jpg)

```C++
输入：nums = [1,3]
输出：[3,1]
解释：[1,3] 和 [3,1] 都是高度平衡二叉搜索树。
```

```C++
class Solution {
public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        TreeNode*root=new TreeNode(0);
        if(nums.size()==0){
            return root;
        }
        int mid=nums.size()/2;
        root->val=nums[mid];
        if(mid>0){
            vector<int>l(nums.begin(),nums.begin()+mid);
            root->left=sortedArrayToBST(l);
        }
        if(mid<nums.size()-1){
            vector<int>r(nums.begin()+mid+1,nums.end());
            root->right=sortedArrayToBST(r);
        }
        return root;
    }
};
```

#### 538. 把二叉搜索树转换为累加树

给出二叉 **搜索** 树的根节点，该树的节点值各不相同，请你将其转换为累加树（Greater Sum Tree），使每个节点 `node` 的新值等于原树中大于或等于 `node.val` 的值之和。

提醒一下，二叉搜索树满足下列约束条件：

- 节点的左子树仅包含键 **小于** 节点键的节点。
- 节点的右子树仅包含键 **大于** 节点键的节点。
- 左右子树也必须是二叉搜索树。

 

**示例 1：**

**![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/05/03/tree.png)**

```C++
输入：[4,1,6,0,2,5,7,null,null,null,3,null,null,null,8]
输出：[30,36,21,36,35,26,15,null,null,null,33,null,null,null,8]
```

**示例 2：**

```C++
输入：root = [0,null,1]
输出：[1,null,1]
```

**示例 3：**

```C++
输入：root = [1,0,2]
输出：[3,3,2]
```

```C++
class Solution {
public:
    int pre=0;
    void func(TreeNode*root){
        if(root==NULL){
            return ;
        }
        func(root->right);
        root->val+=pre;
        pre=root->val;
        func(root->left);
    }
    TreeNode* convertBST(TreeNode* root) {
        func(root);
        return root;
    }
};
```

#### 1382. 将二叉搜索树变平衡

给你一棵二叉搜索树，请你返回一棵 **平衡后** 的二叉搜索树，新生成的树应该与原来的树有着相同的节点值。如果有多种构造方法，请你返回任意一种。

如果一棵二叉搜索树中，每个节点的两棵子树高度差不超过 `1` ，我们就称这棵二叉搜索树是 **平衡的** 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/08/10/balance1-tree.jpg)

```
输入：root = [1,null,2,null,3,null,4,null,null]
输出：[2,1,3,null,null,null,4]
解释：这不是唯一的正确答案，[3,1,4,null,2,null,null] 也是一个可行的构造方案。
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/08/10/balanced2-tree.jpg)

```
输入: root = [2,1,3]
输出: [2,1,3]
```

```c++
class Solution {
public:
    TreeNode* func(vector<int>v){
        if(v.size()==0){
            return NULL;
        }
        int a=(v.size()-1)/2;
        TreeNode*root=new TreeNode(v[a]);
        vector<int>l(v.begin(),v.begin()+a);
        vector<int>r(v.begin()+a+1,v.end());
        root->left=func(l);
        root->right=func(r);
        return root;

    }
    void fun1(TreeNode*root,vector<int>&v){
        if(root==NULL){
            return ;
        }
        fun1(root->left,v);
        v.push_back(root->val);
        fun1(root->right,v);
    }
    TreeNode* balanceBST(TreeNode* root) {
        vector<int>v;
        fun1(root,v);
        TreeNode*cur=func(v);
        return cur;

    }
};
```

#### >>129. 求根节点到叶节点数字之和

给你一个二叉树的根节点 `root` ，树中每个节点都存放有一个 `0` 到 `9` 之间的数字。

每条从根节点到叶节点的路径都代表一个数字：

- 例如，从根节点到叶节点的路径 `1 -> 2 -> 3` 表示数字 `123` 。

计算从根节点到叶节点生成的 **所有数字之和** 。

**叶节点** 是指没有子节点的节点。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/02/19/num1tree.jpg)

```
输入：root = [1,2,3]
输出：25
解释：
从根到叶子节点路径 1->2 代表数字 12
从根到叶子节点路径 1->3 代表数字 13
因此，数字总和 = 12 + 13 = 25
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/02/19/num2tree.jpg)

```
输入：root = [4,9,0,5,1]
输出：1026
解释：
从根到叶子节点路径 4->9->5 代表数字 495
从根到叶子节点路径 4->9->1 代表数字 491
从根到叶子节点路径 4->0 代表数字 40
因此，数字总和 = 495 + 491 + 40 = 1026
```

```c++

```

#### 543. 二叉树的直径

给定一棵二叉树，你需要计算它的直径长度。一棵二叉树的直径长度是任意两个结点路径长度中的最大值。这条路径可能穿过也可能不穿过根结点。

 

**示例 :**
给定二叉树

```
          1
         / \
        2   3
       / \     
      4   5    
```

返回 **3**, 它的长度是路径 [4,2,1,3] 或者 [5,2,1,3]。

```c++
class Solution {
public:
    int ans=0;
    int func(TreeNode*root){
        if(root==NULL){
            return 0;
        }
        int l=func(root->left);
        int r=func(root->right);
        ans=max(ans,l+r);
        return max(l,r)+1;

    }
    int diameterOfBinaryTree(TreeNode* root) {
        func(root);
        return ans;
    }
};
```

#### 124. 二叉树中的最大路径和

**路径** 被定义为一条从树中任意节点出发，沿父节点-子节点连接，达到任意节点的序列。同一个节点在一条路径序列中 **至多出现一次** 。该路径 **至少包含一个** 节点，且不一定经过根节点。

**路径和** 是路径中各节点值的总和。

给你一个二叉树的根节点 `root` ，返回其 **最大路径和** 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/13/exx1.jpg)

```
输入：root = [1,2,3]
输出：6
解释：最优路径是 2 -> 1 -> 3 ，路径和为 2 + 1 + 3 = 6
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/10/13/exx2.jpg)

```
输入：root = [-10,9,20,null,null,15,7]
输出：42
解释：最优路径是 15 -> 20 -> 7 ，路径和为 15 + 20 + 7 = 42
```

```c++
class Solution {
public:
    int maxans=INT_MIN;
    int func(TreeNode*root){
        if(root==NULL){
            return 0;
        }
        int l=max(0,func(root->left));
        int r=max(0,func(root->right));
        maxans=max(l+r+root->val,maxans);
        return root->val+max(l,r);
    }
    int maxPathSum(TreeNode* root) {
        func(root);
        return maxans;
    }
};
```

#### >>114. 二叉树展开为链表

给你二叉树的根结点 `root` ，请你将它展开为一个单链表：

- 展开后的单链表应该同样使用 `TreeNode` ，其中 `right` 子指针指向链表中下一个结点，而左子指针始终为 `null` 。
- 展开后的单链表应该与二叉树 [**先序遍历**](https://baike.baidu.com/item/先序遍历/6442839?fr=aladdin) 顺序相同。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/01/14/flaten.jpg)

```
输入：root = [1,2,5,3,4,null,6]
输出：[1,null,2,null,3,null,4,null,5,null,6]
```

**示例 2：**

```
输入：root = []
输出：[]
```

**示例 3：**

```
输入：root = [0]
输出：[0]
```

```c++
class Solution {
public:
    void flatten(TreeNode* root) {
        if(root==NULL){
            return ;
        }
        flatten(root->left);
        flatten(root->right);
        TreeNode*temp=root->right;
        root->right=root->left;
        root->left=NULL;
        while(root->right!=NULL){
            root=root->right;
        }
        root->right=temp;
    }
};
```



## 回溯算法

#### 77. 组合

给定两个整数 `n` 和 `k`，返回范围 `[1, n]` 中所有可能的 `k` 个数的组合。

你可以按 **任何顺序** 返回答案。

**示例 1：**

```
输入：n = 4, k = 2
输出：
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

**示例 2：**

```
输入：n = 1, k = 1
输出：[[1]]
```

```c++
class Solution {
public:
    vector<vector<int>>ans;
    vector<int>v;
    void backtracking(int n,int k,int l){
        if(v.size()>=k){
            ans.push_back(v);
            return ;
        }
        for(int i=l;i<=n;i++){
            v.push_back(i);
            backtracking(n,k,i+1);
            v.pop_back();
        }
    }

    vector<vector<int>> combine(int n, int k) {
        backtracking(n,k,1);
        return ans;
    }
};
```

#### 216. 组合总和 III

找出所有相加之和为 ***n*** 的 ***k\*** 个数的组合***。\***组合中只允许含有 1 - 9 的正整数，并且每种组合中不存在重复的数字。

**说明：**

- 所有数字都是正整数。
- 解集不能包含重复的组合。 

**示例 1:**

```
输入: k = 3, n = 7
输出: [[1,2,4]]
```

**示例 2:**

```
输入: k = 3, n = 9
输出: [[1,2,6], [1,3,5], [2,3,4]]
```

```c++
class Solution {
public:
    vector<vector<int>>ans;
    vector<int>v;
    int sum=0;
    void backtracking(int k,int n,int l){
        if(sum==n&&v.size()==k){
            ans.push_back(v);
            return;
        }
        if(v.size()>k || sum>n){
            return ;
        }
        for(int i=l;i<=9;i++){
            v.push_back(i);
            sum+=i;
            backtracking(k,n,i+1);
            sum-=i;
            v.pop_back();
        }
    }
    vector<vector<int>> combinationSum3(int k, int n) {
        backtracking(k,n,1);
        return ans;
    }
};
```

#### 17. 电话号码的字母组合

给定一个仅包含数字 `2-9` 的字符串，返回所有它能表示的字母组合。答案可以按 **任意顺序** 返回。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2021/11/09/200px-telephone-keypad2svg.png)

 

**示例 1：**

```
输入：digits = "23"
输出：["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

**示例 2：**

```
输入：digits = ""
输出：[]
```

```C++
class Solution {
public:
    string hash[10]={"","","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
    vector<string>ans;
    string str;
    void backtracking(string digits,int l){
        if(str.size()>=digits.size()){
            ans.push_back(str);
            return ;
        }
        if(l>=digits.size()){
            return ;
        }
        int f=digits[l]-'0';
        for(int i=0;i<hash[f].size();i++){
            str+=hash[f][i];
            backtracking(digits,l+1);
            str.pop_back();
        }
    }
    vector<string> letterCombinations(string digits) {
        if(digits.size()==0){
            return ans;
        }
        backtracking(digits,0);
        return ans;
    }
};
```

#### 39. 组合总和

给你一个 **无重复元素** 的整数数组 `candidates` 和一个目标整数 `target` ，找出 `candidates` 中可以使数字和为目标数 `target` 的 **所有不同组合** ，并以列表形式返回。你可以按 **任意顺序** 返回这些组合。

`candidates` 中的 **同一个** 数字可以 **无限制重复被选取** 。如果至少一个数字的被选数量不同，则两种组合是不同的。 

对于给定的输入，保证和为 `target` 的不同组合数少于 `150` 个。

**示例 1：**

```
输入：candidates = [2,3,6,7], target = 7
输出：[[2,2,3],[7]]
解释：
2 和 3 可以形成一组候选，2 + 2 + 3 = 7 。注意 2 可以使用多次。
7 也是一个候选， 7 = 7 。
仅有这两种组合。
```

**示例 2：**

```
输入: candidates = [2,3,5], target = 8
输出: [[2,2,2,2],[2,3,3],[3,5]]
```

**示例 3：**

```
输入: candidates = [2], target = 1
输出: []
```

```C++
class Solution {
public:
    vector<vector<int>>ans;
    vector<int>v;
    int sum=0;
    void backtracking(vector<int>&candidates,int target,int l){
        if(sum==target){
            ans.push_back(v);
            return ;
        }
        if(sum>target){
            return ;
        }
        for(int i=l;i<candidates.size();i++){
            sum+=candidates[i];
            v.push_back(candidates[i]);
            backtracking(candidates,target,i);
            v.pop_back();
            sum-=candidates[i];
        }
    }
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        backtracking(candidates,target,0);
        return ans;
    }
};
```

#### 40. 组合总和 II

给你一个由候选元素组成的集合 `candidates` 和一个目标数 `target` ，找出 `candidates` 中所有可以使数字和为 `target` 的组合。

`candidates` 中的每个元素在每个组合中只能使用 **一次** 。

**注意：**解集不能包含重复的组合。 

 

**示例 1:**

```
输入: candidates = [10,1,2,7,6,1,5], target = 8,
输出:
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]
```

**示例 2:**

```
输入: candidates = [2,5,2,1,2], target = 5,
输出:
[
[1,2,2],
[5]
]
```

```C++
class Solution {
public:
    vector<vector<int>>ans;
    vector<int>v;
    int sum=0;
    void backtracking(vector<int>&candidates,int target,vector<bool>&b,int l){
        if(sum==target){
            ans.push_back(v);
            return ;
        }
        if(sum>target){
            return ;
        }
        for(int i=l;i<candidates.size();i++){
            if(i>0&&candidates[i]==candidates[i-1]&&b[i-1]==false){
                continue;
            }
            b[i]=true;
            sum+=candidates[i];
            v.push_back(candidates[i]);
            backtracking(candidates,target,b,i+1);
            sum-=candidates[i];
            v.pop_back();
            b[i]=false;
        }


    }

    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        sort(candidates.begin(),candidates.end());
        vector<bool>b(candidates.size(),false);
        backtracking(candidates,target,b,0);
        return ans;
    }
};
```

#### 131. 分割回文串

给你一个字符串 `s`，请你将 `s` 分割成一些子串，使每个子串都是 **回文串** 。返回 `s` 所有可能的分割方案。

**回文串** 是正着读和反着读都一样的字符串。

 

**示例 1：**

```
输入：s = "aab"
输出：[["a","a","b"],["aa","b"]]
```

**示例 2：**

```
输入：s = "a"
输出：[["a"]]
```

```C++
class Solution {
public:
    vector<vector<string>>ans;
    vector<string>v;
    bool isback(string s,int start,int end){
        while(start<end){
            if(s[start++]!=s[end--]){
                return false;
            }
        }
        return true;
    }
    void backtracking(string s,int l){
        if(l>=s.size()){
            ans.push_back(v);
            return ;
        }
        for(int i=l;i<s.size();i++){

            if(isback(s,l,i)){
                v.push_back(s.substr(l,i-l+1));          
            }
            else{
                continue;
            }
            backtracking(s,i+1);
            v.pop_back();
        }
    } 
     
    vector<vector<string>> partition(string s) {
        backtracking(s,0);
        return ans;
    }
};
```

#### 78. 子集

给你一个整数数组 `nums` ，数组中的元素 **互不相同** 。返回该数组所有可能的子集（幂集）。

解集 **不能** 包含重复的子集。你可以按 **任意顺序** 返回解集。

 

**示例 1：**

```c++
输入：nums = [1,2,3]
输出：[[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```

**示例 2：**

```c++
输入：nums = [0]
输出：[[],[0]]
```

```c++
class Solution {
public:
    vector<vector<int>>ans;
    vector<int>v;
    void backtracking(vector<int>&nums,int l){
        ans.push_back(v);
        if(l>=nums.size()){
            return ;
        }
        for(int i=l;i<nums.size();i++){
            v.push_back(nums[i]);
            backtracking(nums,i+1);
            v.pop_back();
        }
    }
    vector<vector<int>> subsets(vector<int>& nums) {
        backtracking(nums,0);
        return ans;
    }
};
```

#### 90. 子集 II

给你一个整数数组 `nums` ，其中可能包含重复元素，请你返回该数组所有可能的子集（幂集）。

解集 **不能** 包含重复的子集。返回的解集中，子集可以按 **任意顺序** 排列。

 

**示例 1：**

```
输入：nums = [1,2,2]
输出：[[],[1],[1,2],[1,2,2],[2],[2,2]]
```

**示例 2：**

```
输入：nums = [0]
输出：[[],[0]]
```

```c++
class Solution {
public:
    vector<vector<int>>ans;
    vector<int>v;
    void backtracking(vector<int>&nums,int l,vector<bool>&b){
        ans.push_back(v);
        if(l>=nums.size()){
            return;
        }
        for(int i=l;i<nums.size();i++){
            if(i>0&&nums[i]==nums[i-1]&&b[i-1]==false){
                continue;
            }
            b[i]=true;
            v.push_back(nums[i]);
            backtracking(nums,i+1,b);
            v.pop_back();
            b[i]=false;
        }
    }
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        vector<bool>b(nums.size(),false);
        backtracking(nums,0,b);
        return ans;
    }
};
```

#### 491. 递增子序列

给你一个整数数组 `nums` ，找出并返回所有该数组中不同的递增子序列，递增子序列中 **至少有两个元素** 。你可以按 **任意顺序** 返回答案。

数组中可能含有重复元素，如出现两个整数相等，也可以视作递增序列的一种特殊情况。

 

**示例 1：**

```
输入：nums = [4,6,7,7]
输出：[[4,6],[4,6,7],[4,6,7,7],[4,7],[4,7,7],[6,7],[6,7,7],[7,7]]
```

**示例 2：**

```
输入：nums = [4,4,3,2,1]
输出：[[4,4]]
```

```c++
class Solution {
public:
    vector<vector<int>>ans;
    vector<int>v;
    void func(vector<int>&nums,int l){
        if(v.size()>1){
            ans.push_back(v);
        }
        if(l>=nums.size()){
            return ;
        }
        unordered_set<int>set;
        for(int i=l;i<nums.size();i++){
            if(!v.empty()&&nums[i]<v.back() || set.find(nums[i])!=set.end()){
                continue;
            }
            set.insert(nums[i]);
            v.push_back(nums[i]);
            func(nums,i+1);
            v.pop_back();
        }
    }
    vector<vector<int>> findSubsequences(vector<int>& nums) {
        func(nums,0);
        return ans;
    }
};
```

#### 46. 全排列

给定一个不含重复数字的数组 `nums` ，返回其 *所有可能的全排列* 。你可以 **按任意顺序** 返回答案。

 

**示例 1：**

```
输入：nums = [1,2,3]
输出：[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

**示例 2：**

```
输入：nums = [0,1]
输出：[[0,1],[1,0]]
```

**示例 3：**

```
输入：nums = [1]
输出：[[1]]
```

```c++
class Solution {
public:
    vector<vector<int>>ans;
    vector<int>v;
    void backtracking(vector<int>&nums,vector<bool>&b){
        if(v.size()==nums.size()){
            ans.push_back(v);
            return ;
        }
        for(int i=0;i<nums.size();i++){
            if(b[i]==true){
                continue;
            }
            b[i]=true;
            v.push_back(nums[i]);
            backtracking(nums,b);
            b[i]=false;
            v.pop_back();
        }
    }
    vector<vector<int>> permute(vector<int>& nums) {
        vector<bool>b(nums.size(),false);
        backtracking(nums,b);
        return ans;
    }
};
```

#### >>47. 全排列 II

给定一个可包含重复数字的序列 `nums` ，***按任意顺序*** 返回所有不重复的全排列。

**示例 1：**

```
输入：nums = [1,1,2]
输出：
[[1,1,2],
 [1,2,1],
 [2,1,1]]
```

**示例 2：**

```
输入：nums = [1,2,3]
输出：[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

 

```c++
class Solution {
public:
    vector<vector<int>>ans;
    vector<int>v;
    void backtracking(vector<int>&nums,vector<bool>&b){
        if(v.size()==nums.size()){
            ans.push_back(v);
            return ;
        }
        for(int i=0;i<nums.size();i++){
            if(i>0&&nums[i]==nums[i-1]&&b[i-1]==false){
                continue;
            }
            if(b[i]==false){
                b[i]=true;
                v.push_back(nums[i]);
                backtracking(nums,b);
                b[i]=false;
                v.pop_back();
            }
        }
    }
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        vector<bool>b(nums.size(),false);
        backtracking(nums,b);
        return ans;
    }
};
```

#### 93. 复原 IP 地址

**有效 IP 地址** 正好由四个整数（每个整数位于 `0` 到 `255` 之间组成，且不能含有前导 `0`），整数之间用 `'.'` 分隔。

- 例如：`"0.1.2.201"` 和` "192.168.1.1"` 是 **有效** IP 地址，但是 `"0.011.255.245"`、`"192.168.1.312"` 和 `"192.168@1.1"` 是 **无效** IP 地址。

给定一个只包含数字的字符串 `s` ，用以表示一个 IP 地址，返回所有可能的**有效 IP 地址**，这些地址可以通过在 `s` 中插入 `'.'` 来形成。你 **不能** 重新排序或删除 `s` 中的任何数字。你可以按 **任何** 顺序返回答案。

 

**示例 1：**

```
输入：s = "25525511135"
输出：["255.255.11.135","255.255.111.35"]
```

**示例 2：**

```
输入：s = "0000"
输出：["0.0.0.0"]
```

**示例 3：**

```
输入：s = "101023"
输出：["1.0.10.23","1.0.102.3","10.1.0.23","10.10.2.3","101.0.2.3"]
```

```c++
class Solution {
public:
    vector<string>ans;
    int count=0;
    bool ist(string s,int start,int end){
        if(start>end){
            return false;
        }
        if(s[start]=='0'&&start!=end){
            return false;
        }

        int sum=0;
        while(start<=end){
            if(s[start]<'0'|| s[start]>'9'){
                return false;
            }
            sum=sum*10+s[start]-'0';
            start++;
            if(sum>255){
                return false;
            }
        }

        return true;
    }
    void backtracking(string s,int l){
        if(count==3&&ist(s,l,s.size()-1)){
            ans.push_back(s);
            return ;
        }

        for(int i=l;i<s.size();i++){
            if(ist(s,l,i)){
                s.insert(s.begin()+i+1,'.');
                count++;
                backtracking(s,i+2);
                count--;
                s.erase(s.begin()+i+1);
            }
            else{
                break;
            }
        }
    }

    vector<string> restoreIpAddresses(string s) {
        backtracking(s,0);
        return ans;
    }
};
```

#### [332. 重新安排行程](https://leetcode.cn/problems/reconstruct-itinerary/)

给你一份航线列表 `tickets` ，其中 `tickets[i] = [fromi, toi]` 表示飞机出发和降落的机场地点。请你对该行程进行重新规划排序。

所有这些机票都属于一个从 `JFK`（肯尼迪国际机场）出发的先生，所以该行程必须从 `JFK` 开始。如果存在多种有效的行程，请你按字典排序返回最小的行程组合。

- 例如，行程 `["JFK", "LGA"]` 与 `["JFK", "LGB"]` 相比就更小，排序更靠前。

假定所有机票至少存在一种合理的行程。且所有的机票 必须都用一次 且 只能用一次。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/03/14/itinerary1-graph.jpg)

```
输入：tickets = [["MUC","LHR"],["JFK","MUC"],["SFO","SJC"],["LHR","SFO"]]
输出：["JFK","MUC","LHR","SFO","SJC"]
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/03/14/itinerary2-graph.jpg)

```
输入：tickets = [["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]
输出：["JFK","ATL","JFK","SFO","ATL","SFO"]
解释：另一种有效的行程是 ["JFK","SFO","ATL","JFK","ATL","SFO"] ，但是它字典排序更大更靠后。
```

```

```

#### >>51. N 皇后

按照国际象棋的规则，皇后可以攻击与之处在同一行或同一列或同一斜线上的棋子。

**n 皇后问题** 研究的是如何将 `n` 个皇后放置在 `n×n` 的棋盘上，并且使皇后彼此之间不能相互攻击。

给你一个整数 `n` ，返回所有不同的 **n 皇后问题** 的解决方案。

每一种解法包含一个不同的 **n 皇后问题** 的棋子放置方案，该方案中 `'Q'` 和 `'.'` 分别代表了皇后和空位。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

```
输入：n = 4
输出：[[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
解释：如上图所示，4 皇后问题存在两个不同的解法。
```

**示例 2：**

```c++
输入：n = 1
输出：[["Q"]]
```

```c++
class Solution {
private:
vector<vector<string>> result;
void backtracking(int n, int row, vector<string>& chessboard) {
    if (row == n) {
        result.push_back(chessboard);
        return;
    }
    for (int col = 0; col < n; col++) {
        if (isValid(row, col, chessboard, n)) { 
            chessboard[row][col] = 'Q'; 
            backtracking(n, row + 1, chessboard);
            chessboard[row][col] = '.'; 
        }
    }
}
bool isValid(int row, int col, vector<string>& chessboard, int n) {
    for (int i = 0; i < row; i++) { 
        if (chessboard[i][col] == 'Q') {
            return false;
        }
    }
    for (int i = row - 1, j = col - 1; i >=0 && j >= 0; i--, j--) {
        if (chessboard[i][j] == 'Q') {
            return false;
        }
    }
    for(int i = row - 1, j = col + 1; i >= 0 && j < n; i--, j++) {
        if (chessboard[i][j] == 'Q') {
            return false;
        }
    }
    return true;
}
public:
    vector<vector<string>> solveNQueens(int n) {
        result.clear();
        std::vector<std::string> chessboard(n, std::string(n, '.'));
        backtracking(n, 0, chessboard);
        return result;
    }
};
```

#### >>37. 解数独

编写一个程序，通过填充空格来解决数独问题。

数独的解法需 **遵循如下规则**：

1. 数字 `1-9` 在每一行只能出现一次。
2. 数字 `1-9` 在每一列只能出现一次。
3. 数字 `1-9` 在每一个以粗实线分隔的 `3x3` 宫内只能出现一次。（请参考示例图）

数独部分空格内已填入了数字，空白格用 `'.'` 表示。

 

**示例 1：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2021/04/12/250px-sudoku-by-l2g-20050714svg.png)

```
输入：board = [["5","3",".",".","7",".",".",".","."],["6",".",".","1","9","5",".",".","."],[".","9","8",".",".",".",".","6","."],["8",".",".",".","6",".",".",".","3"],["4",".",".","8",".","3",".",".","1"],["7",".",".",".","2",".",".",".","6"],[".","6",".",".",".",".","2","8","."],[".",".",".","4","1","9",".",".","5"],[".",".",".",".","8",".",".","7","9"]]
输出：[["5","3","4","6","7","8","9","1","2"],["6","7","2","1","9","5","3","4","8"],["1","9","8","3","4","2","5","6","7"],["8","5","9","7","6","1","4","2","3"],["4","2","6","8","5","3","7","9","1"],["7","1","3","9","2","4","8","5","6"],["9","6","1","5","3","7","2","8","4"],["2","8","7","4","1","9","6","3","5"],["3","4","5","2","8","6","1","7","9"]]
解释：输入的数独如上图所示，唯一有效的解决方案如下所示：
```

```c++

```

#### >>52. N皇后 II

**n 皇后问题** 研究的是如何将 `n` 个皇后放置在 `n × n` 的棋盘上，并且使皇后彼此之间不能相互攻击。

给你一个整数 `n` ，返回 **n 皇后问题** 不同的解决方案的数量。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

```
输入：n = 4
输出：2
解释：如上图所示，4 皇后问题存在两个不同的解法。
```

**示例 2：**

```
输入：n = 1
输出：1
```

```c++

```

#### 22. 括号生成

数字 `n` 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 **有效的** 括号组合。

 

**示例 1：**

```
输入：n = 3
输出：["((()))","(()())","(())()","()(())","()()()"]
```

**示例 2：**

```
输入：n = 1
输出：["()"]
```

```c++
class Solution {
public:
    vector<string>ans;
    void backtracking(int left,int right,string s){
        if(left==0&&right==0){
            ans.push_back(s);
            return ;
        }
        if(left>0){
            backtracking(left-1,right,s+"(");
        }
        if(right>left){
            backtracking(left,right-1,s+")");
        }

    }
    vector<string> generateParenthesis(int n) {
        backtracking(n,n,"");
        return ans;
    }
};
```



## 动态规划

#### 509. 斐波那契数

**斐波那契数** （通常用 `F(n)` 表示）形成的序列称为 **斐波那契数列** 。该数列由 `0` 和 `1` 开始，后面的每一项数字都是前面两项数字的和。也就是：

```
F(0) = 0，F(1) = 1
F(n) = F(n - 1) + F(n - 2)，其中 n > 1
```

给定 `n` ，请计算 `F(n)` 。

**示例 1：**

```
输入：n = 2
输出：1
解释：F(2) = F(1) + F(0) = 1 + 0 = 1
```

**示例 2：**

```
输入：n = 3
输出：2
解释：F(3) = F(2) + F(1) = 1 + 1 = 2
```

**示例 3：**

```
输入：n = 4
输出：3
解释：F(4) = F(3) + F(2) = 2 + 1 = 3
```

```c++
class Solution {
public:
    int fib(int n) {
        int dp[2];
        dp[0]=0;
        dp[1]=1;
        int temp=0;
        if(n==0){
            return dp[0];
        }
        for(int i=2;i<=n;i++){
            temp=dp[0]+dp[1];
            dp[0]=dp[1];
            dp[1]=temp;
            
        }
        return dp[1];
    }
};
```

#### 70. 爬楼梯

假设你正在爬楼梯。需要 `n` 阶你才能到达楼顶。

每次你可以爬 `1` 或 `2` 个台阶。你有多少种不同的方法可以爬到楼顶呢？

**示例 1：**

```
输入：n = 2
输出：2
解释：有两种方法可以爬到楼顶。
1. 1 阶 + 1 阶
2. 2 阶
```

**示例 2：**

```
输入：n = 3
输出：3
解释：有三种方法可以爬到楼顶。
1. 1 阶 + 1 阶 + 1 阶
2. 1 阶 + 2 阶
3. 2 阶 + 1 阶
```

```c++
class Solution {
public:
    int climbStairs(int n) {
        int dp[2];
        dp[0]=0;
        dp[1]=1;
        int temp=0;
        for(int i=1;i<=n;i++){
            temp=dp[0]+dp[1];
            dp[0]=dp[1];
            dp[1]=temp;
        }
        return dp[1];
    }
};
```

#### >>746. 使用最小花费爬楼梯

给你一个整数数组 `cost` ，其中 `cost[i]` 是从楼梯第 `i` 个台阶向上爬需要支付的费用。一旦你支付此费用，即可选择向上爬一个或者两个台阶。

你可以选择从下标为 `0` 或下标为 `1` 的台阶开始爬楼梯。

请你计算并返回达到楼梯顶部的最低花费。

 

**示例 1：**

```
输入：cost = [10,15,20]
输出：15
解释：你将从下标为 1 的台阶开始。
- 支付 15 ，向上爬两个台阶，到达楼梯顶部。
总花费为 15 。
```

**示例 2：**

```
输入：cost = [1,100,1,1,1,100,1,1,100,1]
输出：6
解释：你将从下标为 0 的台阶开始。
- 支付 1 ，向上爬两个台阶，到达下标为 2 的台阶。
- 支付 1 ，向上爬两个台阶，到达下标为 4 的台阶。
- 支付 1 ，向上爬两个台阶，到达下标为 6 的台阶。
- 支付 1 ，向上爬一个台阶，到达下标为 7 的台阶。
- 支付 1 ，向上爬两个台阶，到达下标为 9 的台阶。
- 支付 1 ，向上爬一个台阶，到达楼梯顶部。
总花费为 6 。
```

```c++
class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) {
        int dp[2];
        dp[0]=cost[0];
        dp[1]=cost[1];
        for(int i=2;i<cost.size();i++){
            int temp=min(dp[1],dp[0])+cost[i];
            dp[0]=dp[1];
            dp[1]=temp;
        }
        return min(dp[0],dp[1]);
    }
};
```

#### 62. 不同路径

一个机器人位于一个 `m x n` 网格的左上角 （起始点在下图中标记为 “Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为 “Finish” ）。

问总共有多少条不同的路径？

**示例 1：**

![img](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

```
输入：m = 3, n = 7
输出：28
```

**示例 2：**

```
输入：m = 3, n = 2
输出：3
解释：
从左上角开始，总共有 3 条路径可以到达右下角。
1. 向右 -> 向下 -> 向下
2. 向下 -> 向下 -> 向右
3. 向下 -> 向右 -> 向下
```

**示例 3：**

```
输入：m = 7, n = 3
输出：28
```

**示例 4：**

```
输入：m = 3, n = 3
输出：6
```

```c++
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>>dp(m,vector<int>(n,0));
        for(int i=0;i<m;i++){
            dp[i][0]=1;
        }
        for(int i=0;i<n;i++){
            dp[0][i]=1;
        }
        for(int i=1;i<n;i++){
            for(int j=1;j<m;j++){
                dp[j][i]=dp[j-1][i]+dp[j][i-1];
            }
        }
        return dp[m-1][n-1];
    }
};
```

#### 63. 不同路径 II

一个机器人位于一个 `m x n` 网格的左上角 （起始点在下图中标记为 “Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为 “Finish”）。

现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？

网格中的障碍物和空位置分别用 `1` 和 `0` 来表示。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/04/robot1.jpg)

```
输入：obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]
输出：2
解释：3x3 网格的正中间有一个障碍物。
从左上角到右下角一共有 2 条不同的路径：
1. 向右 -> 向右 -> 向下 -> 向下
2. 向下 -> 向下 -> 向右 -> 向右
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/11/04/robot2.jpg)

```
输入：obstacleGrid = [[0,1],[0,0]]
输出：1
```

```c++
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        vector<vector<int>>dp(obstacleGrid.size(),vector<int>(obstacleGrid[0].size(),0));
        for(int i=0;i<obstacleGrid.size()&&obstacleGrid[i][0]==0;i++){
            dp[i][0]=1;
        }
        for(int i=0;i<obstacleGrid[0].size()&&obstacleGrid[0][i]==0;i++){
            dp[0][i]=1;
        }
        for(int i=1;i<obstacleGrid.size();i++){
            for(int j=1;j<obstacleGrid[0].size();j++){
                if(obstacleGrid[i][j]==1){
                    continue;
                }
                dp[i][j]=dp[i-1][j]+dp[i][j-1];
            }
        }
        return dp[obstacleGrid.size()-1][obstacleGrid[0].size()-1];
    }
};
```

#### 343. 整数拆分

给定一个正整数 `n` ，将其拆分为 `k` 个 **正整数** 的和（ `k >= 2` ），并使这些整数的乘积最大化。

返回 *你可以获得的最大乘积* 。

**示例 1:**

```
输入: n = 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1。
```

**示例 2:**

```
输入: n = 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36。
```

 

```c++
class Solution {
public:
    int integerBreak(int n) {
        if(n==2){
            return 1;
        }
        if(n==3){
            return 2;
        }
        if(n==4){
            return 4;
        }
        int ans=1;
        while(n>4){
            ans*=3;
            n-=3;
        }
        ans*=n;
        return ans;
    }
};


class Solution {
public:
    int integerBreak(int n) {
        vector<int>dp(n+1,0);
        dp[2]=1;
        for(int i=3;i<=n;i++){
            for(int j=1;j<i-1;j++){
                dp[i]=max(dp[i],max((i-j)*j,dp[i-j]*j));
            }
        }
        return dp[n];
        
    }
};
```

#### 96. 不同的二叉搜索树

给你一个整数 `n` ，求恰由 `n` 个节点组成且节点值从 `1` 到 `n` 互不相同的 **二叉搜索树** 有多少种？返回满足题意的二叉搜索树的种数。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg)

```
输入：n = 3
输出：5
```

**示例 2：**

```
输入：n = 1
输出：1
```

```c++
class Solution {
public:
    int numTrees(int n) {
        vector<int>dp(n+1,0);
        dp[0]=1;
        for(int i=1;i<=n;i++){
            for(int j=1;j<=i;j++){
                dp[i]+=dp[j-1]*dp[i-j];
            }
        }
        return dp[n];
    }
};
```

#### 64. 最小路径和

给定一个包含非负整数的 `*m* x *n*` 网格 `grid` ，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

**说明：**每次只能向下或者向右移动一步。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/05/minpath.jpg)

```
输入：grid = [[1,3,1],[1,5,1],[4,2,1]]
输出：7
解释：因为路径 1→3→1→1→1 的总和最小。
```

**示例 2：**

```
输入：grid = [[1,2,3],[4,5,6]]
输出：12
```

```c++
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int a=grid.size();
        int b=grid[0].size();
        vector<vector<int>>dp(a,vector<int>(b,INT_MAX));
        dp[0][0]=grid[0][0];
        for(int i=1;i<a;i++){
            dp[i][0]=dp[i-1][0]+grid[i][0];
        }
        for(int i=1;i<b;i++){
            dp[0][i]=dp[0][i-1]+grid[0][i];
        }
        for(int i=1;i<a;i++){
            for(int j=1;j<b;j++){
                dp[i][j]=min(dp[i][j-1],dp[i-1][j])+grid[i][j];
            }
        }
        return dp[a-1][b-1];
    }
};
```

#### 152. 乘积最大子数组

给你一个整数数组 `nums` ，请你找出数组中乘积最大的非空连续子数组（该子数组中至少包含一个数字），并返回该子数组所对应的乘积。

测试用例的答案是一个 **32-位** 整数。

**子数组** 是数组的连续子序列。

 

**示例 1:**

```
输入: nums = [2,3,-2,4]
输出: 6
解释: 子数组 [2,3] 有最大乘积 6。
```

**示例 2:**

```
输入: nums = [-2,0,-1]
输出: 0
解释: 结果不能为 2, 因为 [-2,-1] 不是子数组。
```

```c++
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        vector<vector<int>>dp(2,vector<int>(nums.size(),1));
        dp[0][0]=nums[0];
        dp[1][0]=nums[0];
        int ans=nums[0];
        for(int i=1;i<nums.size();i++){
            dp[0][i]=max(nums[i]*dp[0][i-1],max(nums[i],nums[i]*dp[1][i-1]));
            dp[1][i]=min(nums[i]*dp[0][i-1],min(nums[i],nums[i]*dp[1][i-1]));
            ans=max(ans,dp[0][i]);
        }
        return ans;
    }
};
```



### 01背包

每样东西只能用一次，且不能重复，写法是：先从前往后遍历物品，在从后往前遍历背包，这样就能保证在遍历中不受重复的影响。

#### 416. 分割等和子集

给你一个 **只包含正整数** 的 **非空** 数组 `nums` 。请你判断是否可以将这个数组分割成两个子集，使得两个子集的元素和相等。

**示例 1：**

```c++
输入：nums = [1,5,11,5]
输出：true
解释：数组可以分割成 [1, 5, 5] 和 [11] 。
```

**示例 2：**

```c++
输入：nums = [1,2,3,5]
输出：false
解释：数组不能分割成两个元素和相等的子集。
```

```c++
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int sum=0;
        for(int i=0;i<nums.size();i++){
            sum+=nums[i];
        }
        if(sum%2){
            return false;
        }
        int count=sum/2;
        vector<int>dp(count+1,0);
        for(int i=0;i<nums.size();i++){
            for(int j=count;j>=nums[i];j--){
                dp[j]=max(dp[j],dp[j-nums[i]]+nums[i]);
            }
        }
        if(dp[count]==count){
            return true;
        }
        return false;
    }
};
```

#### 1049. 最后一块石头的重量 II

有一堆石头，用整数数组 `stones` 表示。其中 `stones[i]` 表示第 `i` 块石头的重量。

每一回合，从中选出**任意两块石头**，然后将它们一起粉碎。假设石头的重量分别为 `x` 和 `y`，且 `x <= y`。那么粉碎的可能结果如下：

- 如果 `x == y`，那么两块石头都会被完全粉碎；
- 如果 `x != y`，那么重量为 `x` 的石头将会完全粉碎，而重量为 `y` 的石头新重量为 `y-x`。

最后，**最多只会剩下一块** 石头。返回此石头 **最小的可能重量** 。如果没有石头剩下，就返回 `0`。

 

**示例 1：**

```c++
输入：stones = [2,7,4,1,8,1]
输出：1
解释：
组合 2 和 4，得到 2，所以数组转化为 [2,7,1,8,1]，
组合 7 和 8，得到 1，所以数组转化为 [2,1,1,1]，
组合 2 和 1，得到 1，所以数组转化为 [1,1,1]，
组合 1 和 1，得到 0，所以数组转化为 [1]，这就是最优值。
```

**示例 2：**

```c++
输入：stones = [31,26,33,21,40]
输出：5
```

```c++
class Solution {
public:
    int lastStoneWeightII(vector<int>& stones) {
        int sum=0;
        for(auto &i:stones){
            sum+=i;
        }
        int count=sum/2;
        vector<int>dp(count+1,0);
        for(int i=0;i<stones.size();i++){
            for(int j=count;j>=stones[i];j--){
                dp[j]=max(dp[j],dp[j-stones[i]]+stones[i]);
            }
        }
        return sum-=2*dp[count];
    }
};
```

#### 494. 目标和

给你一个整数数组 `nums` 和一个整数 `target` 。

向数组中的每个整数前添加 `'+'` 或 `'-'` ，然后串联起所有整数，可以构造一个 **表达式** ：

- 例如，`nums = [2, 1]` ，可以在 `2` 之前添加 `'+'` ，在 `1` 之前添加 `'-'` ，然后串联起来得到表达式 `"+2-1"` 。

返回可以通过上述方法构造的、运算结果等于 `target` 的不同 **表达式** 的数目。

**示例 1：**

```
输入：nums = [1,1,1,1,1], target = 3
输出：5
解释：一共有 5 种方法让最终目标和为 3 。
-1 + 1 + 1 + 1 + 1 = 3
+1 - 1 + 1 + 1 + 1 = 3
+1 + 1 - 1 + 1 + 1 = 3
+1 + 1 + 1 - 1 + 1 = 3
+1 + 1 + 1 + 1 - 1 = 3
```

**示例 2：**

```
输入：nums = [1], target = 1
输出：1
```

```c++
class Solution {
public:
    int findTargetSumWays(vector<int>& nums, int target) {
        int sum=0;
        for(auto &i:nums){
            sum+=i;
        }
        if(abs(target)>sum){
            return 0;
        }
        if((sum+target)%2){
            return 0;
        }
        target=(sum+target)/2;
        vector<int>dp(target+1,0);
        dp[0]=1;
        for(int i=0;i<nums.size();i++){
            for(int j=target;j>=nums[i];j--){
                dp[j]+=dp[j-nums[i]];
            }
        }
        return dp[target];
    }
};
```

#### 474. 一和零

给你一个二进制字符串数组 `strs` 和两个整数 `m` 和 `n` 。

请你找出并返回 `strs` 的最大子集的长度，该子集中 **最多** 有 `m` 个 `0` 和 `n` 个 `1` 。

如果 `x` 的所有元素也是 `y` 的元素，集合 `x` 是集合 `y` 的 **子集** 。

**示例 1：**

```
输入：strs = ["10", "0001", "111001", "1", "0"], m = 5, n = 3
输出：4
解释：最多有 5 个 0 和 3 个 1 的最大子集是 {"10","0001","1","0"} ，因此答案是 4 。
其他满足题意但较小的子集包括 {"0001","1"} 和 {"10","1","0"} 。{"111001"} 不满足题意，因为它含 4 个 1 ，大于 n 的值 3 。
```

**示例 2：**

```
输入：strs = ["10", "0", "1"], m = 1, n = 1
输出：2
解释：最大的子集是 {"0", "1"} ，所以答案是 2 。
```

```c++
class Solution {
public:
    int findMaxForm(vector<string>& strs, int m, int n) {
        vector<vector<int>>dp(m+1,vector<int>(n+1,0));
        for(auto str:strs){
            int zero_count=0;
            int one_count=0;
            for(auto s:str){
                if(s=='0'){
                    zero_count++;
                }
                else{
                    one_count++;
                }
            }
            for(int i=m;i>=zero_count;i--){
                for(int j=n;j>=one_count;j--){
                    dp[i][j]=max(dp[i-zero_count][j-one_count]+1,dp[i][j]);
                }
            }
        }
        return dp[m][n];
    }
}
```

### 完全背包

每样东西可以使用多次来达到要求。写法：从前往后遍历物品，从前往后遍历背包。如果是组合，先遍历物品，在遍历背包。如果是排列，先遍历背包，在遍历物品。

#### 518.零钱兑换

难度中等765收藏分享切换为英文接收动态反馈

给你一个整数数组 `coins` 表示不同面额的硬币，另给一个整数 `amount` 表示总金额。

请你计算并返回可以凑成总金额的硬币组合数。如果任何硬币组合都无法凑出总金额，返回 `0` 。

假设每一种面额的硬币有无限个。 

题目数据保证结果符合 32 位带符号整数。

**示例 1：**

```
输入：amount = 5, coins = [1, 2, 5]
输出：4
解释：有四种方式可以凑成总金额：
5=5
5=2+2+1
5=2+1+1+1
5=1+1+1+1+1
```

**示例 2：**

```
输入：amount = 3, coins = [2]
输出：0
解释：只用面额 2 的硬币不能凑成总金额 3 。
```

**示例 3：**

```
输入：amount = 10, coins = [10] 
输出：1
```

```c++
class Solution {
public:
    int change(int amount, vector<int>& coins) {
        vector<int>dp(amount+1,0);
        dp[0]=1;
        for(int i=0;i<coins.size();i++){
            for(int j=coins[i];j<=amount;j++){
                dp[j]+=dp[j-coins[i]];
            }
        }
        return dp[amount];
    }
};
```

#### 377. 组合总和 Ⅳ

难度中等602收藏分享切换为英文接收动态反馈

给你一个由 **不同** 整数组成的数组 `nums` ，和一个目标整数 `target` 。请你从 `nums` 中找出并返回总和为 `target` 的元素组合的个数。

题目数据保证答案符合 32 位整数范围

**示例 1：**

```
输入：nums = [1,2,3], target = 4
输出：7
解释：
所有可能的组合为：
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)
请注意，顺序不同的序列被视作不同的组合。
```

**示例 2：**

```
输入：nums = [9], target = 3
输出：0
```

```c++
class Solution {
public:
    int combinationSum4(vector<int>& nums, int target) {
        vector<int>dp(target+1,0);
        dp[0]=1;
        for(int i=0;i<=target;i++){
            for(int j=0;j<nums.size();j++){
                if(i-nums[j]>=0&&dp[i] < INT_MAX - dp[i - nums[j]]){
                    dp[i]+=dp[i-nums[j]];
                }
            }
        }
        return dp[target];

    }
};
```

#### >>322. 零钱兑换

给你一个整数数组 `coins` ，表示不同面额的硬币；以及一个整数 `amount` ，表示总金额。

计算并返回可以凑成总金额所需的 **最少的硬币个数** 。如果没有任何一种硬币组合能组成总金额，返回 `-1` 。

你可以认为每种硬币的数量是无限的。 

**示例 1：**

```
输入：coins = [1, 2, 5], amount = 11
输出：3 
解释：11 = 5 + 5 + 1
```

**示例 2：**

```
输入：coins = [2], amount = 3
输出：-1
```

**示例 3：**

```
输入：coins = [1], amount = 0
输出：0
```

```c++
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        vector<int>dp(amount+1,INT_MAX);
        dp[0]=0;
        for(int i=1;i<=amount;i++){
            for(int j=0;j<coins.size();j++){
                if(i-coins[j]>=0&&dp[i-coins[j]]!=INT_MAX){
                    dp[i] = min(dp[i - coins[j]] + 1, dp[i]);
                }
            }
        }
        if(dp[amount]==INT_MAX){
            return -1;
        }
        return dp[amount];
    }
};

class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        vector<int> dp(amount + 1, INT_MAX);
        dp[0] = 0;
        for (int i = 0; i < coins.size(); i++) {
            for (int j = coins[i]; j <= amount; j++) { 
                if (dp[j - coins[i]] != INT_MAX) { 
                    dp[j] = min(dp[j - coins[i]] + 1, dp[j]);
                }
            }
        }
        if (dp[amount] == INT_MAX) return -1;
        return dp[amount];
    }
};
```

#### 279. 完全平方数

给你一个整数 `n` ，返回 *和为 `n` 的完全平方数的最少数量* 。

**完全平方数** 是一个整数，其值等于另一个整数的平方；换句话说，其值等于一个整数自乘的积。例如，`1`、`4`、`9` 和 `16` 都是完全平方数，而 `3` 和 `11` 不是。

**示例 1：**

```
输入：n = 12
输出：3 
解释：12 = 4 + 4 + 4
```

**示例 2：**

```
输入：n = 13
输出：2
解释：13 = 4 + 9
```

```c++
class Solution {
public:
    int numSquares(int n) {
        vector<int>dp(n+1,INT_MAX);
        dp[0]=0;
        for(int i=0;i<=n;i++){
            for(int j=1;j*j<=i;j++){
                dp[i]=min(dp[i-j*j]+1,dp[i]);
            }
        }
        return dp[n];
    }
};
```

#### >>139. 单词拆分

给你一个字符串 `s` 和一个字符串列表 `wordDict` 作为字典。请你判断是否可以利用字典中出现的单词拼接出 `s` 。

**注意：**不要求字典中出现的单词全部都使用，并且字典中的单词可以重复使用。

**示例 1：**

```c++
输入: s = "leetcode", wordDict = ["leet", "code"]
输出: true
解释: 返回 true 因为 "leetcode" 可以由 "leet" 和 "code" 拼接成。
```

**示例 2：**

```c++
输入: s = "applepenapple", wordDict = ["apple", "pen"]
输出: true
解释: 返回 true 因为 "applepenapple" 可以由 "apple" "pen" "apple" 拼接成。
     注意，你可以重复使用字典中的单词。
```

**示例 3：**

```c++
输入: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
输出: false
```

```c++
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        vector<bool>dp(s.size()+1,false);
        unordered_set<string>set(wordDict.begin(),wordDict.end());
        dp[0]=true;
        for(int i=1;i<=s.size();i++){
            for(int j=0;j<i;j++){
                string str=s.substr(j,i-j);
                if(set.find(str)!=set.end()&&dp[j]==true){
                    dp[i]=true;
                }
            }
        }  
        if(dp[s.size()]==true){
            return true;
        }
        return false;
    }
};
```

### 打家劫舍

#### 198. 打家劫舍

你是一个专业的小偷，计划偷窃沿街的房屋。每间房内都藏有一定的现金，影响你偷窃的唯一制约因素就是相邻的房屋装有相互连通的防盗系统，**如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警**。

给定一个代表每个房屋存放金额的非负整数数组，计算你 **不触动警报装置的情况下** ，一夜之内能够偷窃到的最高金额。

 

**示例 1：**

```
输入：[1,2,3,1]
输出：4
解释：偷窃 1 号房屋 (金额 = 1) ，然后偷窃 3 号房屋 (金额 = 3)。
     偷窃到的最高金额 = 1 + 3 = 4 。
```

**示例 2：**

```
输入：[2,7,9,3,1]
输出：12
解释：偷窃 1 号房屋 (金额 = 2), 偷窃 3 号房屋 (金额 = 9)，接着偷窃 5 号房屋 (金额 = 1)。
     偷窃到的最高金额 = 2 + 9 + 1 = 12 。
```

```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        if(nums.size()==0){
            return 0;
        }
        if(nums.size()==1){
            return nums[0];
        }
        vector<int>dp(nums.size());
        dp[0]=nums[0];
        dp[1]=max(nums[0],nums[1]);
        for(int i=2;i<nums.size();i++){
            dp[i]=max(dp[i-1],dp[i-2]+nums[i]);
        }
        return dp[nums.size()-1];
    }
};
```

#### 213. 打家劫舍 II

你是一个专业的小偷，计划偷窃沿街的房屋，每间房内都藏有一定的现金。这个地方所有的房屋都 **围成一圈** ，这意味着第一个房屋和最后一个房屋是紧挨着的。同时，相邻的房屋装有相互连通的防盗系统，**如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警** 。

给定一个代表每个房屋存放金额的非负整数数组，计算你 **在不触动警报装置的情况下** ，今晚能够偷窃到的最高金额。

 

**示例 1：**

```
输入：nums = [2,3,2]
输出：3
解释：你不能先偷窃 1 号房屋（金额 = 2），然后偷窃 3 号房屋（金额 = 2）, 因为他们是相邻的。
```

**示例 2：**

```
输入：nums = [1,2,3,1]
输出：4
解释：你可以先偷窃 1 号房屋（金额 = 1），然后偷窃 3 号房屋（金额 = 3）。
     偷窃到的最高金额 = 1 + 3 = 4 。
```

**示例 3：**

```
输入：nums = [1,2,3]
输出：3
```

```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        if(nums.size()==0){
            return 0;
        }
        if(nums.size()==1){
            return nums[0];
        }
        int ans1=func(nums,0,nums.size()-2);
        int ans2=func(nums,1,nums.size()-1);
        return max(ans1,ans2);
    }

    int func(vector<int>&nums,int start,int end){
        if(start==end){
            return nums[start];
        }
        vector<int>dp(nums.size());
        dp[start]=nums[start];
        dp[start+1]=max(nums[start+1],nums[start]);
        for(int i=start+2;i<=end;i++){
            dp[i]=max(dp[i-1],dp[i-2]+nums[i]);
        }
        return dp[end];
    }
};
```

#### >>337. 打家劫舍 III

小偷又发现了一个新的可行窃的地区。这个地区只有一个入口，我们称之为 `root` 。

除了 `root` 之外，每栋房子有且只有一个“父“房子与之相连。一番侦察之后，聪明的小偷意识到“这个地方的所有房屋的排列类似于一棵二叉树”。 如果 **两个直接相连的房子在同一天晚上被打劫** ，房屋将自动报警。

给定二叉树的 `root` 。返回 ***在不触动警报的情况下** ，小偷能够盗取的最高金额* 。

 

**示例 1:**

![img](https://assets.leetcode.com/uploads/2021/03/10/rob1-tree.jpg)

```
输入: root = [3,2,3,null,3,null,1]
输出: 7 
解释: 小偷一晚能够盗取的最高金额 3 + 3 + 1 = 7
```

**示例 2:**

![img](https://assets.leetcode.com/uploads/2021/03/10/rob2-tree.jpg)

```v++
输入: root = [3,4,5,1,3,null,1]
输出: 9
解释: 小偷一晚能够盗取的最高金额 4 + 5 = 9
```

```c++
class Solution {
public:
    vector<int> func(TreeNode*root){
        if(root==NULL){
            return {0,0};           
        }
        vector<int>left=func(root->left);
        vector<int>right=func(root->right);
        int val1=root->val+left[0]+right[0];
        int val2=max(left[0],left[1])+max(right[0],right[1]);
        return {val2,val1};
    }
    int rob(TreeNode* root) {
        vector<int>dp=func(root);
        return max(dp[0],dp[1]);
    }
};
```

### 股票问题

#### 121. 买卖股票的最佳时机

给定一个数组 `prices` ，它的第 `i` 个元素 `prices[i]` 表示一支给定股票第 `i` 天的价格。

你只能选择 **某一天** 买入这只股票，并选择在 **未来的某一个不同的日子** 卖出该股票。设计一个算法来计算你所能获取的最大利润。

返回你可以从这笔交易中获取的最大利润。如果你不能获取任何利润，返回 `0` 。

**示例 1：**

```
输入：[7,1,5,3,6,4]
输出：5
解释：在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格；同时，你不能在买入前卖出股票。
```

**示例 2：**

```
输入：prices = [7,6,4,3,1]
输出：0
解释：在这种情况下, 没有交易完成, 所以最大利润为 0。
```

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int len=prices.size();
        if(len==0){
            return 0;
        }
        vector<vector<int>>dp(len,vector<int>(2,0));
        dp[0][0] -= prices[0];
        dp[0][1] = 0;
        for(int i=1;i<len;i++){
            dp[i][0] = max(dp[i - 1][0], -prices[i]);
            dp[i][1] = max(dp[i - 1][1], prices[i] + dp[i - 1][0]);
        }
        return dp[len-1][1];
    }
};
```

#### 122. 买卖股票的最佳时机 II

给你一个整数数组 `prices` ，其中 `prices[i]` 表示某支股票第 `i` 天的价格。

在每一天，你可以决定是否购买和/或出售股票。你在任何时候 **最多** 只能持有 **一股** 股票。你也可以先购买，然后在 **同一天** 出售。

返回 *你能获得的 **最大** 利润* 。

**示例 1：**

```
输入：prices = [7,1,5,3,6,4]
输出：7
解释：在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5 - 1 = 4 。
     随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6 - 3 = 3 。
     总利润为 4 + 3 = 7 。
```

**示例 2：**

```
输入：prices = [1,2,3,4,5]
输出：4
解释：在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5 - 1 = 4 。
     总利润为 4 。
```

**示例 3：**

```
输入：prices = [7,6,4,3,1]
输出：0
解释：在这种情况下, 交易无法获得正利润，所以不参与交易可以获得最大利润，最大利润为 0 。
```

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        vector<vector<int>>dp(prices.size(),vector<int>(2));
        dp[0][0]=-prices[0];
        dp[0][1]=0;
        for(int i=1;i<prices.size();i++){
            dp[i][0]=max(dp[i-1][0],dp[i-1][1]-prices[i]);
            dp[i][1]=max(dp[i-1][1],dp[i-1][0]+prices[i]);
        }
        return dp[prices.size()-1][1];
    }
};
```

#### >>123. 买卖股票的最佳时机 III

给定一个数组，它的第 `i` 个元素是一支给定的股票在第 `i` 天的价格。

设计一个算法来计算你所能获取的最大利润。你最多可以完成 **两笔** 交易。

**注意：**你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

**示例 1:**

```
输入：prices = [3,3,5,0,0,3,1,4]
输出：6
解释：在第 4 天（股票价格 = 0）的时候买入，在第 6 天（股票价格 = 3）的时候卖出，这笔交易所能获得利润 = 3-0 = 3 。
     随后，在第 7 天（股票价格 = 1）的时候买入，在第 8 天 （股票价格 = 4）的时候卖出，这笔交易所能获得利润 = 4-1 = 3 。
```

**示例 2：**

```
输入：prices = [1,2,3,4,5]
输出：4
解释：在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。   
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。   
     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
```

**示例 3：**

```
输入：prices = [7,6,4,3,1] 
输出：0 
解释：在这个情况下, 没有交易完成, 所以最大利润为 0。
```

**示例 4：**

```
输入：prices = [1]
输出：0
```

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        vector<vector<int>>dp(prices.size(),vector<int>(5));
        dp[0][1]=-prices[0];
        dp[0][3]=-prices[0];
        for(int i=1;i<prices.size();i++){
            dp[i][0]=dp[i-1][0];
            dp[i][1]=max(dp[i-1][1],dp[i-1][0]-prices[i]);
            dp[i][2]=max(dp[i-1][2],dp[i-1][1]+prices[i]);
            dp[i][3]=max(dp[i-1][3],dp[i-1][2]-prices[i]);
            dp[i][4]=max(dp[i-1][4],dp[i-1][3]+prices[i]);
        }
        return dp[prices.size()-1][4];
    }
}
```

#### >>188. 买卖股票的最佳时机 IV

给定一个整数数组 `prices` ，它的第 `i` 个元素 `prices[i]` 是一支给定的股票在第 `i` 天的价格。

设计一个算法来计算你所能获取的最大利润。你最多可以完成 **k** 笔交易。

**注意：**你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

**示例 1：**

```
输入：k = 2, prices = [2,4,1]
输出：2
解释：在第 1 天 (股票价格 = 2) 的时候买入，在第 2 天 (股票价格 = 4) 的时候卖出，这笔交易所能获得利润 = 4-2 = 2 。
```

**示例 2：**

```
输入：k = 2, prices = [3,2,6,5,0,3]
输出：7
解释：在第 2 天 (股票价格 = 2) 的时候买入，在第 3 天 (股票价格 = 6) 的时候卖出, 这笔交易所能获得利润 = 6-2 = 4 。
     随后，在第 5 天 (股票价格 = 0) 的时候买入，在第 6 天 (股票价格 = 3) 的时候卖出, 这笔交易所能获得利润 = 3-0 = 3 。
```

```c++
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        if(prices.size()==0){
            return 0;
        }
        vector<vector<int>>dp(prices.size(),vector<int>(2*k+1));
        for(int i=1;i<2*k;i+=2){
            dp[0][i]=-prices[0];
        }
        for(int i=1;i<prices.size();i++){
            for(int j=0;j<2*k-1;j+=2){
                dp[i][j+1]=max(dp[i-1][j+1],dp[i-1][j]-prices[i]);
                dp[i][j+2]=max(dp[i-1][j+2],dp[i-1][j+1]+prices[i]);
            }
        }
        return dp[prices.size()-1][2*k];
    }
};
```

#### >>309. 最佳买卖股票时机含冷冻期

给定一个整数数组`prices`，其中第 `prices[i]` 表示第 `*i*` 天的股票价格 。

设计一个算法计算出最大利润。在满足以下约束条件下，你可以尽可能地完成更多的交易（多次买卖一支股票）:

- 卖出股票后，你无法在第二天买入股票 (即冷冻期为 1 天)。

**注意：**你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

 

**示例 1:**

```c++
输入: prices = [1,2,3,0,2]
输出: 3 
解释: 对应的交易状态为: [买入, 卖出, 冷冻期, 买入, 卖出]
```

**示例 2:**

```c++
输入: prices = [1]
输出: 0
```

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        if (n == 0) return 0;
        vector<vector<int>> dp(n, vector<int>(4, 0));
        dp[0][0] -= prices[0]; 
        for (int i = 1; i < n; i++) {
            dp[i][0] = max(dp[i - 1][0], max(dp[i - 1][3], dp[i - 1][1]) - prices[i]);
            dp[i][1] = max(dp[i - 1][1], dp[i - 1][3]);
            dp[i][2] = dp[i - 1][0] + prices[i];
            dp[i][3] = dp[i - 1][2];
        }
        return max(dp[n - 1][3],max(dp[n - 1][1], dp[n - 1][2]));
    }
};
```

#### 714. 买卖股票的最佳时机含手续费

给定一个整数数组 `prices`，其中 `prices[i]`表示第 `i` 天的股票价格 ；整数 `fee` 代表了交易股票的手续费用。

你可以无限次地完成交易，但是你每笔交易都需要付手续费。如果你已经购买了一个股票，在卖出它之前你就不能再继续购买股票了。

返回获得利润的最大值。

**注意：**这里的一笔交易指买入持有并卖出股票的整个过程，每笔交易你只需要为支付一次手续费。

 

**示例 1：**

```
输入：prices = [1, 3, 2, 8, 4, 9], fee = 2
输出：8
解释：能够达到的最大利润:  
在此处买入 prices[0] = 1
在此处卖出 prices[3] = 8
在此处买入 prices[4] = 4
在此处卖出 prices[5] = 9
总利润: ((8 - 1) - 2) + ((9 - 4) - 2) = 8
```

**示例 2：**

```
输入：prices = [1,3,7,5,10,3], fee = 3
输出：6
```

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices, int fee) {
        int n = prices.size();
        vector<vector<int>> dp(n, vector<int>(2, 0));
        dp[0][0] -= prices[0]; // 持股票
        for (int i = 1; i < n; i++) {
            dp[i][0] = max(dp[i - 1][0], dp[i - 1][1] - prices[i]);
            dp[i][1] = max(dp[i - 1][1], dp[i - 1][0] + prices[i] - fee);
        }
        return max(dp[n - 1][0], dp[n - 1][1]);
    }
};
```

### 子序列问题

#### >>300. 最长递增子序列

给你一个整数数组 `nums` ，找到其中最长严格递增子序列的长度。

**子序列** 是由数组派生而来的序列，删除（或不删除）数组中的元素而不改变其余元素的顺序。例如，`[3,6,2,7]` 是数组 `[0,3,1,6,2,2,7]` 的子序列。

**示例 1：**

```
输入：nums = [10,9,2,5,3,7,101,18]
输出：4
解释：最长递增子序列是 [2,3,7,101]，因此长度为 4 。
```

**示例 2：**

```
输入：nums = [0,1,0,3,2,3]
输出：4
```

**示例 3：**

```
输入：nums = [7,7,7,7,7,7,7]
输出1
```

```c++
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
         vector<int>dp(nums.size(),1);
         if(nums.size()<=1){
             return nums.size();
         }
         int ans=0;
         for(int i=1;i<nums.size();i++){
             for(int j=0;j<i;j++){
                 if(nums[i]>nums[j]){
                     dp[i]=max(dp[i],dp[j]+1);
                 }
             }
            ans=max(ans,dp[i]);
         }
         return ans;

    }
};
```

#### 674. 最长连续递增序列

给定一个未经排序的整数数组，找到最长且 **连续递增的子序列**，并返回该序列的长度。

**连续递增的子序列** 可以由两个下标 `l` 和 `r`（`l < r`）确定，如果对于每个 `l <= i < r`，都有 `nums[i] < nums[i + 1]` ，那么子序列 `[nums[l], nums[l + 1], ..., nums[r - 1], nums[r]]` 就是连续递增子序列。

 

**示例 1：**

```
输入：nums = [1,3,5,4,7]
输出：3
解释：最长连续递增序列是 [1,3,5], 长度为3。
尽管 [1,3,5,7] 也是升序的子序列, 但它不是连续的，因为 5 和 7 在原数组里被 4 隔开。 
```

**示例 2：**

```
输入：nums = [2,2,2,2,2]
输出：1
解释：最长连续递增序列是 [2], 长度为1。
```

```c++
class Solution {
public:
    int findLengthOfLCIS(vector<int>& nums) {
        if(nums.size()<=1){
            return nums.size();
        }
        int ans=1;
        vector<int>dp(nums.size(),1);
        for(int i=0;i<nums.size()-1;i++){
            if(nums[i+1]>nums[i]){
                dp[i+1]=dp[i]+1;
            }
            if(dp[i+1]>ans){
                ans=dp[i+1];
            }
        }
        return ans;
    }
};

class Solution {
public:
    int findLengthOfLCIS(vector<int>& nums) {
        int ans=1;
        int count=1;
        for(int i=1;i<nums.size();i++){
            if(nums[i]>nums[i-1]){
                count++;
            }
            else{
                count=1;
            }
            ans=max(ans,count);
        }
        return ans;
    }
};
```

#### >>718. 最长重复子数组

给两个整数数组 `nums1` 和 `nums2` ，返回 *两个数组中 **公共的** 、长度最长的子数组的长度* 。

 

**示例 1：**

```
输入：nums1 = [1,2,3,2,1], nums2 = [3,2,1,4,7]
输出：3
解释：长度最长的公共子数组是 [3,2,1] 。
```

**示例 2：**

```
输入：nums1 = [0,0,0,0,0], nums2 = [0,0,0,0,0]
输出：5
```

```c++
class Solution {
public:
    int findLength(vector<int>& nums1, vector<int>& nums2) {
        vector<vector<int>>dp(nums1.size()+1,vector<int>(nums2.size()+1,0));
        int ans=0;
        for(int i=1;i<=nums1.size();i++){
            for(int j=1;j<=nums2.size();j++){
                if(nums1[i-1]==nums2[j-1]){
                    dp[i][j]=dp[i-1][j-1]+1;
                }
                ans=max(ans,dp[i][j]);
            }

        }
        return ans;
    }
};
```

#### 1143. 最长公共子序列

给定两个字符串 `text1` 和 `text2`，返回这两个字符串的最长 **公共子序列** 的长度。如果不存在 **公共子序列** ，返回 `0` 。

一个字符串的 **子序列** 是指这样一个新的字符串：它是由原字符串在不改变字符的相对顺序的情况下删除某些字符（也可以不删除任何字符）后组成的新字符串。

- 例如，`"ace"` 是 `"abcde"` 的子序列，但 `"aec"` 不是 `"abcde"` 的子序列。

两个字符串的 **公共子序列** 是这两个字符串所共同拥有的子序列。

 

**示例 1：**

```
输入：text1 = "abcde", text2 = "ace" 
输出：3  
解释：最长公共子序列是 "ace" ，它的长度为 3 。
```

**示例 2：**

```
输入：text1 = "abc", text2 = "abc"
输出：3
解释：最长公共子序列是 "abc" ，它的长度为 3 。
```

**示例 3：**

```
输入：text1 = "abc", text2 = "def"
输出：0
解释：两个字符串没有公共子序列，返回 0 。
```

```c++
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        vector<vector<int >>dp(text1.size()+1,vector<int>(text2.size()+1,0));
        for(int i=1;i<=text1.size();i++){
            for(int j=1;j<=text2.size();j++){
                if(text1[i-1]==text2[j-1]){
                    dp[i][j]=dp[i-1][j-1]+1;
                }
                else{
                    dp[i][j]=max(dp[i-1][j],dp[i][j-1]);
                }
            }
        }   
        return dp[text1.size()][text2.size()];
    }
};
```

#### 1035. 不相交的线

在两条独立的水平线上按给定的顺序写下 `nums1` 和 `nums2` 中的整数。

现在，可以绘制一些连接两个数字 `nums1[i]` 和 `nums2[j]` 的直线，这些直线需要同时满足满足：

-  `nums1[i] == nums2[j]`
- 且绘制的直线不与任何其他连线（非水平线）相交。

请注意，连线即使在端点也不能相交：每个数字只能属于一条连线。

以这种方法绘制线条，并返回可以绘制的最大连线数。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2019/04/26/142.png)

```
输入：nums1 = [1,4,2], nums2 = [1,2,4]
输出：2
解释：可以画出两条不交叉的线，如上图所示。 
但无法画出第三条不相交的直线，因为从 nums1[1]=4 到 nums2[2]=4 的直线将与从 nums1[2]=2 到 nums2[1]=2 的直线相交。
```

**示例 2：**

```
输入：nums1 = [2,5,1,2,5], nums2 = [10,5,2,1,5,2]
输出：3
```

**示例 3：**

```
输入：nums1 = [1,3,7,1,7,5], nums2 = [1,9,2,5,1]
输出：2
```

```c++
class Solution {
public:
    int maxUncrossedLines(vector<int>& nums1, vector<int>& nums2) {
        vector<vector<int>>dp(nums1.size()+1,vector<int>(nums2.size()+1,0));
        for(int i=1;i<=nums1.size();i++){
            for(int j=1;j<=nums2.size();j++){
                if(nums1[i-1]==nums2[j-1]){
                    dp[i][j]=dp[i-1][j-1]+1;
                }
                else{
                    dp[i][j]=max(dp[i-1][j],dp[i][j-1]);
                }
            }
        }
        return dp[nums1.size()][nums2.size()];
    }
};
```

#### 53. 最大子数组和

给你一个整数数组 `nums` ，请你找出一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

**子数组** 是数组中的一个连续部分。

 

**示例 1：**

```
输入：nums = [-2,1,-3,4,-1,2,1,-5,4]
输出：6
解释：连续子数组 [4,-1,2,1] 的和最大，为 6 。
```

**示例 2：**

```
输入：nums = [1]
输出：1
```

**示例 3：**

```
输入：nums = [5,4,-1,7,8]
输出：23
```

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int ans=nums[0];
        int sum=0;
        for(int i=0;i<nums.size();i++){
            sum=max(nums[i],sum+nums[i]);
            ans=max(sum,ans);
        }
        return ans;
    }
};

class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        if(nums.size()==0){
            return 0;
        }
        vector<int>dp(nums.size(),0);
        int ans=nums[0];
        dp[0]=nums[0];
        for(int i=1;i<nums.size();i++){
            dp[i]=max(nums[i],dp[i-1]+nums[i]);
            ans=max(ans,dp[i]);
        }
        return ans;
    }
};
```

#### 392. 判断子序列

给定字符串 **s** 和 **t** ，判断 **s** 是否为 **t** 的子序列。

字符串的一个子序列是原始字符串删除一些（也可以不删除）字符而不改变剩余字符相对位置形成的新字符串。（例如，`"ace"`是`"abcde"`的一个子序列，而`"aec"`不是）。

**进阶：**

如果有大量输入的 S，称作 S1, S2, ... , Sk 其中 k >= 10亿，你需要依次检查它们是否为 T 的子序列。在这种情况下，你会怎样改变代码？

**致谢：**

特别感谢 [@pbrother ](https://leetcode.com/pbrother/)添加此问题并且创建所有测试用例。

 

**示例 1：**

```
输入：s = "abc", t = "ahbgdc"
输出：true
```

**示例 2：**

```
输入：s = "axc", t = "ahbgdc"
输出：false
```

```c++
class Solution {
public:
    bool isSubsequence(string s, string t) {
        vector<vector<int>>dp(s.size()+1,vector<int>(t.size()+1,0));
        for(int i=1;i<=s.size();i++){
            for(int j=1;j<=t.size();j++){
                if(s[i-1]==t[j-1]){
                    dp[i][j]=dp[i-1][j-1]+1;
                }else{
                    dp[i][j]=dp[i][j-1];
                }
            }
        }
        if(dp[s.size()][t.size()]==s.size()){
            return true;
        }
        return false;
    }
};
```

#### 673. 最长递增子序列的个数

给定一个未排序的整数数组 `nums` ， *返回最长递增子序列的个数* 。

**注意** 这个数列必须是 **严格** 递增的。

**示例 1:**

```
输入: [1,3,5,4,7]
输出: 2
解释: 有两个最长递增子序列，分别是 [1, 3, 4, 7] 和[1, 3, 5, 7]。
```

**示例 2:**

```
输入: [2,2,2,2,2]
输出: 5
解释: 最长递增子序列的长度是1，并且存在5个子序列的长度为1，因此输出5。
```

```c++

```



#### >>115. 不同的子序列

给定一个字符串 `s` 和一个字符串 `t` ，计算在 `s` 的子序列中 `t` 出现的个数。

字符串的一个 **子序列** 是指，通过删除一些（也可以不删除）字符且不干扰剩余字符相对位置所组成的新字符串。（例如，`"ACE"` 是 `"ABCDE"` 的一个子序列，而 `"AEC"` 不是）

题目数据保证答案符合 32 位带符号整数范围。

**示例 1：**

```
输入：s = "rabbbit", t = "rabbit"
输出：3
解释：
如下图所示, 有 3 种可以从 s 中得到 "rabbit" 的方案。
rabbbit
rabbbit
rabbbit
```

**示例 2：**

```
输入：s = "babgbag", t = "bag"
输出：5
解释：
如下图所示, 有 5 种可以从 s 中得到 "bag" 的方案。 
babgbag
babgbag
babgbag
babgbag
babgbag
```

```c++

```

#### 583. 两个字符串的删除操作

给定两个单词 `word1` 和 `word2` ，返回使得 `word1` 和 `word2` **相同**所需的**最小步数**。

**每步** 可以删除任意一个字符串中的一个字符。

 

**示例 1：**

```
输入: word1 = "sea", word2 = "eat"
输出: 2
解释: 第一步将 "sea" 变为 "ea" ，第二步将 "eat "变为 "ea"
```

**示例  2:**

```
输入：word1 = "leetcode", word2 = "etco"
输出：4
```

```c++
class Solution {
public:
    int minDistance(string word1, string word2) {
        vector<vector<int>>dp(word1.size()+1,vector<int>(word2.size()+1,0));
        for(int i=1;i<=word1.size();i++){
            for(int j=1;j<=word2.size();j++){
                if(word1[i-1]==word2[j-1]){
                    dp[i][j]=dp[i-1][j-1]+1;
                }
                else{
                    dp[i][j]=max(dp[i][j-1],dp[i-1][j]);
                }
            }
        }
        return word1.size()+word2.size()-2*dp[word1.size()][word2.size()];
    }
};
```

#### >>72. 编辑距离

给你两个单词 `word1` 和 `word2`， *请返回将 `word1` 转换成 `word2` 所使用的最少操作数* 。

你可以对一个单词进行如下三种操作：

- 插入一个字符
- 删除一个字符
- 替换一个字符

**示例 1：**

```
输入：word1 = "horse", word2 = "ros"
输出：3
解释：
horse -> rorse (将 'h' 替换为 'r')
rorse -> rose (删除 'r')
rose -> ros (删除 'e')
```

**示例 2：**

```
输入：word1 = "intention", word2 = "execution"
输出：5
解释：
intention -> inention (删除 't')
inention -> enention (将 'i' 替换为 'e')
enention -> exention (将 'n' 替换为 'x')
exention -> exection (将 'n' 替换为 'c')
exection -> execution (插入 'u')
```

```c++

```

#### >>647. 回文子串

给你一个字符串 `s` ，请你统计并返回这个字符串中 **回文子串** 的数目。

**回文字符串** 是正着读和倒过来读一样的字符串。

**子字符串** 是字符串中的由连续字符组成的一个序列。

具有不同开始位置或结束位置的子串，即使是由相同的字符组成，也会被视作不同的子串。

 

**示例 1：**

```
输入：s = "abc"
输出：3
解释：三个回文子串: "a", "b", "c"
```

**示例 2：**

```
输入：s = "aaa"
输出：6
解释：6个回文子串: "a", "a", "a", "aa", "aa", "aaa"
```

```c++
class Solution {
public:
    int countSubstrings(string s) {
        vector<vector<bool>>dp(s.size(),vector<bool>(s.size(),false));
        int count=0;
        for(int i=s.size()-1;i>=0;i--){
            for(int j=i;j<s.size();j++){
                if(s[i]==s[j] &&(j-i<=1 || dp[i+1][j-1]==true)){
                    count++;
                    dp[i][j]=true;
                }
            }
        }
        return count;
    }
};
```

#### >>516. 最长回文子序列

给你一个字符串 `s` ，找出其中最长的回文子序列，并返回该序列的长度。

子序列定义为：不改变剩余字符顺序的情况下，删除某些字符或者不删除任何字符形成的一个序列。

**示例 1：**

```
输入：s = "bbbab"
输出：4
解释：一个可能的最长回文子序列为 "bbbb" 。
```

**示例 2：**

```
输入：s = "cbbd"
输出：2
解释：一个可能的最长回文子序列为 "bb" 。
```

```c++
class Solution {
public:
    int longestPalindromeSubseq(string s) {
        vector<vector<int>> dp(s.size(), vector<int>(s.size(), 0));
        for (int i = 0; i < s.size(); i++) dp[i][i] = 1;
        for (int i = s.size() - 1; i >= 0; i--) {
            for (int j = i + 1; j < s.size(); j++) {
                if (s[i] == s[j]) {
                    dp[i][j] = dp[i + 1][j - 1] + 2;
                } else {
                    dp[i][j] = max(dp[i + 1][j], dp[i][j - 1]);
                }
            }
        }
        return dp[0][s.size() - 1];
    }
};
```

#### >>5. 最长回文子串

给你一个字符串 `s`，找到 `s` 中最长的回文子串。

**示例 1：**

```
输入：s = "babad"
输出："bab"
解释："aba" 同样是符合题意的答案。
```

**示例 2：**

```
输入：s = "cbbd"
输出："bb"
```

```c++
class Solution {
public:
    string longestPalindrome(string s) {
        int left=0;
        int right=0;
        int maxlength=0;
        vector<vector<int>>dp(s.size(),vector<int>(s.size(),0));
        for(int i=s.size()-1;i>=0;i--){
            for(int j=i;j<s.size();j++){
                if(s[i]==s[j]){
                    if(j-i<=1){
                        dp[i][j]=true;
                    }
                    else if(dp[i+1][j-1]){                       
                        dp[i][j]=true;                        
                    }
                }
                if(dp[i][j]&&j-i+1>maxlength){
                    left=i;
                    right=j;
                    maxlength=j-i+1;
                }
            }
        }
        return s.substr(left,maxlength);     
    }
};
```

#### >>132. 分割回文串 II

给你一个字符串 `s`，请你将 `s` 分割成一些子串，使每个子串都是回文。

返回符合要求的 **最少分割次数** 。

**示例 1：**

```
输入：s = "aab"
输出：1
解释：只需一次分割就可将 s 分割成 ["aa","b"] 这样两个回文子串。
```

**示例 2：**

```
输入：s = "a"
输出：0
```

**示例 3：**

```
输入：s = "ab"
输出：1
```

```c++

```



## 图

#### >>841. 钥匙和房间]

有 `n` 个房间，房间按从 `0` 到 `n - 1` 编号。最初，除 `0` 号房间外的其余所有房间都被锁住。你的目标是进入所有的房间。然而，你不能在没有获得钥匙的时候进入锁住的房间。

当你进入一个房间，你可能会在里面找到一套不同的钥匙，每把钥匙上都有对应的房间号，即表示钥匙可以打开的房间。你可以拿上所有钥匙去解锁其他房间。

给你一个数组 `rooms` 其中 `rooms[i]` 是你进入 `i` 号房间可以获得的钥匙集合。如果能进入 **所有** 房间返回 `true`，否则返回 `false`。

**示例 1：**

```
输入：rooms = [[1],[2],[3],[]]
输出：true
解释：
我们从 0 号房间开始，拿到钥匙 1。
之后我们去 1 号房间，拿到钥匙 2。
然后我们去 2 号房间，拿到钥匙 3。
最后我们去了 3 号房间。
由于我们能够进入每个房间，我们返回 true。
```

**示例 2：**

```
输入：rooms = [[1,3],[3,0,1],[2],[0]]
输出：false
解释：我们不能进入 2 号房间。
```

```c++

```

#### >>127. 单词接龙

字典 `wordList` 中从单词 `beginWord` 和 `endWord` 的 **转换序列** 是一个按下述规格形成的序列 `beginWord -> s1 -> s2 -> ... -> sk`：

- 每一对相邻的单词只差一个字母。
-  对于 `1 <= i <= k` 时，每个 `si` 都在 `wordList` 中。注意， `beginWord` 不需要在 `wordList` 中。
- `sk == endWord`

给你两个单词 `beginWord` 和 `endWord` 和一个字典 `wordList` ，返回 *从 `beginWord` 到 `endWord` 的 **最短转换序列** 中的 **单词数目*** 。如果不存在这样的转换序列，返回 `0` 。

**示例 1：**

```
输入：beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
输出：5
解释：一个最短转换序列是 "hit" -> "hot" -> "dot" -> "dog" -> "cog", 返回它的长度 5。
```

**示例 2：**

```
输入：beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]
输出：0
解释：endWord "cog" 不在字典中，所以无法进行转换。
```

```c++

```

#### >>684. 冗余连接

树可以看成是一个连通且 **无环** 的 **无向** 图。

给定往一棵 `n` 个节点 (节点值 `1～n`) 的树中添加一条边后的图。添加的边的两个顶点包含在 `1` 到 `n` 中间，且这条附加的边不属于树中已存在的边。图的信息记录于长度为 `n` 的二维数组 `edges` ，`edges[i] = [ai, bi]` 表示图中在 `ai` 和 `bi` 之间存在一条边。

请找出一条可以删去的边，删除后可使得剩余部分是一个有着 `n` 个节点的树。如果有多个答案，则返回数组 `edges` 中最后出现的边。

 

**示例 1：**

![img](https://pic.leetcode-cn.com/1626676174-hOEVUL-image.png)

```
输入: edges = [[1,2], [1,3], [2,3]]
输出: [2,3]
```

**示例 2：**

![img](https://pic.leetcode-cn.com/1626676179-kGxcmu-image.png)

```
输入: edges = [[1,2], [2,3], [3,4], [1,4], [1,5]]
输出: [1,4]
```

```c++

```

#### >>685. 冗余连接 II

在本问题中，有根树指满足以下条件的 **有向** 图。该树只有一个根节点，所有其他节点都是该根节点的后继。该树除了根节点之外的每一个节点都有且只有一个父节点，而根节点没有父节点。

输入一个有向图，该图由一个有着 `n` 个节点（节点值不重复，从 `1` 到 `n`）的树及一条附加的有向边构成。附加的边包含在 `1` 到 `n` 中的两个不同顶点间，这条附加的边不属于树中已存在的边。

结果图是一个以边组成的二维数组 `edges` 。 每个元素是一对 `[ui, vi]`，用以表示 **有向** 图中连接顶点 `ui` 和顶点 `vi` 的边，其中 `ui` 是 `vi` 的一个父节点。

返回一条能删除的边，使得剩下的图是有 `n` 个节点的有根树。若有多个答案，返回最后出现在给定二维数组的答案。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/12/20/graph1.jpg)

```
输入：edges = [[1,2],[1,3],[2,3]]
输出：[2,3]
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/12/20/graph2.jpg)

```
输入：edges = [[1,2],[2,3],[3,4],[4,1],[1,5]]
输出：[4,1]
```

#### >>207. 课程表

你这个学期必须选修 `numCourses` 门课程，记为 `0` 到 `numCourses - 1` 。

在选修某些课程之前需要一些先修课程。 先修课程按数组 `prerequisites` 给出，其中 `prerequisites[i] = [ai, bi]` ，表示如果要学习课程 `ai` 则 **必须** 先学习课程 `bi` 。

- 例如，先修课程对 `[0, 1]` 表示：想要学习课程 `0` ，你需要先完成课程 `1` 。

请你判断是否可能完成所有课程的学习？如果可以，返回 `true` ；否则，返回 `false` 。

 

**示例 1：**

```
输入：numCourses = 2, prerequisites = [[1,0]]
输出：true
解释：总共有 2 门课程。学习课程 1 之前，你需要完成课程 0 。这是可能的。
```

**示例 2：**

```
输入：numCourses = 2, prerequisites = [[1,0],[0,1]]
输出：false
解释：总共有 2 门课程。学习课程 1 之前，你需要先完成课程 0 ；并且学习课程 0 之前，你还应先完成课程 1 。这是不可能的。
```

```c++

```

#### >>399. 除法求值

给你一个变量对数组 `equations` 和一个实数值数组 `values` 作为已知条件，其中 `equations[i] = [Ai, Bi]` 和 `values[i]` 共同表示等式 `Ai / Bi = values[i]` 。每个 `Ai` 或 `Bi` 是一个表示单个变量的字符串。

另有一些以数组 `queries` 表示的问题，其中 `queries[j] = [Cj, Dj]` 表示第 `j` 个问题，请你根据已知条件找出 `Cj / Dj = ?` 的结果作为答案。

返回 **所有问题的答案** 。如果存在某个无法确定的答案，则用 `-1.0` 替代这个答案。如果问题中出现了给定的已知条件中没有出现的字符串，也需要用 `-1.0` 替代这个答案。

**注意：**输入总是有效的。你可以假设除法运算中不会出现除数为 0 的情况，且不存在任何矛盾的结果。

 

**示例 1：**

```
输入：equations = [["a","b"],["b","c"]], values = [2.0,3.0], queries = [["a","c"],["b","a"],["a","e"],["a","a"],["x","x"]]
输出：[6.00000,0.50000,-1.00000,1.00000,-1.00000]
解释：
条件：a / b = 2.0, b / c = 3.0
问题：a / c = ?, b / a = ?, a / e = ?, a / a = ?, x / x = ?
结果：[6.0, 0.5, -1.0, 1.0, -1.0 ]
```

**示例 2：**

```
输入：equations = [["a","b"],["b","c"],["bc","cd"]], values = [1.5,2.5,5.0], queries = [["a","c"],["c","b"],["bc","cd"],["cd","bc"]]
输出：[3.75000,0.40000,5.00000,0.20000]
```

**示例 3：**

```
输入：equations = [["a","b"]], values = [0.5], queries = [["a","b"],["b","a"],["a","c"],["x","y"]]
输出：[0.50000,2.00000,-1.00000,-1.00000]
```

```c++

```



## 其他

#### 657. 机器人能否返回原点

在二维平面上，有一个机器人从原点 `(0, 0)` 开始。给出它的移动顺序，判断这个机器人在完成移动后是否在 **`(0, 0)` 处结束**。

移动顺序由字符串 `moves` 表示。字符 `move[i]` 表示其第 `i` 次移动。机器人的有效动作有 `R`（右），`L`（左），`U`（上）和 `D`（下）。

如果机器人在完成所有动作后返回原点，则返回 `true`。否则，返回 `false`。

**注意：**机器人“面朝”的方向无关紧要。 `“R”` 将始终使机器人向右移动一次，`“L”` 将始终向左移动等。此外，假设每次移动机器人的移动幅度相同。

**示例 1:**

```
输入: moves = "UD"
输出: true
解释：机器人向上移动一次，然后向下移动一次。所有动作都具有相同的幅度，因此它最终回到它开始的原点。因此，我们返回 true。
```

**示例 2:**

```
输入: moves = "LL"
输出: false
解释：机器人向左移动两次。它最终位于原点的左侧，距原点有两次 “移动” 的距离。我们返回 false，因为它在移动结束时没有返回原点。
```

```c++
class Solution {
public:
    bool judgeCircle(string moves) {
        int u=0;
        int r=0;
        for(int i=0;i<moves.size();i++){
            if(moves[i]=='U'){
                u++;
            }
            if(moves[i]=='D'){
                u--;
            }
            if(moves[i]=='L'){
                r--;
            }
            if(moves[i]=='R'){
                r++;
            }
        }
        if(u || r){
            return false;
        }
        return true;
    }
};
```

#### 463. 岛屿的周长

给定一个 `row x col` 的二维网格地图 `grid` ，其中：`grid[i][j] = 1` 表示陆地， `grid[i][j] = 0` 表示水域。

网格中的格子 **水平和垂直** 方向相连（对角线方向不相连）。整个网格被水完全包围，但其中恰好有一个岛屿（或者说，一个或多个表示陆地的格子相连组成的岛屿）。

岛屿中没有“湖”（“湖” 指水域在岛屿内部且不和岛屿周围的水相连）。格子是边长为 1 的正方形。网格为长方形，且宽度和高度均不超过 100 。计算这个岛屿的周长。

 

**示例 1：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/island.png)

```
输入：grid = [[0,1,0,0],[1,1,1,0],[0,1,0,0],[1,1,0,0]]
输出：16
解释：它的周长是上面图片中的 16 个黄色的边
```

**示例 2：**

```
输入：grid = [[1]]
输出：4
```

**示例 3：**

```
输入：grid = [[1,0]]
输出：4
```

```c++
class Solution {
public:
    int islandPerimeter(vector<vector<int>>& grid) {
        if(grid.size()==0){
            return 0;
        }
        int count=0;
        for(int i=0;i<grid.size();i++){
            for(int j=0;j<grid[i].size();j++){
                if(grid[i][j]==1){
                    count+=4;
                    if(i>0&&grid[i-1][j]==1){
                        count-=2;
                    }
                    if(j>0&&grid[i][j-1]==1){
                        count-=2;
                    }
                }
                
            }
        }
        return count;

    }
};
```

#### >>1356. 根据数字二进制下 1 的数目排序

给你一个整数数组 `arr` 。请你将数组中的元素按照其二进制表示中数字 **1** 的数目升序排序。

如果存在多个数字二进制中 **1** 的数目相同，则必须将它们按照数值大小升序排列。

请你返回排序后的数组。

**示例 1：**

```
输入：arr = [0,1,2,3,4,5,6,7,8]
输出：[0,1,2,4,8,3,5,6,7]
解释：[0] 是唯一一个有 0 个 1 的数。
[1,2,4,8] 都有 1 个 1 。
[3,5,6] 有 2 个 1 。
[7] 有 3 个 1 。
按照 1 的个数排序得到的结果数组为 [0,1,2,4,8,3,5,6,7]
```

**示例 2：**

```
输入：arr = [1024,512,256,128,64,32,16,8,4,2,1]
输出：[1,2,4,8,16,32,64,128,256,512,1024]
解释：数组中所有整数二进制下都只有 1 个 1 ，所以你需要按照数值大小将它们排序。
```

**示例 3：**

```
输入：arr = [10000,10000]
输出：[10000,10000]
```

**示例 4：**

```
输入：arr = [2,3,5,7,11,13,17,19]
输出：[2,3,5,17,7,11,13,19]
```

**示例 5：**

```
输入：arr = [10,100,1000,10000]
输出：[10,100,10000,1000]
```

```c++
class Solution {
public:
    static int bitcount(int n){
        int count=0;
        while(n){
            n&=(n-1);
            count++;
        }
        return count;
    }
    static bool cmp(int a,int b){
        int bita=bitcount(a);
        int bitb=bitcount(b);
        if(bita==bitb){
            return a<b;
        }
        return bita<bitb;
    }
    vector<int> sortByBits(vector<int>& arr) {
        sort(arr.begin(),arr.end(),cmp);
        return arr;
    }
};
```

#### 190. 颠倒二进制位

颠倒给定的 32 位无符号整数的二进制位。

**提示：**

- 请注意，在某些语言（如 Java）中，没有无符号整数类型。在这种情况下，输入和输出都将被指定为有符号整数类型，并且不应影响您的实现，因为无论整数是有符号的还是无符号的，其内部的二进制表示形式都是相同的。
- 在 Java 中，编译器使用[二进制补码](https://baike.baidu.com/item/二进制补码/5295284)记法来表示有符号整数。因此，在 **示例 2** 中，输入表示有符号整数 `-3`，输出表示有符号整数 `-1073741825`。

 

**示例 1：**

```
输入：n = 00000010100101000001111010011100
输出：964176192 (00111001011110000010100101000000)
解释：输入的二进制串 00000010100101000001111010011100 表示无符号整数 43261596，
     因此返回 964176192，其二进制表示形式为 00111001011110000010100101000000。
```

**示例 2：**

```
输入：n = 11111111111111111111111111111101
输出：3221225471 (10111111111111111111111111111111)
解释：输入的二进制串 11111111111111111111111111111101 表示无符号整数 4294967293，
     因此返回 3221225471 其二进制表示形式为 10111111111111111111111111111111 。
```

```c++
class Solution {
public:
    uint32_t reverseBits(uint32_t n) {
        uint32_t ans=0;
        int a=32;
        while(a--){
            ans<<=1;
            ans+=n&1;
            n>>=1;
        }
        return ans;
    }
};
```

#### 191. 位1的个数

编写一个函数，输入是一个无符号整数（以二进制串的形式），返回其二进制表达式中数字位数为 '1' 的个数（也被称为[汉明重量](https://baike.baidu.com/item/汉明重量)）。

 

**提示：**

- 请注意，在某些语言（如 Java）中，没有无符号整数类型。在这种情况下，输入和输出都将被指定为有符号整数类型，并且不应影响您的实现，因为无论整数是有符号的还是无符号的，其内部的二进制表示形式都是相同的。
- 在 Java 中，编译器使用[二进制补码](https://baike.baidu.com/item/二进制补码/5295284)记法来表示有符号整数。因此，在上面的 **示例 3** 中，输入表示有符号整数 `-3`。

 

**示例 1：**

```
输入：00000000000000000000000000001011
输出：3
解释：输入的二进制串 00000000000000000000000000001011 中，共有三位为 '1'。
```

**示例 2：**

```
输入：00000000000000000000000010000000
输出：1
解释：输入的二进制串 00000000000000000000000010000000 中，共有一位为 '1'。
```

**示例 3：**

```
输入：11111111111111111111111111111101
输出：31
解释：输入的二进制串 11111111111111111111111111111101 中，共有 31 位为 '1'。
```

```c++
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int ans=0;
        int a=32;
        while(a--){
            if(n&1){
                ans++;
            }
            n>>=1;
        }   
        return ans;
    }
};
```

#### 326. 3 的幂

给定一个整数，写一个函数来判断它是否是 3 的幂次方。如果是，返回 `true` ；否则，返回 `false` 。

整数 `n` 是 3 的幂次方需满足：存在整数 `x` 使得 `n == 3x`

 

**示例 1：**

```
输入：n = 27
输出：true
```

**示例 2：**

```
输入：n = 0
输出：false
```

**示例 3：**

```
输入：n = 9
输出：true
```

**示例 4：**

```
输入：n = 45
输出：false
```

```c++
class Solution {
public:
    bool isPowerOfThree(int n) {
        if(n==0){
            return false;
        }
        while(n!=1){
            if(n%3){
                return false;
            }
            n/=3;
            
        }
        return true;
    }
};
```

#### 387. 字符串中的第一个唯一字符

给定一个字符串 `s` ，找到 *它的第一个不重复的字符，并返回它的索引* 。如果不存在，则返回 `-1` 。

 

**示例 1：**

```
输入: s = "leetcode"
输出: 0
```

**示例 2:**

```
输入: s = "loveleetcode"
输出: 2
```

**示例 3:**

```
输入: s = "aabb"
输出: -1
```

```c++
class Solution {
public:
    int firstUniqChar(string s) {
        int hash[26]={0};
        for(int i=0;i<s.size();i++){
            hash[s[i]-'a']++;
        }   
        for(int i=0;i<s.size();i++){
            if(hash[s[i]-'a']==1){
                return i;
            }
        }
        return -1;
    }
};
```

#### >>31. 下一个排列

整数数组的一个 **排列** 就是将其所有成员以序列或线性顺序排列。

- 例如，`arr = [1,2,3]` ，以下这些都可以视作 `arr` 的排列：`[1,2,3]`、`[1,3,2]`、`[3,1,2]`、`[2,3,1]` 。

整数数组的 **下一个排列** 是指其整数的下一个字典序更大的排列。更正式地，如果数组的所有排列根据其字典顺序从小到大排列在一个容器中，那么数组的 **下一个排列** 就是在这个有序容器中排在它后面的那个排列。如果不存在下一个更大的排列，那么这个数组必须重排为字典序最小的排列（即，其元素按升序排列）。

- 例如，`arr = [1,2,3]` 的下一个排列是 `[1,3,2]` 。
- 类似地，`arr = [2,3,1]` 的下一个排列是 `[3,1,2]` 。
- 而 `arr = [3,2,1]` 的下一个排列是 `[1,2,3]` ，因为 `[3,2,1]` 不存在一个字典序更大的排列。

给你一个整数数组 `nums` ，找出 `nums` 的下一个排列。

必须**[ 原地 ](https://baike.baidu.com/item/原地算法)**修改，只允许使用额外常数空间。

 

**示例 1：**

```
输入：nums = [1,2,3]
输出：[1,3,2]
```

**示例 2：**

```
输入：nums = [3,2,1]
输出：[1,2,3]
```

**示例 3：**

```
输入：nums = [1,1,5]
输出：[1,5,1]
```

```c++
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        for(int i=nums.size()-1;i>=0;i--){
            for(int j=nums.size()-1;j>i;j--){
                if(nums[j]>nums[i]){
                    swap(nums[i],nums[j]);
                    reverse(nums.begin()+i+1,nums.end());
                    return ;
                }
            }
        } 
        reverse(nums.begin(),nums.end());
    }
};
```

#### 32. 最长有效括号

给你一个只包含 `'('` 和 `')'` 的字符串，找出最长有效（格式正确且连续）括号子串的长度。

 

**示例 1：**

```
输入：s = "(()"
输出：2
解释：最长有效括号子串是 "()"
```

**示例 2：**

```
输入：s = ")()())"
输出：4
解释：最长有效括号子串是 "()()"
```

**示例 3：**

```
输入：s = ""
输出：0
```

```c++
class Solution {
public:
    int longestValidParentheses(string s) {
        if(s.size()==0){
            return 0;
        }
        vector<bool>b(s.size(),false);
        for(int i=0;i<s.size();i++){
            if(s[i]=='('){
                continue;
            }
            for(int j=i-1;j>=0;j--){
                if(b[j]==true){
                    continue;
                }
                else if(s[j]!='('){
                    break;
                }
                else if(s[j]=='('){
                    b[i]=true;
                    b[j]=true;
                    break;
                }
            }
        }
        int ans=0;
        int count=b[0];
        for(int i=1;i<s.size();i++){
            if(b[i]==false){
                count=0;
            }
            else{
                count++;
            }
            ans=max(ans,count);

        }
        return ans;
    }
};
```

#### >>146. LRU 缓存

请你设计并实现一个满足 [LRU (最近最少使用) 缓存](https://baike.baidu.com/item/LRU) 约束的数据结构。

实现 `LRUCache` 类：

- `LRUCache(int capacity)` 以 **正整数** 作为容量 `capacity` 初始化 LRU 缓存
- `int get(int key)` 如果关键字 `key` 存在于缓存中，则返回关键字的值，否则返回 `-1` 。
- `void put(int key, int value)` 如果关键字 `key` 已经存在，则变更其数据值 `value` ；如果不存在，则向缓存中插入该组 `key-value` 。如果插入操作导致关键字数量超过 `capacity` ，则应该 **逐出** 最久未使用的关键字。

函数 `get` 和 `put` 必须以 `O(1)` 的平均时间复杂度运行。

 

**示例：**

```
输入
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
输出
[null, null, null, 1, null, -1, null, -1, 3, 4]

解释
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // 缓存是 {1=1}
lRUCache.put(2, 2); // 缓存是 {1=1, 2=2}
lRUCache.get(1);    // 返回 1
lRUCache.put(3, 3); // 该操作会使得关键字 2 作废，缓存是 {1=1, 3=3}
lRUCache.get(2);    // 返回 -1 (未找到)
lRUCache.put(4, 4); // 该操作会使得关键字 1 作废，缓存是 {4=4, 3=3}
lRUCache.get(1);    // 返回 -1 (未找到)
lRUCache.get(3);    // 返回 3
lRUCache.get(4);    // 返回 4
```

```c++
struct Link{
    int key,value;
    Link*pre;
    Link*next;
    Link():key(0),value(0),pre(NULL),next(NULL){};
    Link(int _key,int _value):key(_key),value(_value),pre(NULL),next(NULL){};
};
class LRUCache {
private:
    unordered_map<int,Link*>cache;
    Link*head;
    Link*tail;
    int size;
    int capacity;
public:   
    LRUCache(int capacity):capacity(capacity),size(0) {
        head=new Link();
        tail=new Link();
        head->next=tail;
        tail->pre=head;
    }
    
    int get(int key) {
        if(!cache.count(key)){
            return -1;
        }
        Link*node=cache[key];
        movetohead(node);
        return node->value;
    }
    
    void put(int key, int value) {
        if(!cache.count(key)){
            Link*node=new Link(key,value);
            cache[key]=node;
            addtohead(node);
            size++;
            if(size>capacity){
                Link*removed=removetail();
                cache.erase(removed->key);
                delete removed;
                size--;
            }
        }
        else{
            Link*node=cache[key];
            node->value=value;
            movetohead(node);
        }
    }
    void addtohead(Link*node){
        node->pre=head;
        node->next=head->next;
        head->next->pre=node;
        head->next=node;
    }
    void removenode(Link*node){
        node->pre->next=node->next;
        node->next->pre=node->pre;
    }
    void movetohead(Link*node){
        removenode(node);
        addtohead(node);
    }
    Link*removetail(){
        Link*node=tail->pre;
        removenode(node);
        return node;
    }
};
```

#### >>208. 实现 Trie (前缀树)

**[Trie](https://baike.baidu.com/item/字典树/9825209?fr=aladdin)**（发音类似 "try"）或者说 **前缀树** 是一种树形数据结构，用于高效地存储和检索字符串数据集中的键。这一数据结构有相当多的应用情景，例如自动补完和拼写检查。

请你实现 Trie 类：

- `Trie()` 初始化前缀树对象。
- `void insert(String word)` 向前缀树中插入字符串 `word` 。
- `boolean search(String word)` 如果字符串 `word` 在前缀树中，返回 `true`（即，在检索之前已经插入）；否则，返回 `false` 。
- `boolean startsWith(String prefix)` 如果之前已经插入的字符串 `word` 的前缀之一为 `prefix` ，返回 `true` ；否则，返回 `false` 。

 

**示例：**

```
输入
["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
[[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]
输出
[null, null, true, false, true, null, true]

解释
Trie trie = new Trie();
trie.insert("apple");
trie.search("apple");   // 返回 True
trie.search("app");     // 返回 False
trie.startsWith("app"); // 返回 True
trie.insert("app");
trie.search("app");     // 返回 True
```

```c++
class Trie {
private:
    vector<Trie*> children;
    bool isEnd;

    Trie* searchPrefix(string prefix) {
        Trie* node = this;
        for (char ch : prefix) {
            ch -= 'a';
            if (node->children[ch] == nullptr) {
                return nullptr;
            }
            node = node->children[ch];
        }
        return node;
    }

public:
    Trie() : children(26), isEnd(false) {}

    void insert(string word) {
        Trie* node = this;
        for (char ch : word) {
            ch -= 'a';
            if (node->children[ch] == nullptr) {
                node->children[ch] = new Trie();
            }
            node = node->children[ch];
        }
        node->isEnd = true;
    }

    bool search(string word) {
        Trie* node = this->searchPrefix(word);
        return node != nullptr && node->isEnd;
    }

    bool startsWith(string prefix) {
        return this->searchPrefix(prefix) != nullptr;
    }
};
```

#### >>200. 岛屿数量

给你一个由 `'1'`（陆地）和 `'0'`（水）组成的的二维网格，请你计算网格中岛屿的数量。

岛屿总是被水包围，并且每座岛屿只能由水平方向和/或竖直方向上相邻的陆地连接形成。

此外，你可以假设该网格的四条边均被水包围。

 

**示例 1：**

```
输入：grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
输出：1
```

**示例 2：**

```
输入：grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
输出：3
```

```c++
class Solution {
public:
    void dfs(vector<vector<char>>&grid,int i,int j){
        if(i<0 || j<0 || i>=grid.size() ||j>=grid[0].size() || grid[i][j]=='0'){
            return ;
        }
        grid[i][j]='0';
        dfs(grid,i+1,j);
        dfs(grid,i-1,j);
        dfs(grid,i,j+1);
        dfs(grid,i,j-1);
    }
    int numIslands(vector<vector<char>>& grid) {
        int ans=0;
        for(int i=0;i<grid.size();i++){
            for(int j=0;j<grid[0].size();j++){
                if(grid[i][j]=='1'){
                    ans++;
                    dfs(grid,i,j);
                }
            }
        }
        return ans;
    }
};
```

#### 221. 最大正方形

在一个由 `'0'` 和 `'1'` 组成的二维矩阵内，找到只包含 `'1'` 的最大正方形，并返回其面积。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/26/max1grid.jpg)

```
输入：matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
输出：4
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/11/26/max2grid.jpg)

```
输入：matrix = [["0","1"],["1","0"]]
输出：1
```

**示例 3：**

```
输入：matrix = [["0"]]
输出：0
```

```c++
class Solution {
public:
    int maximalSquare(vector<vector<char>>& matrix) {
        vector<vector<int>>dp(matrix.size(),vector<int>(matrix[0].size(),0));
        int ans=0;
        for(int i=0;i<matrix.size();i++){
            dp[i][0]=matrix[i][0]-'0';
            ans=max(ans,dp[i][0]);
        }
        for(int j=0;j<matrix[0].size();j++){
            dp[0][j]=matrix[0][j]-'0';
            ans=max(ans,dp[0][j]);
        }
        for(int i=1;i<matrix.size();i++){
            for(int j=1;j<matrix[0].size();j++){
                if(matrix[i][j]=='0'){
                    continue;
                }
                if(dp[i-1][j-1]==0){
                    dp[i][j]=1;
                }
                else{
                    dp[i][j]=min(min(dp[i-1][j],dp[i][j-1]),dp[i-1][j-1])+1;
                }
                ans=max(ans,dp[i][j]);
            }
        }
        return ans*ans;
        
    }
};
```

#### 238. 除自身以外数组的乘积

给你一个整数数组 `nums`，返回 *数组 `answer` ，其中 `answer[i]` 等于 `nums` 中除 `nums[i]` 之外其余各元素的乘积* 。

题目数据 **保证** 数组 `nums`之中任意元素的全部前缀元素和后缀的乘积都在 **32 位** 整数范围内。

请**不要使用除法，**且在 `O(*n*)` 时间复杂度内完成此题。

 

**示例 1:**

```
输入: nums = [1,2,3,4]
输出: [24,12,8,6]
```

**示例 2:**

```
输入: nums = [-1,1,0,-3,3]
输出: [0,0,9,0,0]
```

```c++
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        vector<int>ans(nums.size(),1);
        int t=1;
        for(int i=1;i<nums.size();i++){
            t*=nums[i-1];
            ans[i]=t;
        }
        t=1;
        for(int i=nums.size()-1;i>0;i--){
            t*=nums[i];
            ans[i-1]*=t;
        }
        return ans;
    }
};
```

#### 240. 搜索二维矩阵 II

编写一个高效的算法来搜索 `*m* x *n*` 矩阵 `matrix` 中的一个目标值 `target` 。该矩阵具有以下特性：

- 每行的元素从左到右升序排列。
- 每列的元素从上到下升序排列。

 

**示例 1：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/11/25/searchgrid2.jpg)

```
输入：matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 5
输出：true
```

**示例 2：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/11/25/searchgrid.jpg)

```
输入：matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 20
输出：false
```

```c++
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int i=0;
        int j=matrix[0].size()-1;
        while(i<matrix.size()&&j>=0){
            if(matrix[i][j]<target){
                i++;
            }
            else if(matrix[i][j]>target){
                j--;
            }
            else{
                return true;
            }
        }  
        return false;
    }
}
```

#### >>394. 字符串解码

给定一个经过编码的字符串，返回它解码后的字符串。

编码规则为: `k[encoded_string]`，表示其中方括号内部的 `encoded_string` 正好重复 `k` 次。注意 `k` 保证为正整数。

你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。

此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 `k` ，例如不会出现像 `3a` 或 `2[4]` 的输入。

 

**示例 1：**

```
输入：s = "3[a]2[bc]"
输出："aaabcbc"
```

**示例 2：**

```
输入：s = "3[a2[c]]"
输出："accaccacc"
```

**示例 3：**

```
输入：s = "2[abc]3[cd]ef"
输出："abcabccdcdcdef"
```

**示例 4：**

```
输入：s = "abc3[cd]xyz"
输出："abccdcdcdxyz"
```

```c++
class Solution {
public:
    string decodeString(string s) {
        stack<string>s_stk;
        stack<int>i_stk;
        string ans;
        string temp;
        int num=0;
        for(int i=0;i<s.size();i++){
            if(s[i]>='0'&&s[i]<='9'){
                num=num*10+s[i]-'0';
            }
            else if(s[i]=='['){
                i_stk.push(num);
                num=0;
                s_stk.push(temp);
                temp.clear();
            }
            else if((s[i]>='a'&&s[i]<='z')||(s[i]>='A'&&s[i]<='Z')){
                temp+=s[i];
            }
            else if(s[i]==']'){
                int a=i_stk.top();
                for(int i=0;i<a;i++){
                    s_stk.top()+=temp;
                }
                i_stk.pop();
                temp=s_stk.top();
                s_stk.pop();
            }
        }
        return ans+temp;
    }
};
```

#### >>621. 任务调度器

给你一个用字符数组 `tasks` 表示的 CPU 需要执行的任务列表。其中每个字母表示一种不同种类的任务。任务可以以任意顺序执行，并且每个任务都可以在 1 个单位时间内执行完。在任何一个单位时间，CPU 可以完成一个任务，或者处于待命状态。

然而，两个 **相同种类** 的任务之间必须有长度为整数 `n` 的冷却时间，因此至少有连续 `n` 个单位时间内 CPU 在执行不同的任务，或者在待命状态。

你需要计算完成所有任务所需要的 **最短时间** 。

 

**示例 1：**

```
输入：tasks = ["A","A","A","B","B","B"], n = 2
输出：8
解释：A -> B -> (待命) -> A -> B -> (待命) -> A -> B
     在本示例中，两个相同类型任务之间必须间隔长度为 n = 2 的冷却时间，而执行一个任务只需要一个单位时间，所以中间出现了（待命）状态。 
```

**示例 2：**

```
输入：tasks = ["A","A","A","B","B","B"], n = 0
输出：6
解释：在这种情况下，任何大小为 6 的排列都可以满足要求，因为 n = 0
["A","A","A","B","B","B"]
["A","B","A","B","A","B"]
["B","B","B","A","A","A"]
...
诸如此类
```

**示例 3：**

```
输入：tasks = ["A","A","A","A","A","A","B","C","D","E","F","G"], n = 2
输出：16
解释：一种可能的解决方案是：
     A -> B -> C -> A -> D -> E -> A -> F -> G -> A -> (待命) -> (待命) -> A -> (待命) -> (待命) -> A
```

```c++
class Solution {
public:
   int leastInterval(vector<char>& tasks, int n) {
        int l=tasks.size();
        vector<int>hash(26);
        for(auto i:tasks){
            hash[i-'A']++;
        }
        sort(hash.begin(),hash.end(),[] (int &x,int &y){return x>y;});

        int cnt=1;
        while(cnt<hash.size()&&hash[cnt]==hash[0]){
            cnt++;
        }
        return max(l,cnt+(n+1)*(hash[0]-1));
    }

};
```

#### >>739. 每日温度

给定一个整数数组 `temperatures` ，表示每天的温度，返回一个数组 `answer` ，其中 `answer[i]` 是指对于第 `i` 天，下一个更高温度出现在几天后。如果气温在这之后都不会升高，请在该位置用 `0` 来代替。

**示例 1:**

```
输入: temperatures = [73,74,75,71,69,72,76,73]
输出: [1,1,4,2,1,1,0,0]
```

**示例 2:**

```
输入: temperatures = [30,40,50,60]
输出: [1,1,1,0]
```

**示例 3:**

```
输入: temperatures = [30,60,90]
输出: [1,1,0]
```

```c++
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& temperatures) {
        vector<int>ans(temperatures.size(),0);
        for(int i=temperatures.size()-2;i>=0;i--){
            for(int j=i+1;j<temperatures.size();j+=ans[j]){
                if(temperatures[i]<temperatures[j]){
                    ans[i]=j-i;
                    break;
                }
                else if(ans[j]==0){
                    ans[i]=0;
                    break;
                }
            }
        }  
        return ans;   
    }
};
```

#### 7. 整数反转

给你一个 32 位的有符号整数 `x` ，返回将 `x` 中的数字部分反转后的结果。

如果反转后整数超过 32 位的有符号整数的范围 `[−231, 231 − 1]` ，就返回 0。

**假设环境不允许存储 64 位整数（有符号或无符号）。**

 

**示例 1：**

```
输入：x = 123
输出：321
```

**示例 2：**

```
输入：x = -123
输出：-321
```

**示例 3：**

```
输入：x = 120
输出：21
```

**示例 4：**

```
输入：x = 0
输出：0
```

```c++
class Solution {
public:
    int reverse(int x) {
        long ans=0;
        while(x){
            ans=ans*10+x%10;
            x/=10;
        }
        return ans>INT_MAX|| ans<INT_MIN?0:ans;
    }
};
```

#### 292. Nim 游戏

你和你的朋友，两个人一起玩 [Nim 游戏](https://baike.baidu.com/item/Nim游戏/6737105)：

- 桌子上有一堆石头。
- 你们轮流进行自己的回合， **你作为先手** 。
- 每一回合，轮到的人拿掉 1 - 3 块石头。
- 拿掉最后一块石头的人就是获胜者。

假设你们每一步都是最优解。请编写一个函数，来判断你是否可以在给定石头数量为 `n` 的情况下赢得游戏。如果可以赢，返回 `true`；否则，返回 `false` 。

 

**示例 1：**

```
输入：n = 4
输出：false 
解释：以下是可能的结果:
1. 移除1颗石头。你的朋友移走了3块石头，包括最后一块。你的朋友赢了。
2. 移除2个石子。你的朋友移走2块石头，包括最后一块。你的朋友赢了。
3.你移走3颗石子。你的朋友移走了最后一块石头。你的朋友赢了。
在所有结果中，你的朋友是赢家。
```

**示例 2：**

```
输入：n = 1
输出：true
```

**示例 3：**

```
输入：n = 2
输出：true
```

```c++
class Solution {
public:
    bool canWinNim(int n) {
        if(n%4==0){
            return false;
        }
        else{
            return true;
        }
    }
};
```

#### >>89. 格雷编码

**n 位格雷码序列** 是一个由 `2n` 个整数组成的序列，其中：

- 每个整数都在范围 `[0, 2n - 1]` 内（含 `0` 和 `2n - 1`）
- 第一个整数是 `0`
- 一个整数在序列中出现 **不超过一次**
- 每对 **相邻** 整数的二进制表示 **恰好一位不同** ，且
- **第一个** 和 **最后一个** 整数的二进制表示 **恰好一位不同**

给你一个整数 `n` ，返回任一有效的 **n 位格雷码序列** 。

 

**示例 1：**

```
输入：n = 2
输出：[0,1,3,2]
解释：
[0,1,3,2] 的二进制表示是 [00,01,11,10] 。
- 00 和 01 有一位不同
- 01 和 11 有一位不同
- 11 和 10 有一位不同
- 10 和 00 有一位不同
[0,2,3,1] 也是一个有效的格雷码序列，其二进制表示是 [00,10,11,01] 。
- 00 和 10 有一位不同
- 10 和 11 有一位不同
- 11 和 01 有一位不同
- 01 和 00 有一位不同
```

**示例 2：**

```
输入：n = 1
输出：[0,1]
```

```c++
class Solution {
public:
    vector<int> grayCode(int n) {
        vector<int>ans={0};
        for(int i=0;i<n;i++){
            int num=1<<i;
            int c=ans.size();
            for(int j=c-1;j>=0;j--){
                ans.push_back(ans[j]+num);
            }
        }
        return ans;
        
    }
};
```

#### >>50. Pow(x, n)（缺少快速幂的方法)

实现 [pow(*x*, *n*)](https://www.cplusplus.com/reference/valarray/pow/) ，即计算 `x` 的整数 `n` 次幂函数（即，`xn` ）。

 

**示例 1：**

```
输入：x = 2.00000, n = 10
输出：1024.00000
```

**示例 2：**

```
输入：x = 2.10000, n = 3
输出：9.26100
```

**示例 3：**

```
输入：x = 2.00000, n = -2
输出：0.25000
解释：2-2 = 1/22 = 1/4 = 0.25
```

```c++
class Solution {
public:
    double func(double x,long n){
        if(n==0){
            return 1;
        }
        if(n==1){
            return x;
        }
        double a=func(x,n/2);
        if(n%2==0){
            return a*a;
        }
        return a*a*x;
    }
    double myPow(double x, int n) {
        long m=abs((long) n);
        double num=func(x,m);
        if(n<0){
            return 1/num;
        }
        return num;
    }
};
```

