python 一个从数字返回列表的示例：
```
number = 12345
digits = [int(d) for d in str(number)]
print(digits)  # Output: [1, 2, 3, 4, 5]
```

#189. 轮转数组
```
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n=len(nums)
        k%=n
        self.rotate_List(nums,0,n-1)
        self.rotate_List(nums,0,k-1)
        self.rotate_List(nums,k,n-1)
    def rotate_List(self,digits: List[int],begin:int,end:int)->None:
        while begin<end:
            digits[begin] ,digits[end] = digits[end] ,digits[begin]# 解构（unpacking）赋值
            begin+=1
            end-=1
```
#66. 加一
```
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        n=len(digits)
        total=1
        for i in range(n):
            total+=digits[i]*10**(n-i-1)
        return [int(d) for d in str(total)] 
```   
```
# 模拟加法 处理进位条件
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        n=len(digits)
        add=0
        digits[n-1]+=1
        for i in range(n-1,-1,-1):
            digits[i]+=add
            add=digits[i]//10
            digits[i]=digits[i]%10
            if add==0:return digits
        digits=[0]*(n+1)
        digits[0]=1
        return digits
```
#724. 寻找数组的中心下标
```
class Solution:
    def pivotIndex(self, nums: List[int]) -> int:
        n = len(nums)
        total = sum(nums)  # 计算数组的总和
        left_sum = 0  # 左侧元素之和
        for i in range(n):
            if left_sum == (total - left_sum - nums[i]):
                return i
            left_sum += nums[i]  # 更新左侧元素之和
        return -1  # 没有找到中心索引，返回 -1
```
#485. 最大连续 1 的个数
```
#容易忽略边界 遍历到最后一个的时候再加一个判断
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        n=len(nums)
        total=0 
        total_temp=0
        for i in range(n):
            total+=nums[i]
            if nums[i]==0:
                if total>total_temp:
                    total_temp=total 
                total=0
            if i==n-1:
                if total>total_temp:
                    total_temp=total
        return total_temp
```
```
#稍微优化过
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        n=len(nums)
        total=0 
        total_temp=0
        for i in range(n):
            total+=nums[i]
            if nums[i]==0:
                if total>total_temp:
                    total_temp=total 
                total=0
        return max(total_temp,total)
```
#238. 除自身以外数组的乘积
```
#第一想法 超时
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        n=len(nums)
        answer=[0]*n
        for i in range(n):
            answer[i]=self.cheng(0,i,nums)*self.cheng(i+1,n,nums)
        return answer
    def cheng(self,begin: int,end: int,nums:List[int])->int:
        total=1
        for i in range(begin,end):
            total*=nums[i]
        return total
```
```
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        n=len(nums)
        answer=[0]*n

        #计算左侧乘积
        left=[1]*n
        for i in range(1,n):# 从1开始遍历 因为第一个元素左侧默认设为1
            left[i]=left[i-1]*nums[i-1]
        right=1
        #从后向前遍历 直接计算总值
        for i in range(n-1,-1,-1):
            answer[i]=right*left[i]
            right*=nums[i]
        return answer
```
#498. 对角线遍历
```
class Solution:
    def findDiagonalOrder(self, mat: List[List[int]]) -> List[int]:
        m=len(mat)
        n=len(mat[0])
        a=[]
        for diagonal in range(m+n-1):#对角线之和在0到m+n-2的范围中
            if diagonal%2==0:
                row=min(diagonal,m-1)
                col=diagonal-row
                while row>=0 and col<n:
                    a.append(mat[row][col])
                    row-=1#行减列加 正向遍历
                    col+=1
            else:
                col=min(diagonal,n-1)
                row=diagonal-col
                while col>=0 and row<m:
                    a.append(mat[row][col])
                    col-=1# 反向遍历
                    row+=1
        return a
```
#旋转图像
```
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        n=len(matrix)
        for i in range(n):
            for j in range(i,n):
                matrix[i][j],matrix[j][i]=matrix[j][i],matrix[i][j]
        for i in range(n):
            matrix[i].reverse()
```