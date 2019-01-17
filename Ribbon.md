#Ribbon的介绍#
##Ribbon的功能主要下面几个方面##
- <h3>服务发现</h3> *发现各个服务的每个实例*

--------------
- <h3>服务选择规则</h3> *负载均衡的方式*

----------

- <h3>服务监听</h3> *检测失效的服务 做到高效剔除*

----------
**robbon的主要组件**</br>
*ServerList 对应获取实例*</br>
*IRule 对应负载均衡规则*<br/>
*ServerListFilter 对应服务监听*<br/>
-------------------------------
更改Ribbon的轮询规则:


       ORDERAPP:
  		  ribbon:
    	    NFLoadBalancerRuleClassName: com.netflix.loadbalancer.RandomRule