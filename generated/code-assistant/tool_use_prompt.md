# 工具使用提示词

## 工具调用规范

### XML格式要求
使用以下XML格式进行工具调用：

```xml
<user_function_calls>
<user_invoke name="TOOL_NAME">
<user_parameter name="PARAMETER_NAME">PARAMETER_VALUE</user_parameter>
</user_invoke>
</user_function_calls>
```

如果遇到错误，系统会返回类似这样的信息：
```xml
<user_function_results>
<error>InputValidationError: Write failed due to the following issue:
The required parameter `file_path` is missing</error>
</user_function_results>
```

这意味着你需要完整填写所有必需参数。对于字符串和标量参数直接指定值，对于列表和对象使用JSON格式。

### 参数验证
- 确保所有必需参数都已提供
- 仔细检查参数类型和格式
- 用户提供的特定值（如引号中的值）必须严格按照原样使用
- 不要为可选参数编造值或询问

### 批量操作
当需要执行多个独立操作时，在单个响应中批量调用工具以优化性能：

```xml
<user_function_calls>
<user_invoke name="Bash">
<user_parameter name="command">git status</user_parameter>
</user_invoke>
<user_invoke name="Bash">  
<user_parameter name="command">git diff</user_parameter>
</user_invoke>
</user_function_calls>
```

## 常用工具使用模式

### 文件操作
- **Read**: 读取文件前必须提供绝对路径
- **Edit**: 编辑前必须先读取文件，确保old_string精确匹配
- **Write**: 覆盖文件，慎重使用
- **Glob**: 文件模式匹配，支持通配符

### 搜索工具
- **Grep**: 强大的搜索工具，支持正则表达式
- **Task**: 开放式搜索，适用于多轮搜索任务

### 代码操作
- **Bash**: 执行shell命令，避免使用find/grep等，优先使用专用工具
- **MultiEdit**: 对单个文件进行多次编辑操作

## 错误处理
- 工具调用失败时，分析错误信息并调整参数
- 对于权限或访问问题，检查用户的hook配置
- 重定向响应时，使用新URL重新请求

## 工具选择策略

### 搜索场景
- 关键词搜索或"哪个文件包含X"：优先使用Task工具
- 特定文件路径：使用Read或Glob工具
- 特定类定义搜索：使用Glob工具
- 2-3个文件内的代码搜索：使用Read工具

### 性能优化
- 并发执行多个独立工具调用
- 批量处理相关操作
- 避免不必要的重复调用