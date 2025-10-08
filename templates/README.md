# Templates 依赖的 GitHub 仓库

## 主要数据源

### 1. system-prompts-and-models-of-ai-tools
- **仓库地址**: https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools
- **用途**: 收集各种AI工具的系统提示词和模型信息
- **更新频率**: 定期更新
- **本地路径**: `templates/system-prompts-and-models-of-ai-tools/`

### 2. kiro (Spec-Driven Development Guide)
- **仓库地址**: https://github.com/jasonkneen/kiro
- **用途**: 规范驱动开发方法论和最佳实践指南
- **核心内容**: Requirements → Design → Tasks 三阶段开发流程
- **本地路径**: `templates/kiro-full/`
- **特色**: 
  - EARS标准需求格式化
  - AI协作优化的提示策略
  - 系统化设计决策框架
  - 完整的质量保证流程

### 3. RIPER-5 (AI提示词工程与工作流集合)
- **仓库地址**: https://github.com/NeekChaw/RIPER-5.git
- **用途**: 高质量、结构化的AI提示词和工作流集合，专注于提升AI在软件开发等领域的协作效率
- **核心内容**: RIPER-5行为协议 + Claude Code专用提示词集合
- **本地路径**: `templates/RIPER-5/`
- **特色**:
  - RIPER-5 AI编码行为协议框架，确保安全可控的编码流程
  - 多种专业工作流：需求收集、代码重构、专业Git提交等
  - 针对Claude模型优化的提示词集合
  - 多代理协作深度思考工作流
  - 实用的开发场景解决方案

### 4. kingkongshot-prompts (精选提示词集合)
- **仓库地址**: https://github.com/kingkongshot/prompts
- **用途**: 精选的AI提示词集合，包含开发工具、代理和可视化等多个领域
- **核心内容**: Claude提示词、Kiro工作流规范、Obsidian可视化等
- **本地路径**: `templates/kingkongshot-prompts/`
- **特色**:
  - Claude开发环境配置和代理模板
  - Kiro规范驱动开发工作流（中英文）
  - 专业的Git提交格式化工具
  - Obsidian Canvas功能框架图绘制指南
  - 内存网络构建和库使用研究代理

### 5. Anthropic Engineering Blog (AI代理系统工程实践)
- **博客地址**: https://www.anthropic.com/engineering/
- **用途**: Anthropic官方工程博客，分享AI代理系统构建的最佳实践和技术洞察
- **核心内容**: 代理工具设计、上下文工程、多代理系统、性能优化等
- **特色**:
  - Anthropic官方工程团队实战经验分享
  - 聚焦代理系统（Agentic AI）的完整技术栈
  - 从工具设计到性能基准测试的系统化方法论
  - 结合评估驱动开发(Evaluation-Driven Development)的实践案例
  - 涵盖MCP协议、工具优化、提示工程等前沿技术

## 使用说明

1. templates目录下的仓库通过 Git Submodule 管理，确保版本可控
2. 初次克隆本仓库后，需要初始化 submodules
3. 分析这些模板后，在`generated/`目录创建优化的提示词套装

## Submodule 管理命令

### 初次克隆仓库
```bash
# 克隆主仓库并初始化所有 submodules
git clone --recursive https://github.com/<your-username>/BizDevOpsPrompts.git

# 或者分步执行
git clone https://github.com/<your-username>/BizDevOpsPrompts.git
cd BizDevOpsPrompts
git submodule update --init --recursive
```

### 添加新的 Submodule（仅维护者需要）
```bash
# 添加主要模板仓库
git submodule add https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools.git templates/system-prompts-and-models-of-ai-tools

# 添加规范驱动开发指南
git submodule add https://github.com/jasonkneen/kiro.git templates/kiro-full

# 添加AI提示词工程与工作流集合
git submodule add https://github.com/NeekChaw/RIPER-5.git templates/RIPER-5

# 添加精选提示词集合
git submodule add https://github.com/kingkongshot/prompts.git templates/kingkongshot-prompts
```

### 更新 Submodules
```bash
# 更新所有 submodules 到最新版本
git submodule update --remote --merge

# 更新单个 submodule
cd templates/system-prompts-and-models-of-ai-tools
git pull origin main
cd ../..
git add templates/system-prompts-and-models-of-ai-tools
git commit -m "Update submodule: system-prompts-and-models-of-ai-tools"
```

## 注意事项

- 第三方仓库内容仅用于学习和参考
- 生成的提示词应该是原创内容，避免直接复制
- Submodules 会锁定在特定 commit，确保环境一致性
- 定期使用 `git submodule update --remote` 更新到最新版本