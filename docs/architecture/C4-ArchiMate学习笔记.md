# C4 模型与 ArchiMate 学习笔记

## 📚 相关资源链接表

| 资源名称 | 链接 | 说明 |
|---------|------|------|
| **C4 模型官网** | https://c4model.com/abstractions | C4 模型官方文档和抽象概念 |
| **C4 工具支持** | https://c4model.com/tooling | C4 官方推荐的工具列表 |
| **ArchiMate 官方** | https://www.opengroup.org/archimate-forum/archimate-overview | The Open Group 管理的 ArchiMate 标准 |
| **ArchiMate 规范** | https://pubs.opengroup.org/architecture/archimate3-doc/ | ArchiMate 3.2 官方规范文档 |
| **ArchiMate 与 C4** | https://www.archimatetool.com/blog/2020/04/18/c4-model-architecture-viewpoint-and-archi-4-7/ | ArchiMate 如何支持 C4 模型 |
| **Archi 工具官网** | https://www.archimatetool.com/ | 开源 ArchiMate 建模工具 |
| **Structurizr 官网** | https://structurizr.com/ | C4 官方创造者设计的工具 |
| **IcePanel 官网** | https://icepanel.io/c4-model | 实时协作 C4 建模工具 |
| **C4-PlantUML** | https://github.com/plantuml-stdlib/C4-PlantUML | PlantUML 的 C4 支持库 |

---

## 1️⃣ C4 模型是什么？

### 核心定义

**C4 模型** 是一套用于软件架构可视化和记录的标准化方法论，由 Simon Brown 创建，提供了一套通用的抽象概念和图表类型，让软件架构师和开发人员能够以清晰、结构化的方式描述和交流系统设计。

### C4 的四层抽象

C4 model 使用 4 个层级的抽象来描述软件系统的静态结构：

1. **软件系统（Software System）**
   - 最高层级，描述整个系统的全局视图
   - 用于系统上下文图（System Context Diagram）

2. **容器（Container）**
   - 第二层级，如应用程序、数据库等独立部署的组件
   - 用于容器图（Container Diagram）

3. **组件（Component）**
   - 第三层级，容器内部的逻辑构成部分
   - 用于组件图（Component Diagram）

4. **代码（Code）**
   - 最低层级，具体的实现细节，如类、接口、函数等
   - 用于代码图（Code Diagram）

### C4 的设计理念

- **以抽象为先** - 基于软件架构师和开发人员实际思考方式设计
- **简洁易学** - 通过有限的抽象和图表类型保持简单
- **包含参与者** - 考虑到系统的使用者（用户、角色等）

### 额外的图表类型

除了核心的四层外，C4 还提供了：
- **系统景观图（System Landscape Diagram）** - 显示多个软件系统
- **动态图（Dynamic Diagram）** - 展示系统间的交互序列
- **部署图（Deployment Diagram）** - 展示系统的物理部署情况

---

## 2️⃣ ArchiMate 是什么？

### 核心定义

**ArchiMate** 是一个标准化的架构建模语言，由 The Open Group 开发，用于创建、记录和交流软件架构。它提供了一套统一的概念、符号和关系，使架构师能够以标准化的方式描述系统架构。

### 官方地位

- **管理机构** - The Open Group（通过 ArchiMate Forum）
- **最新版本** - ArchiMate 3.2（2022年10月发布）
- **性质** - 开放标准，独立于具体工具

### ArchiMate 的核心概念：架构视点（Architecture Viewpoint）

架构视点是 ArchiMate 的核心思想，定义了一种特定的"看问题的方式"：

**定义**：一组规范和约定，用于为特定的利益相关者解决特定的关切问题

**核心要素**：
- **目标受众** - 谁使用这个视点（如 CISO、技术主管等）
- **关键关切** - 解决什么问题（如安全性、性能、成本等）
- **所需的细节层级** - 概览 vs 详细
- **使用的概念和关系类型** - 哪些 ArchiMate 元素
- **表示方式** - 图表、目录、矩阵等

### 架构视点的实际例子

**互联网数据流安全视点**（文章中的例子）：
- 为 CISO 准备的视点，关注互联网相关的数据流
- 只使用 ArchiMate 的子集（Node、Network 等）
- 网络区域用大方框表示，内部嵌套节点
- 风险流用红色标记
- 标签和颜色双重标记（兼容色盲和黑白打印）

