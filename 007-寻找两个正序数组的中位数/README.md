# 题目

leetcode ： [寻找两个正序数组的中位数](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/)

## 解法一 类似于归并排序
时间复杂度 O(n+m)
```Java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int i=0;
        int j=0;
        int[] que = new int[2];
        int n = nums1.length;
        int m = nums2.length;
        int cnt = (m+n)/2+1;

        while(i<nums1.length&&j<nums2.length&&cnt!=0){
            if(nums1[i]<=nums2[j]){
                que[0] = que[1];
                que[1] = nums1[i];
                cnt--;
                i++;
            }
            else{
                que[0] = que[1];
                que[1] = nums2[j];
                cnt--;
                j++;
            }
        }
        while(i<nums1.length&&cnt!=0){
            que[0] = que[1];
            que[1] = nums1[i];
            cnt--;
            i++;  
        }
        while(j<nums2.length&&cnt!=0){
            que[0] = que[1];
            que[1] = nums2[j];
            cnt--;
            j++;            
        }

        return (m+n)%2==0 ? (que[0]+que[1]+0.0)/2 : que[1];
    }
}
```
## 解法二 二分思想
二分：用什么标准来进行二分，排除那一半？

```Java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int n = nums1.length;
        int m = nums2.length;

        if((n+m)%2==0){
            int a = findN(nums1, nums2, 0, 0, (n+m)/2);
            int b = findN(nums1, nums2, 0, 0, (n+m)/2+1);     
            return (a+b+0.0)/2;       
        }
        else{
            return findN(nums1, nums2, 0, 0, (n+m)/2+1);
        } 
    }
    public int findN(int[] nums1, int[] nums2, int i, int j, int N){
        if(i>=nums1.length){
            return nums2[j+N-1];
        }
        if(j>=nums2.length){
            return nums1[i+N-1];
        }
        if(N==1){
            return Math.min(nums1[i], nums2[j]);
        }
        
        int mid1 = Math.min(i+N/2-1, nums1.length-1);
        int mid2 = Math.min(j+N/2-1, nums2.length-1);

        if(nums1[mid1]>=nums2[mid2]){
            return findN(nums1, nums2, i, mid2+1, N-(mid2-j+1));
        }
        else{
            return  findN(nums1, nums2, mid1+1, j, N-(mid1-i+1));
        }
        
    }
}
```
