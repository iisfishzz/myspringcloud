#Feign介绍#
<font style="color:#1AFD9C">feign是生命式REST客户端(伪RPC)</font><br/>
<font style="color:#BE77FF">采用了基于接口的注解</font><br/>
<h3>具体的使用步骤</h3>
1. 引入依赖 <br/>

		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-feign</artifactId>
			<version>1.4.6.RELEASE</version>
		</dependency>

2. 在启动类上添加`@EnableFeignClients`标签启动Feign
3. 创建一个类映射被访问端的端口代码如下:<br/>

		@FeignClient(value="product",path="product")
		public interface ProductClient {
		    @GetMapping("msg")
		    String msg();
		}

<text style="color:red">注意:`@FeignClient` 中的**value**对应的是被访问应用的名称 **path**对应的是项目的路径,如果没有可以不填. **msg** 是客户端对应的接口名 <br/></text>
4. 将上面创建好的类交给`Spring`管理.,在实现类中直接调用`msg`方法即可 代码只有一句: <br/>
`String response = productClient.msg();`
