# 开始
## 创建项目
通过micro new创建五个文件夹，微服务。  
改过程需要用到protoc，micro，consul
1. web端相当于中间者，接收vue前端数据，发送给后端srv
2. vue_gin用于前端，发送数据至web端
3. srv是服务端，接收web端获取的参数，返回给vue前端

## rpc升级为grpc
1. github.com/micro/go-grpc  
2. service :grpc.NewService()  


## 整合gin框架
1. router:=gin.Default()  
2. web.Handle(router)

## 项目结构调整
1. web项目下：controller(product,seckill,user)|handler|html|router(router)|static


# 注册 181
## 模型
zhiliao_user_srv\zhiliao_user_srv\models\front_user.go  
## 连接数据库
zhiliao_user_srv\zhiliao_user_srv\data_source\mysql_conn.go
## 前端用户注册
zhiliao_vue_gin\zhiliao_vue_gin\src\views\front\Register.vue  
1. 邮箱
2. 验证码
## web端用户注册
zhiliao_user_srv\zhiliao_user_srv\controller\front_user.go  
##  服务端用户注册
zhiliao_web\zhiliao_web\controller\user\front_user.go  
1. MD5 zhiliao_user_srv\zhiliao_user_srv\utils\get_md5_data.go


# 登陆 196
JWT：JSON Web Token：是一种跨域认证解决方案，规定了一种Token实现方式，用于前后端分离等场景。
我isnhoufusn

## token认证
web端认证：zhiliao_web\zhiliao_web\utils\jwt_token.go

## 用户前端登录
zhiliao_vue_gin\zhiliao_vue_gin\src\views\front\Login.vue    
zhiliao_web\zhiliao_web\controller\user\front_user.go  
zhiliao_user_srv\zhiliao_user_srv\controller\front_user.go
  
## 用户状态管理
zhiliao_vue_gin\zhiliao_vue_gin\src\auth\auth.js

## 登出
zhiliao_vue_gin\zhiliao_vue_gin\src\views\front\GoodsList.vue  

## 导航守卫
拦截器  
未登录时点击加购物车跳转至登录  
zhiliao_vue_gin\zhiliao_vue_gin\src\router.js  
添加判断  

# 管理员 209
##  管理员登录
zhiliao_vue_gin\zhiliao_vue_gin\src\views\cms\user\Login.vue  

## 管理员web
zhiliao_web\zhiliao_web\controller\user\admin_user.go

## 管理员srv
zhiliao_user_srv\zhiliao_user_srv\proto\admin_user\admin_user.micro.go  
zhiliao_user_srv\zhiliao_user_srv\controller\admin_user.go  


# 用户列表 213
## 前端用户列表
zhiliao_vue_gin\zhiliao_vue_gin\src\views\cms\user\UserList.vue  

## 用户列表接口
zhiliao_web\zhiliao_web\controller\user\front_user.go  

## 服务端
zhiliao_user_srv\zhiliao_user_srv\controller\front_user.go

## 分页
1. 前端，pagination，UserList
2. 后端，FrontUserList

# 管理端token认证中间件 220
zhiliao_web\zhiliao_web\middle_ware\jwt_token.go

# 商品管理列表 221

## 前端
1. 商品：zhiliao_vue_gin\zhiliao_vue_gin\src\views\cms\product\ProductList.vue  
2. 秒杀活动：zhiliao_vue_gin\zhiliao_vue_gin\src\views\cms\seckill\SeckillList.vue

## web端
1. 商品：zhiliao_web\zhiliao_web\controller\product\product_manage.go
2. 秒杀活动：zhiliao_web\zhiliao_web\controller\seckill\seckill_manage.go
## 后端商品
1. 表：zhiliao_product_srv\zhiliao_product_srv\models\product.go
2. zhiliao_product_srv\zhiliao_product_srv\controller\product.go
## 后端秒杀活动
1. 表：zhiliao_product_srv\zhiliao_product_srv\models\seckill.go
2. zhiliao_product_srv\zhiliao_product_srv\controller\seckill.go

## 商品添加编辑前端
zhiliao_vue_gin\zhiliao_vue_gin\src\views\cms\product\ProductAdd.vue  
zhiliao_vue_gin\zhiliao_vue_gin\src\views\cms\product\ProductEdit.vue
## 商品编辑web端
zhiliao_web\zhiliao_web\controller\product\product_manage.go  


# 活动设计 236
## 模型设计
zhiliao_seckill_srv\zhiliao_seckill_srv\models\seckill.go

## 活动前端
zhiliao_vue_gin\zhiliao_vue_gin\src\views\cms\seckill\SeckillList.vue  
zhiliao_vue_gin\zhiliao_vue_gin\src\views\cms\seckill\SeckillEdit.vue  
zhiliao_vue_gin\zhiliao_vue_gin\src\views\cms\seckill\SeckillAdd.vue  


## web端活动管理
zhiliao_web\zhiliao_web\controller\seckill\seckill_manage.go



# 活动前端 252
## 商品展示
zhiliao_vue_gin\zhiliao_vue_gin\src\views\front\GoodsList.vue
## 商品细节
zhiliao_vue_gin\zhiliao_vue_gin\src\views\front\GoodsDetail.vue





# 秒杀服务 260
## 定义
zhiliao_seckill_srv\zhiliao_seckill_srv\controller\seckill.go


# jmeter压力测试 266




# 升级一 rabbitMQ 274
## 方法
zhiliao_web\zhiliao_web\rabbitmq\mq.go  
## 使用
web端将数据送入MQ，服务端从MQ获取数据。  
1. 将下单任务放入MQ。  
zhiliao_web\zhiliao_web\controller\seckill\seckill.go|SecKill
2. 服务端从MQ消费任务
zhiliao_seckill_srv\zhiliao_seckill_srv\controller\seckill.go|Orderapply
## 测试
zhiliao_web\zhiliao_web\test\test_mq.go  


# 升级二 Redis 287
## init
zhiliao_seckill_srv\zhiliao_seckill_srv\redis_lib\redis_init.go
## use 
1. 将消费结果放入redis
zhiliao_seckill_srv\zhiliao_seckill_srv\controller\seckill.go|redis_lib.Conn.Do("SET", front_user_email, utils.MapToStr(map_data))
2. 消费结果写回前端
methods:{
    async getResult(){

## 测试
zhiliao_seckill_srv\zhiliao_seckill_srv\test\test_redis.go





