# Chaozhi Admin

AI-first full-stack admin scaffold for Spring Boot + Vue business modules.

Chaozhi Admin 是一套面向全栈开发者的 AI 驱动全栈后台脚手架。  
你可以基于结构化的 Markdown 需求文档，生成 Spring Boot + Vue 的业务模块代码，而不是反复手写 CRUD、权限、状态流转和接口联调代码。

## 这是什么

很多后台模板只解决其中一层：

- 有的偏前端页面脚手架
- 有的偏后端模板工程
- 有的提供组件，但没有完整的业务交付工作流

Chaozhi Admin 解决的是另一类问题：

- 面向全栈业务模块生成，而不只是生成页面
- 以 Markdown 需求文档为输入，而不是依赖零散聊天记录
- 通过 `CLAUDE.md` 固化仓库级规则，降低 AI 输出漂移
- 提前统一接口契约、鉴权方式、权限规范、状态流转风格
- 目标是生成可运行、可联调的业务代码，而不是只有演示价值的 mock 页面

## 可以生成什么

在“系统总览 + 单模块需求文档”的输入方式下，默认目标是整套全栈模块：

- 后端 controller / service / mapper / entity / DTO / VO
- 前端 API / route / page / i18n
- 页面权限 / 按钮权限 / 接口权限
- CRUD 列表页与业务表单页
- submit / approve / confirm / cancel 这类状态动作接口
- 来源单据联动能力，例如采购订单带入入库单

## 核心约定

为了让 AI 输出稳定，这个仓库提前固定了一些规则：

- 成功响应结构：`{ code: 0, data: ... }`
- 鉴权方式：`token + Redis session + Authorization header`
- 新增后端接口默认需要登录后访问
- 状态动作接口默认使用：`PUT /{module}/{id}/{action}`
- 来源单查询默认使用：`GET /{source-module}/detail-by-no?orderNo=xxx`
- 新前端模块默认直接联调真实后端接口，不生成 mock 占位逻辑
- 新模块默认带权限接入，不跳过权限控制

## 项目结构

```text
chaozhi-admin/
├── chaozhi-backend/     Spring Boot 后端脚手架
├── chaozhi-web/         Vue 3 + Vite + Ant Design Vue 前端后台工程
├── CLAUDE.md            仓库级 AI 生成规范
└── demo/                系统总览、权限规范、SQL、模块提示词示例
```

## 工作流怎么跑

1. 先写一份 `系统总览.md`，定义业务域和模块边界。
2. 再写单模块需求文档，例如 `入库管理.md`。
3. 让 AI 按以下规则生成代码：
   - `CLAUDE.md`
   - `chaozhi-backend/CLAUDE.md`
   - `chaozhi-web/CLAUDE.md`
4. 直接运行生成后的前后端代码，联调真实接口。

## 项目截图

### 登录页

![登录页](./.github/assets/login-page.png)

### 锁屏页

![锁屏页](./.github/assets/login-lock-screen.png)

### 采购订单页

![采购订单页](./.github/assets/purchase-order-page.png)

## Demo 资料

仓库内已经提供了一套完整的 demo 文档，放在 `demo/` 目录下：

- `系统总览.md`
- `权限体系规范.md`
- `模块提示词示例/物料.md`
- `模块提示词示例/采购订单.md`
- `模块提示词示例/入库管理.md`
- `模块提示词示例/库存管理.md`
- `模块提示词示例/库存流水.md`
- `模块提示词示例/销售出库.md`
- `chaozhi.sql`

这些不是凑数文档，而是这套脚手架的核心资产：

- 系统怎么拆模块
- 模块需求怎么写
- 权限怎么设计
- AI 该按什么规则生成代码

## 技术栈

- 后端：Spring Boot、MyBatis-Plus、Redis
- 前端：Vue 3、TypeScript、Vite、Ant Design Vue、Pinia、vue-router
- 协作方式：`CLAUDE.md` + Markdown 业务需求文档

## 快速启动

### 启动后端

```bash
cd chaozhi-backend
mvn spring-boot:run
```

### 启动前端

```bash
cd chaozhi-web
pnpm install
pnpm dev
```

本地默认地址：

- 前端：`http://localhost:5666`
- 后端：`http://localhost:8080`

## 这套仓库为什么会越用越顺

这个仓库真正有价值的，不只是脚手架本身，而是这一整套可复用资产：

- 稳定的工程规范
- 可复用的系统总览模板
- 可复用的模块需求文档
- 可复用的权限体系约定
- 可复用的全栈模块生成示例

这意味着你不是每做一个模块都重新从零开始，而是在沉淀一套越来越稳定的业务生成体系。

## 当前状态

当前仓库处于对外公开的早期阶段，核心目标很明确：

验证 AI 驱动的全栈业务模块生成工作流是否足够稳定、足够高效。

当前说明：

- 后端仍保留部分占位包名，例如 `com.xxx.xxx`
- 当前 workflow 和 demo 已可使用
- 后续会持续优化文档表现、生成质量和模块示例完整度

## Roadmap

- 优化仓库首页与公开展示资产
- 增加更完整的业务模块示例
- 继续打磨默认权限接入方案
- 提升生成页面质量与 CRUD 交互细节
- 补充更完整的开源发布与上手文档

## License

本项目采用 MIT License，详见 [LICENSE](./LICENSE)。
