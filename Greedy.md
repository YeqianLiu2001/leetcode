## 最大子序列和
局部最优：当前连续和为负数时立即放弃，从下一个元素重新开始  
全局最优：选取连续最大的‘连续和’  
 public int maxSubArray(int[] nums) {   
        int sum =0;  
        int res = Integer.MIN_VALUE;//这里不是0 是负数  
        for(int i=0;i<nums.length;i++){  
            sum += nums[i];  
          *** res = Math.max(res,sum);//取最大的    
            if(sum>0){  
                continue;  
            }  
            else{  
                sum = 0;
            }
        }  
        return res;  
          
          
  ## 买卖股票最佳时期
  数组的第i个元素是一只股票第i天的价格，通过多次买卖一只股票获得利益（买完卖完才能再买）  
  最终利润是可以分解的。局部最优  
  第0天买，第三天卖出 profit = (p[3]-p[2])+(p[2]-p[1])+(p[1]-p[0]) = p[3]-p[0]  
  所以！这个数组为profit = price[i+1]-price[i];  
  相当于每天都可买入第二天卖出没有漏算的。利润分解为每天为单位的，只要以买入那天为0，算出每天的正负即可。  
  因为要盈利所以只需要把正数加起来即可，算的是全部利润之和不是只能买卖一次取最大子序列和。  
  
  ## 跳跃游戏
  数组的每个元素代表在该位置最大可以跳的length。跳跃范围能不能覆盖到终点  
  有点像non-overloop区间  
  ![image](https://user-images.githubusercontent.com/113034973/219900374-6a6c40a0-4e03-4eeb-a173-9fa538d783bc.png)  
   重点是每次在max = Math.max(max,coverRange)之前要判断i<=max，才能保证这个点能被之前最大的Range cover住。  
        int max = 0;  
        int l = 0;  
        for(int i=0;i<nums.length;i++){  
            l = i +nums[i];  
            if(i<=max){  
            max = Math.max(max,l);  
        }
        else{
            return false;  
        }  
        }  
        return true;
     
   ## 跳跃游戏2
   使用最少跳跃次数到达数组的最后一个位置（假设一定能跳到）  
   局部最优：尽可能多走  
   需要统计两个范围，当前这一步最大覆盖和下一步最大覆盖。**以最小的步数增加最大的覆盖范围，直到覆盖终点。**  
      int cur = 0;  
        int next = 0;//下一步覆盖的  
        int count = 0;  
        for(int i = 0;i<nums.length-1;i++){  
            next = Math.max(next,nums[i]+i); **这里很重要，这里的i是连续不间断地实现了遍历）**  
            if( i == cur ){  
                cur = next;  
                count++;//  
            }      
        }  
        ![image](https://user-images.githubusercontent.com/113034973/220166920-eb83c5a5-4f2e-4560-b6d8-6856e35276ad.png)


   

  ## k次取反后最大化的数组和，将A[i]替换为-A[i]从而使和最大，重复k次
  局部最优：让绝对值大的负数变为正数，当前数值达到最大。从而达到整体最优  
  当负数都变为正数后，k若还大于0，使绝对值最小的正数反转。  
  解题步骤：  
  1.绝对值从大到小排序。  
  2.从前向后遍历，若遇到负数，k--  
  3.若k>0,反转**最小的数**(只用反转最小的正负正负这样循环就行）直到k=0 
  
  ## 加油站。
环行路N个加油站，第i个加油站有gas[i]升汽油，油箱无限容量的汽车从第i个加油站开往第i+1个需要消耗cost[i]升汽油。从其中一个加油站出发，如果可以绕行一周，则返回出发时加油站编号。  
暴力解法：是一个环形问题，要取余数。for适合模拟从头到尾，while适合模拟环形遍历。  
局部最优：每个加油站剩余量rest[i]=gas[i]-cost[i]，如果curSum<0，说明[0,i]区间都不能作为起始位置。所以从i+1作为起始位置算起.**这时清空了curSum重新从0开始**  
![image](https://user-images.githubusercontent.com/113034973/220179026-3460cc3d-5251-4bf1-9da9-8ad2a27e66a8.png)  
```java
 public int canCompleteCircuit(int[] gas, int[] cost) {
        int count =0;
        int curSum =0;
        int totalSum = 0;
       for(int i=0;i<gas.length;i++){
           curSum += gas[i] - cost[i];
           totalSum +=gas[i] - cost[i];
           if(curSum<0){
               count = i+1;
               curSum=0;//从0开始
           }
       }
           if(totalSum<0){//如果总gas<cost 说明不能返回
               return -1;
           }
       return count;
    }
```
  
  ## 分发糖果
  
  
