<h1>Eureka客户端之间通信的三种方式
![图片](http://thyrsi.com/t6/652/1546913774x1822611383.jpg)
<h5><code>public void static main(String args[]){</br>
Sysytem.out.prinln("Hello World! ");}</code></h5>
**方式一** > *直接使用RestTemplate对象 url手写*


     RestTemplate template = new RestTemplate();
        String response = template.getForObject("http://localhost:8081/product/msg", String.class);
        System.out.println("方式一接收到的返回结果:" + response);

----------
**上面的方式通信的url要手写,可能会不知道对方客户的具体地址,或者对方有多个ip无法区分**</br>

----------
**方式二**> *使用LoadBalancerClient获取URL*

     	//提前注入LoadBalancerClient对象
		@Autowired
		private LoadBalancerClient loadBalanceClient;
		//输入服务的ID得到服务实例
        ServiceInstance instance = loadBalancerClient.choose("APPNAME");
        //通过实例获取访问地址
        String url = String.format("http://%s:%s" ,instance.getHost(),instance.getPort()) + "/msg";
        RestTemplate template = new RestTemplate();
        String response = template.getForObject(url, String.class);
        System.out.println("方式二接收到的返回结果:" + response);

----------
**方式三**> *使用配置的方式获取URL*
	
	使用配置的方式将RestTemplate导入
    @Component
	public class RestTemplateConfig {
	    @Bean
	    @LoadBalanced
	    public RestTemplate restTemplate(){
	        return new RestTemplate();
	    }
	}

	//在使用restTemplate时可直接使用下面方式访问(APPNAME 是应用ID)
	String response = restTemplate.getForObject("http://APPNAME/msg", String.class);
        System.out.println("方式三接收到的返回结果:" + response);