---

## 3️⃣ C4 与 ArchiMate 的映射关系

### 元素映射表

| C4 元素 | ArchiMate 映射 | 说明 |
|--------|----------------|------|
| **Person** | Business Actor | 人类参与者 |
| **Software System** | Application Component | 软件系统 |
| **Container** | Application Component | 容器（应用/数据库） |
| **Component** | Application Function | 组件 |
| **Code Element** | Application Function | 代码级元素（类、函数等） |
| **Relationship** | Triggering Relationship | 调用关系（从调用者到被调用者） |

### 组合使用的优势

- **C4** 提供了独立于工具的架构描述方法
- **ArchiMate** 提供了标准化的表示语言和工具
- **两者结合** - 可以用 ArchiMate 标准来实现 C4 的图表，同时获得模型化和自动化分析的好处

---

## 4️⃣ 支持 C4 的工具对比

### 工具排名与特点

#### 🏆 **专门为 C4 设计的工具**

**1. Structurizr**（官方推荐）
- 由 C4 模型创造者 Simon Brown 开发
- **特点**：
  - "diagrams as code" 方式
  - 从单一模型自动生成多个 C4 图
  - 支持四层级自动关联
- **价格**：免费开源版 + 付费网络平台
- **适用场景**：专业企业级应用

**2. IcePanel**（新兴明星）
- 实时协作模型工具
- **特点**：
  - 内置 C4 模型支持
  - 交互式缩放四层级图表
  - 实时协作功能
- **价格**：免费版和付费版都有
- **适用场景**：团队协作，需要交互式查看

#### 💻 **代码即图表方式**

**3. Mermaid.js**
- 免费开源，JavaScript 库
- 内置 C4 支持
- 易于使用，适合文档集成
- **适用场景**：文档中嵌入 C4 图

**4. PlantUML**
- 免费开源
- 有专门的 C4 扩展项目
- **适用场景**：DevOps 集成

#### 🎨 **通用图表工具支持 C4**

**5. Diagrams.net**（原 draw.io）
- 免费在线工具
- 内置 C4 记号
- 开源，使用简单

**6. Visual Paradigm Online**
- 商业工具
- 功能全面

**7. Enterprise Architect**（Sparx Systems）
- 企业级方案
- 官方支持的 C4 模型插件

### 工具选择建议

| 场景 | 推荐工具 | 原因 |
|------|--------|------|
| 最专业、功能最全 | Structurizr | 官方设计，功能完整 |
| 团队协作、实时编辑 | IcePanel | 实时同步，交互式 |
| 开源免费、入门级 | Mermaid.js 或 Diagrams.net | 无成本，易上手 |
| DevOps/代码集成 | PlantUML | 代码友好 |
| 企业级方案 | Enterprise Architect | 功能全面 |

---

## 5️⃣ PlantUML 与 C4：手动维护问题详解

### PlantUML 对 C4 的支持

#### 支持的图表类型

PlantUML 支持创建 C4 的所有层级：

1. **System Context Diagram** - `!include C4_Context.puml`
2. **Container Diagram** - `!include C4_Container.puml`
3. **Component Diagram** - `!include C4_Component.puml`
4. **Code Diagram** - 包含在 Component 中
5. **Dynamic Diagram** - `!include C4_Dynamic.puml`
6. **Deployment Diagram** - 支持

#### 关键限制：分离的图表

PlantUML 的 C4 支持是"分离的"，而不是"关联的"：
- 每个图表类型需要独立的 `.puml` 文件
- **不存在**自动的层级"钻取"机制
- 需要**手动维护**多个图表之间的一致性

### "手动维护"的具体含义

#### 场景：电商系统架构的 C4 图

**第1层：System Context（系统上下文图）**

```plantuml
@startuml
Person(customer, "Customer", "使用电商系统的顾客")
System(ecommerce, "E-Commerce System", "提供在线购物功能")
System_Ext(payment, "Payment Gateway", "第三方支付系统")

Rel(customer, ecommerce, "uses")
Rel(ecommerce, payment, "requests payment")
@enduml
```

这个图定义了：
- 系统名字：**"E-Commerce System"**
- 系统的职责：**"提供在线购物功能"**

