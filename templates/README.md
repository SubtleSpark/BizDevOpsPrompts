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

## 使用说明

1. templates目录下的文件默认被.gitignore排除，避免提交大量第三方内容
2. 需要时可以手动克隆相关仓库到对应目录
3. 分析这些模板后，在`generated/`目录创建优化的提示词套装

## 克隆命令

```bash
# 克隆主要模板仓库
git clone https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools.git templates/system-prompts-and-models-of-ai-tools

# 克隆规范驱动开发指南
git clone https://github.com/jasonkneen/kiro.git templates/kiro-full

# 克隆AI提示词工程与工作流集合
git clone https://github.com/NeekChaw/RIPER-5.git templates/RIPER-5
```

## 注意事项

- 第三方仓库内容仅用于学习和参考
- 生成的提示词应该是原创内容，避免直接复制
- 定期更新模板仓库以获取最新内容