# 卡了电竞 - Java + MySQL 完整项目

## 项目简介

这是一个基于 Spring Boot + MySQL 的完整电竞陪玩平台项目，包含用户注册、登录、充值等功能。

## 技术栈

- **后端**: Spring Boot 3.2.0, Spring Data JPA, MySQL
- **前端**: HTML, CSS, JavaScript
- **数据库**: MySQL 8.0+

## 项目结构

```
src/
├── main/
│   ├── java/
│   │   └── org/example/
│   │       ├── Main.java                    # Spring Boot 主类
│   │       ├── config/                      # 配置类
│   │       ├── controller/                  # REST API 控制器
│   │       ├── dto/                         # 数据传输对象
│   │       ├── entity/                      # 实体类
│   │       ├── repository/                  # 数据访问层
│   │       └── service/                     # 业务逻辑层
│   ├── resources/
│   │   ├── application.properties           # 应用配置
│   │   ├── application.yml                  # YAML 配置
│   │   └── db/
│   │       └── schema.sql                   # 数据库初始化脚本
│   └── html/
│       └── t1/                              # 前端页面
│           ├── index.html                   # 首页
│           ├── login.html                   # 登录页
│           ├── register.html                # 注册页
│           ├── recharge.html                # 充值页
│           └── projects/                    # 游戏详情页
└── pom.xml                                  # Maven 配置
```

## 功能特性

### 1. 用户管理
- ✅ 用户注册（用户名、密码、邮箱、手机号）
- ✅ 用户登录
- ✅ 用户信息查询
- ✅ 余额管理

### 2. 充值功能
- ✅ 创建充值订单
- ✅ 选择支付方式（支付宝、微信、银行卡）
- ✅ 充值记录查询
- ✅ 充值确认（模拟支付成功）

### 3. 前端页面
- ✅ 赛博朋克风格设计
- ✅ 响应式布局
- ✅ 用户登录状态显示
- ✅ 余额实时显示

## 快速开始

### 1. 环境要求

- JDK 21+
- Maven 3.6+
- MySQL 8.0+
- IDE (IntelliJ IDEA / Eclipse)

### 2. 数据库配置

#### 2.1 创建数据库

执行 `src/main/resources/db/schema.sql` 脚本创建数据库和表：

```sql
CREATE DATABASE IF NOT EXISTS kale_esports CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE kale_esports;
-- ... 表结构会自动创建
```

#### 2.2 修改数据库连接

编辑 `src/main/resources/application.properties` 或 `application.yml`：

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/kale_esports?useUnicode=true&characterEncoding=utf8&useSSL=false&serverTimezone=Asia/Shanghai
spring.datasource.username=root
spring.datasource.password=你的密码
```

### 3. 运行项目

#### 方式一：使用 Maven

```bash
# 编译项目
mvn clean compile

# 运行项目
mvn spring-boot:run
```

#### 方式二：使用 IDE

1. 导入项目到 IDE
2. 等待 Maven 依赖下载完成
3. 运行 `Main.java` 的 `main` 方法

### 4. 访问项目

- 前端页面: http://localhost:8080/t1/index.html
- API 文档: http://localhost:8080/api/user/login (POST)

## API 接口

### 用户相关

#### 1. 用户注册
```
POST /api/user/register
Content-Type: application/json

{
  "username": "testuser",
  "password": "123456",
  "email": "test@example.com",
  "phone": "13800138000"
}
```

#### 2. 用户登录
```
POST /api/user/login
Content-Type: application/json

{
  "username": "testuser",
  "password": "123456"
}
```

#### 3. 查询用户信息
```
GET /api/user/info/{userId}
```

### 充值相关

#### 1. 创建充值订单
```
POST /api/recharge/create?userId={userId}
Content-Type: application/json

{
  "amount": 100.00,
  "paymentMethod": "ALIPAY"
}
```

#### 2. 确认充值（模拟支付成功）
```
POST /api/recharge/confirm/{rechargeId}
```

#### 3. 查询充值记录
```
GET /api/recharge/list/{userId}
```

#### 4. 查询充值详情
```
GET /api/recharge/{rechargeId}
```

## 数据库表结构

### users 表
- `id`: 主键
- `username`: 用户名（唯一）
- `password`: 密码
- `email`: 邮箱（唯一）
- `phone`: 手机号
- `balance`: 余额
- `created_at`: 创建时间
- `updated_at`: 更新时间

### recharges 表
- `id`: 主键
- `user_id`: 用户ID（外键）
- `amount`: 充值金额
- `status`: 状态（PENDING/SUCCESS/FAILED）
- `payment_method`: 支付方式
- `transaction_id`: 交易ID
- `created_at`: 创建时间
- `updated_at`: 更新时间

## 注意事项

1. **密码安全**: 当前版本密码为明文存储，生产环境请使用 BCrypt 等加密方式
2. **跨域配置**: 已配置允许所有来源，生产环境请限制具体域名
3. **支付集成**: 当前为模拟支付，实际项目需要集成第三方支付 SDK
4. **会话管理**: 当前使用 localStorage 存储用户信息，建议使用 JWT Token

## 开发计划

- [ ] 密码加密（BCrypt）
- [ ] JWT Token 认证
- [ ] 订单管理
- [ ] 陪玩服务下单
- [ ] 管理员后台
- [ ] 支付接口集成

## 许可证

MIT License

## 联系方式

如有问题，请联系开发团队。

