# gin+vue+微服务秒杀商城

## 前端后端
1. 前端技术：vue3，ant-design-vue,vue-router,axios 
2. 后端技术：gin框架，gorm，微服务（集群部署）web,srv

## 介绍
![jiashao](note/jieshao.png) 

## 难点
1. 代码和部署完全隔离（微服务）
2. 怎么避免雪崩（微服务）
3. 根据后端承载能力，进行限流和过载保护（限流熔断）
4. 使用redis承载海量QPS（redis队列）
5. mysql性能瓶颈（sql优化，拆库，拆表）
6. 可扩展性（机器的扩展等）
7. 长连接（先不管）


## 分类
1. 前端：my_vue_gin
vue create my_vue_gin
2. micro-web:my_web
micro new my_web --type="web" --namespace="my.web"
3. 用户管理服务:my_user_srv   
micro new my_user_srv --type="srv" --namespace="my.user"
4. 商品和活动管理服务 my_product_srv  
micro new my_product_srv --type="srv" --namespace="my.product"
5. 秒杀服务:my_seckill_srv
micro new my_seckill_srv --type="srv" --namespace="my.seckill"


