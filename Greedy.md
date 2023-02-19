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
   

  ## k次取反后最大化的数组和
  
  
  