**第2层：Container（容器图）**

```plantuml
@startuml
Person(customer, "Customer")

Container(web, "Web Application", "React", "提供购物界面")
Container(api, "API Server", "Node.js", "处理业务逻辑")
ContainerDb(db, "Database", "PostgreSQL", "存储产品和订单数据")

Rel(customer, web, "uses")
Rel(web, api, "calls")
Rel(api, db, "reads/writes")
@enduml
```

#### ❌ 数据不一致的问题

| 信息 | System Context 图 | Container 图 | 问题 |
|------|-----------------|-------------|------|
| 系统名称 | "E-Commerce System" | （没有了） | ❌ Container 图没有明确说明这些容器属于哪个系统 |
| 系统描述 | "提供在线购物功能" | （分散在各容器中） | ❌ 需要从各个容器推断 |
| 系统与支付系统的关系 | 明确定义 | （没有体现） | ❌ 容器图没有显示与外部系统的交互 |

#### 维护问题举例

**假设需求变更**：系统要增加直播带货功能

修改 Context 图：
```plantuml
System(ecommerce, "E-Commerce System", "提供在线购物和直播带货功能")
```

**问题**：Container 图没有自动更新，两个图变成不一致的状态！

你需要**手动**：
1. 打开 Container 图文件
2. 检查是否需要添加新容器（如直播服务）
3. 同步相关信息
4. 检查 Component 图
5. 再检查 Code 图
6. 重新生成所有图表验证一致性

#### ✅ 对比：Structurizr 的自动关联

```structurizr
workspace {
    model {
        customer = person "Customer"

        ecommerce = softwareSystem "E-Commerce System" {
            web = container "Web App" "React"
            api = container "API" "Node.js"
            db = container "Database" "PostgreSQL"
        }

        payment = softwareSystem "Payment"
    }

    views {
        systemContext ecommerce { /* 自动生成 */ }
        container ecommerce { /* 自动生成 */ }
        component api { /* 自动生成 */ }
    }
}
```

**关键区别**：
- 系统定义只有一份
- 从这一份模型**自动**生成四层级的图
- 修改一处，**所有图都同步**更新

### 手动维护的三大成本

| 方面 | PlantUML | Structurizr/IcePanel |
|------|---------|-------------------|
| **修改时间** | 需要改多个文件 | 改一个模型 |
| **出错风险** | 高（容易遗漏） | 低（自动同步） |
| **文档一致性** | 需要人工检查 | 自动保证 |

### 何时选择 PlantUML

#### ✅ PlantUML 就够了

- 小项目：只有 1-2 个 C4 图
- 一次性图：画好就不再改
- 学习 C4 模型：简单演示
- 不需要自动钻取：可以接受手动跳转
- 低成本要求：完全免费

#### ❌ 需要升级到 Structurizr

- 大型架构：要维护 10+ 张图表
- 长期维护：架构经常变更
- 团队协作：需要保证团队间的一致性
- 交互式查看：需要在四层级间缩放
- 企业级需求：需要专业支持

---

## 📋 核心要点总结

### C4 模型

- ✅ 四层抽象：System → Container → Component → Code
- ✅ 独立于工具
- ✅ 适合架构描述和团队沟通

### ArchiMate

- ✅ 标准化的建模语言
- ✅ 提供"架构视点"的概念
- ✅ 可以用来实现 C4 模型

### C4 + ArchiMate

- ✅ 用 ArchiMate 实现 C4，获得标准化和可分析性

### 工具选择

| 需求 | 工具 |
|------|------|
| 官方推荐 + 功能完整 | **Structurizr** |
| 团队协作 + 实时编辑 | **IcePanel** |
| 免费 + 简单 | **PlantUML / Diagrams.net** |
| 文档集成 | **Mermaid.js** |

### PlantUML 的权衡

- ✅ **优点**：免费、开源、易学
- ❌ **缺点**：需要手动维护多个文件，容易不一致

---

## 🔗 延伸阅读

- [C4 Model Official](https://c4model.com/)
- [ArchiMate Standard](https://pubs.opengroup.org/architecture/archimate3-doc/)
- [Structurizr Documentation](https://structurizr.com/help)
- [C4-PlantUML README](https://github.com/plantuml-stdlib/C4-PlantUML/blob/master/README.md)