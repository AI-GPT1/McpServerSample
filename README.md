# McpServerSample

## 项目介绍

McpServerSample 是一个基于 Spring Boot 和 Spring AI 的 Model Context Protocol (MCP) 服务器示例项目。
该项目主要提供天气服务功能，通过集成官方天气 API (weather.gov) 实现了以下核心功能：

- 根据经纬度获取指定位置的天气预报信息
- 根据美国州代码获取特定地区的天气警报信息
- 利用 Spring AI 提供的工具注册机制，使这些天气服务可以作为 AI 模型调用的工具

## 项目结构

```
McpServerSample/
├── src/
│   └── main/
│       ├── java/
│       │   └── com/ai/mcpserver/
│       │       ├── McpServerApplication.java   # 应用程序入口类
│       │       └── WeatherService.java         # 天气服务实现类
│       └── resources/
├── target/
│   ├── classes/
│   │   ├── application.properties             # 应用配置文件
│   │   └── com/
├── pom.xml                                     # Maven 项目配置文件
└── README.md                                   # 项目说明文档
```

## 技术栈

- **Spring Boot 3.4.4** - 应用程序框架
- **Spring AI 1.0.0-M7** - AI 功能支持
- **Spring AI MCP Server** - Model Context Protocol 服务器实现
- **Spring Web/Spring WebFlux** - Web 服务支持
- **Jackson** - JSON 处理
- **RestClient** - HTTP 客户端
- **Maven** - 项目构建管理

## 功能特性

### 天气服务接口

项目提供以下天气相关的服务接口：

1. **getWeatherForecastByLocation**
   - 功能：获取特定纬度/经度的天气预报
   - 参数：
     - latitude: 纬度
     - longitude: 经度
   - 返回：指定位置的详细天气预报信息

2. **getAlerts**
   - 功能：获取美国某个州的天气警报
   - 参数：
     - state: 两字母的美国州代码（例如 CA, NY）
   - 返回：指定州的天气警报信息

### MCP 工具注册

项目通过 Spring AI 的 `ToolCallbackProvider` 将天气服务方法注册为可供 AI 模型调用的工具。这使得 AI 模型能够直接调用天气服务获取实时天气数据。

## 项目部署运行步骤

### 依赖环境条件

- JDK 17 或更高版本
- Maven 3.6.0 或更高版本

### 构建步骤

1. 克隆或下载项目代码到本地

2. 进入项目根目录

3. 执行 Maven 构建命令：

```bash
mvn clean package
```

### 运行步骤

#### 方法一：使用 Maven 运行

在项目根目录执行：

```bash
mvn spring-boot:run
```

#### 方法二：使用 Java 运行 JAR 文件

构建完成后，在 target 目录下会生成 JAR 文件，执行：

```bash
java -jar target/McpServerSample-0.0.1-SNAPSHOT.jar
```

### 访问服务

服务启动后，默认在 8086 端口运行。可以通过以下方式验证服务是否正常启动：

- 查看控制台输出，确认服务已成功启动
- 服务日志将记录在 `./model-context-protocol/mcp-weather-stdio-server.log` 文件中

