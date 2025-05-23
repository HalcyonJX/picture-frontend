# 智能协同云图库
前端：https://github.com/HalcyonJX/picture-frontend

后端：https://github.com/HalcyonJX/picture-backend

## 项目介绍
基于 Spring Boot + Redis + COS + AI + WebSocket 的企业级智能协同云图库平台。

系统分为公共图库、私有图库和团队共享图库三大模块。

用户可上传图片和检索图片，可以对私有空间进行批量管理、多维检索、编辑和分析；管理员可以上传、审核和管理图片；企业可开通团队空间邀请成员，共享和实时协同编辑图片。

## 主要工作

### 前端
+ 使用Vue3 + cursor 辅助完成前端页面。

### 后端
1. 用户登录：通过 Redis 整合 Spring Session 分布式保存用户登录态，实现了跨服务器的用户识别。

2. 运用 模板方法 设计模式统一封装本地图片和 URL 图片上传的流程，如校验、下载、上传和资源释放，复用代码并提高可维护性。

3. 查询优化：为提高主页热门图片的查询性能，采用 Redis + Caffeine 构建 多级缓存，并通过随机过期时间降低缓存雪崩风险。

4. AI 扩图：基于阿里云百炼大模型封装 AI 绘图服务，提供创建与查询任务的 API，采用异步任务轮询处理进度。

5. 基于 Sa-Token 的 Kit 模式实现了多账号体系的RBAC 权限控制，通过从请求上下文中获取参数实现了统一的权限校验逻辑，并运用注解合并简化了鉴权注解的使用，轻松实现方法级别的权限校验。

6. 基于 WebSocket +事件驱动设计实现多人协作编辑图片功能，自定义握手拦截器确保权限校验通过后才能连接，并通过 “编辑锁” 机制，避免编辑冲突。