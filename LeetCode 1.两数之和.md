# LeetCode	1.两数之和

## 方法1.二重循环


```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for(int i = 0; i < nums.length; i++){
            for(int k = i + 1; k < nums.length; k++){
                if(nums[i] + nums[k] == target){
                   return new int[]{i,k};
                }
            }
        }
        return null;
    }
}
```

细节：第二层for循环应从”k = i + 1“开始，第一次错误是写成”k = 0“，第二层错误写成”k = i“

收获：返回一个新的数组时，可以写”return new int[]{}“花括号内写输出的下标

## 方法2.HashMap

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer,Integer> hash = new HashMap<>();
        for(int i = 0; i < nums.length; i++){
            if(!hash.containsKey(nums[i])){
                hash.put(target - nums[i],i);
            }else{
                return new int[]{hash.get(nums[i]),i};
            }
        }
        return null;
    }
}
```

HashMap<key,value>的使用可以降低时间复杂度。

思路：先判断哈希表内有没有已经存入的nums[i]值。如果没有，那就将target - nums[i]作为key，i（下标）作为values存入哈希表。当nums[i]和哈希表的key有相同时，那么表示匹配成功。

例如：nums = [3,2,4], target = 6

​			输出：[1,2]

判断哈希表内key有没有3，没有则6 - 3 = 3	存入哈希表<3,0>

判断哈希表内key有没有2，没有则6 - 2 = 4	存入哈希表<4,1>

判断哈希表内key有没有4，有则输出[1,2]

### HashMap常用的方法：

put(key，value)

containsKey()检验出map集合中有没有包含Key为key的元素，如果有则返回true，否则返回false。

containsValue() 检验出map集合中有没有包含Value为value的元素，如果有则返回true，否则返回false。

get()通过key来获取value