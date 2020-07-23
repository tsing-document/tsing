# 1.两数之和
- 题目：
    - 给定一个整数数组 `nums` 和一个目标值 `target`,请在该数组中找到和为目标值的两个整数，并返回数组的下标。
- 示例：
    ```md
        给定 nums = [2, 7, 11, 15], target = 9

        因为 nums[0] + nums[1] = 2 + 7 = 9
        所以返回 [0, 1]
    ```
- 解决方案：
    - 方案1:
        ```java
            public class TowSum {

                public static int[] towSum (int[] nums, int target) {
                    for (int i = 0; i < nums.length; i++) {
                        for (int j = i + 1; j < nums.length; j++) {
                            if (nums[i]+nums[j] == target) {
                                return new int[] {i,j};
                            }
                        }
                    }
                    return null;
                }
                
                public static void main(String[] args) {
                    int[] nums = {1, 3, 10};
                    int[] result = TowSum.towSum(nums, 13);
                    for (int i = 0; i < result.length; i++) {
                        System.err.println(result[i]);
                    }
                }
            }

        ```