---
layout: post
title: house robber DP解法
categories: algorithm
description: one algorithm a day
keywords: keyword1, keyword2
---

## LeetCode house robber 
### 问题描述

> You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

> Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

### 问题分析
我们先将这个问题抽象，可以理解为**"给定一个非负的数组，找出不相邻数的最大和"** 

这个问题可以用dp问题进行解决，就相当于我们从一串数字中选取数字，按照数组下标依次往后取值，每到一个下标都会有一个选择，1.取出来加到之前的结果中（这时需要上一个决定是不取，因为不能相邻），2.不取，仍保留当前的结果（这时候上一个状态就是取了）根据此判断我们可以得出状态转移方程
设定robber[nums.length+1][2],robber[n][0]表示在n-1下标处不选，而robber[n][1]就是选择。

	robber[k][0]=max(robber[k-1][1],robber[k-1][0]);
	robber[k][1]=nums[k-1]+robber[k-1][0];

可以书写程序

    import java.lang.Math;
    class Solution {
        public int rob(int[] nums) {
            if(nums.length==0){
                return 0;
            }
            int[][] robber = new int[nums.length+1][2];
            for(int i=1;i<=nums.length;i++){
            	robber[i][0]=Math.max(robber[i-1][0],robber[i-1][1]);
            	robber[i][1]=nums[i-1]+robber[i-1][0];
            }
            return Math.max(robber[nums.length][0],robber[nums.length][1]);
        }
    }
    
**自顶向下的递归防范解决**

每一步都是上一步结果的叠加.时间较长

    import java.lang.Math;
    class Solution {

        public int rob(int[] nums) {
            return recuRobber(nums,nums.length);
        }

        public int recuRobber(int[] nums ,int num){
            if (num==0) {
                return 0;
            }
            if (num==1) {
                return nums[0];
            }
            if (num==2) {
                return Math.max(nums[0],nums[1]);
            }
            int robberNo=recuRobber(nums,num-1);
            int robberYes=recuRobber(nums,num-2)+nums[num-1];
            return Math.max(robberYes,robberNo);
        }
    }