# 🍜 黑马点评 (HeiMa DianPing)

基于 Spring Boot 构建的生活服务点评平台，实现商户浏览、用户互动、优惠券秒杀等核心功能。

## 🛠 技术栈

- **后端框架**：Spring Boot 2.3.12
- **ORM**：MyBatis-Plus 3.4.3
- **数据库**：MySQL 5.7 + Redis
- **分布式锁**：Redisson 3.13.6 + 自定义 Redis 锁
- **工具库**：Hutool 5.7.17、Lombok
- **构建工具**：Maven
- **语言**：Java 8

## ✨ 核心功能

| 模块 | 功能 | 技术亮点 |
|------|------|----------|
| 🏪 商户管理 | 商户列表、详情查询、分类筛选 | Redis 缓存 + 缓存穿透防护 |
| 👤 用户系统 | 注册登录、个人信息、Token 刷新 | Session 共享 + 登录拦截器 |
| 📝 笔记动态 | 发布笔记、评论互动、点赞 | 滚动分页查询 |
| 🔔 关注取关 | 关注用户、共同关注 | Redis Set 交集运算 |
| 🎫 优惠券秒杀 | 秒杀下单、库存扣减、一人一单 | Lua 脚本 + 分布式锁 + Redisson |

## 🚀 快速开始

### 环境要求

- JDK 8+
- Maven 3.6+
- MySQL 5.7+
- Redis 6.0+

### 1. 初始化数据库

执行 `hm-dianping/src/main/resources/db/hmdp.sql` 导入表结构和初始数据。

### 2. 修改配置

编辑 `hm-dianping/src/main/resources/application.yaml`，修改数据库和 Redis 连接信息：

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/hmdp?useSSL=false&serverTimezone=Asia/Shanghai
    username: root
    password: your_password
  redis:
    host: localhost
    port: 6379
```

### 3. 启动项目

```bash
cd hm-dianping
mvn spring-boot:run
```

启动后访问 `http://localhost:8080`。

## 📁 项目结构

```
hm-dianping/
├── src/main/java/com/hmdp/
│   ├── config/          # 配置类（MVC、MyBatis、Redisson）
│   ├── controller/      # 控制器层
│   ├── dto/             # 数据传输对象
│   ├── entity/          # 实体类
│   ├── mapper/          # MyBatis 映射接口
│   ├── service/         # 服务接口与实现
│   └── utils/           # 工具类（缓存、锁、拦截器）
├── src/main/resources/
│   ├── application.yaml # 应用配置
│   ├── db/hmdp.sql      # 数据库初始化脚本
│   ├── seckill.lua      # 秒杀 Lua 脚本
│   └── unlock.lua       # 分布式锁释放脚本
└── pom.xml
```

## 📄 License

本项目仅供学习交流使用。
