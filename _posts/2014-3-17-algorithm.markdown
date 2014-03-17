---
layout: post
title:  "Algorithm: Climbing Stairs"
date:   2014-3-17 23:30:00
categories: algorithm
---

Problem: You are climbing a stair case. It takes n steps to reach to the top. Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Solution:

- n stair, the ways to reach n have two cases: 1) n-1 step to stair n-1 + 1 step  2) n-2 step to stair n-2 + 2 steps, thus

f(n) = f(n-1)+f(n-2)

- Using recursive programming, Time Complexity around O(2^n), Space Complexity O(n) stack space

{% highlight ruby %}
int climbStair(int n) {
	if(n == 1) return 1;
	if(n == 2) return 2;
	return climbStair(n-1) + climbStair(n-2);
}
{% endhighlight %}

- Optimization 1: Using Tail Recursion, Time Complexity O(n), Space Complexity O(1)

{% highlight ruby %}
int climbStair(int n, int acc1, int acc2) {
	if(n == 1) return acc1;
	return climbStair(n-1, acc2, acc1+acc2);
}
{% endhighlight %}

- Optimization 2: Using Dynamic Programming, Iterative, Time Complexity O(n), Space Complexity O(n)

{% highlight ruby %}
int climbStair(int n) {
	int[] result = new int[n];
	result[0] = 1;
	result[1] = 1;
    for(int i = 2; i<n;i++){
    	result[i] = result[i-1] + result[i-2]
	}
	return result[n-1];
}
{% endhighlight %}

- Optimization 3: Further Optimize on 2 -- Time Complexity O(n), Space Complexity O(1)

{% highlight ruby %}
int climbStair(int n) {
	int[] result = new int[n];
	result[0] = 1;
	result[1] = 1;
    for(int i = 2; i<n;i++){
    	result[i%3] = result[(i-1)%3] + result[(i-2)%3]
	}
	return result[(n-1)%3];
}
{% endhighlight %}