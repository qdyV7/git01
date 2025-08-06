# API 文档模板

## 概述

本模板提供了为公共API、函数和组件创建全面文档的标准格式。当项目中添加源代码时，请使用此模板来记录所有公共接口。

## API 文档结构

### 1. API 端点文档模板

```markdown
## [HTTP方法] /api/endpoint

### 描述
简要描述此API端点的功能和用途。

### 请求

#### URL参数
| 参数名 | 类型 | 必需 | 描述 | 示例值 |
|--------|------|------|------|--------|
| id | string | 是 | 用户唯一标识符 | "12345" |
| format | string | 否 | 响应格式 | "json" |

#### 查询参数
| 参数名 | 类型 | 必需 | 默认值 | 描述 |
|--------|------|------|--------|------|
| page | number | 否 | 1 | 页码 |
| limit | number | 否 | 10 | 每页记录数 |

#### 请求体
```json
{
  "name": "string",
  "email": "string",
  "age": "number"
}
```

### 响应

#### 成功响应 (200)
```json
{
  "success": true,
  "data": {
    "id": "12345",
    "name": "张三",
    "email": "zhangsan@example.com"
  },
  "message": "操作成功"
}
```

#### 错误响应
| 状态码 | 描述 | 响应体示例 |
|--------|------|------------|
| 400 | 请求参数错误 | `{"error": "Invalid parameters"}` |
| 401 | 未授权 | `{"error": "Unauthorized"}` |
| 404 | 资源未找到 | `{"error": "Resource not found"}` |
| 500 | 服务器内部错误 | `{"error": "Internal server error"}` |

### 示例

#### cURL 示例
```bash
curl -X POST \
  http://localhost:3000/api/users \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "张三",
    "email": "zhangsan@example.com",
    "age": 25
  }'
```

#### JavaScript 示例
```javascript
const response = await fetch('/api/users', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    name: '张三',
    email: 'zhangsan@example.com',
    age: 25
  })
});

const data = await response.json();
console.log(data);
```

#### Python 示例
```python
import requests

url = "http://localhost:3000/api/users"
payload = {
    "name": "张三",
    "email": "zhangsan@example.com",
    "age": 25
}

response = requests.post(url, json=payload)
data = response.json()
print(data)
```
```

### 2. 函数文档模板

```markdown
## 函数名: functionName

### 语法
```javascript
functionName(param1, param2, options)
```

### 描述
详细描述函数的功能、用途和行为。

### 参数

| 参数名 | 类型 | 必需 | 默认值 | 描述 |
|--------|------|------|--------|------|
| param1 | string | 是 | - | 第一个参数的描述 |
| param2 | number | 否 | 0 | 第二个参数的描述 |
| options | object | 否 | {} | 配置选项对象 |

#### options 对象属性

| 属性名 | 类型 | 默认值 | 描述 |
|--------|------|--------|------|
| timeout | number | 5000 | 超时时间（毫秒） |
| retries | number | 3 | 重试次数 |

### 返回值

| 类型 | 描述 |
|------|------|
| Promise<Object> | 返回一个Promise，解析为结果对象 |

#### 返回值结构
```javascript
{
  success: boolean,
  data: any,
  error?: string
}
```

### 异常

| 异常类型 | 触发条件 | 描述 |
|----------|----------|------|
| TypeError | param1不是字符串 | 参数类型错误 |
| RangeError | param2超出有效范围 | 参数值超出范围 |

### 示例

#### 基本用法
```javascript
const result = await functionName('hello', 42);
console.log(result);
// 输出: { success: true, data: 'processed hello 42 times' }
```

#### 带选项的用法
```javascript
const result = await functionName('world', 10, {
  timeout: 3000,
  retries: 5
});
```

#### 错误处理
```javascript
try {
  const result = await functionName('test', -1);
} catch (error) {
  console.error('函数执行失败:', error.message);
}
```

### 注意事项
- 列出使用此函数时需要注意的重要事项
- 性能考虑
- 兼容性信息

### 相关函数
- [relatedFunction1](#relatedfunction1)
- [relatedFunction2](#relatedfunction2)
```

### 3. 组件文档模板

```markdown
## 组件名: ComponentName

### 概述
简要描述组件的功能和用途。

### 导入
```javascript
import ComponentName from './ComponentName';
// 或
const ComponentName = require('./ComponentName');
```

### 属性 (Props)

| 属性名 | 类型 | 必需 | 默认值 | 描述 |
|--------|------|------|--------|------|
| title | string | 是 | - | 组件标题 |
| visible | boolean | 否 | true | 是否可见 |
| onClose | function | 否 | - | 关闭回调函数 |
| children | ReactNode | 否 | - | 子组件内容 |

### 事件

| 事件名 | 参数 | 描述 |
|--------|------|------|
| onClose | () => void | 组件关闭时触发 |
| onChange | (value: any) => void | 值变化时触发 |

### 方法

| 方法名 | 参数 | 返回值 | 描述 |
|--------|------|--------|------|
| show | () | void | 显示组件 |
| hide | () | void | 隐藏组件 |
| reset | () | void | 重置组件状态 |

### 样式类

| 类名 | 描述 |
|------|------|
| .component-name | 根容器样式 |
| .component-name__header | 头部样式 |
| .component-name__content | 内容区域样式 |

### 示例

#### 基本用法
```jsx
<ComponentName 
  title="示例标题"
  visible={true}
  onClose={() => console.log('组件已关闭')}
>
  <p>这是组件内容</p>
</ComponentName>
```

#### 高级用法
```jsx
import React, { useState, useRef } from 'react';

function App() {
  const [visible, setVisible] = useState(false);
  const componentRef = useRef();

  const handleShow = () => {
    componentRef.current.show();
  };

  return (
    <div>
      <button onClick={handleShow}>显示组件</button>
      <ComponentName 
        ref={componentRef}
        title="高级示例"
        onClose={() => setVisible(false)}
      >
        <div>复杂的内容结构</div>
      </ComponentName>
    </div>
  );
}
```

#### 自定义样式
```css
.component-name {
  background-color: #f0f0f0;
  border-radius: 8px;
}

.component-name__header {
  font-weight: bold;
  color: #333;
}
```

### 可访问性
- 支持键盘导航
- 兼容屏幕阅读器
- 符合WCAG 2.1指南

### 浏览器兼容性
| 浏览器 | 版本 | 支持状态 |
|--------|------|----------|
| Chrome | 60+ | ✅ 完全支持 |
| Firefox | 55+ | ✅ 完全支持 |
| Safari | 12+ | ✅ 完全支持 |
| Edge | 79+ | ✅ 完全支持 |

### 故障排除

#### 常见问题

**Q: 组件不显示怎么办？**
A: 检查 `visible` 属性是否设置为 `true`。

**Q: 样式不生效？**
A: 确保已正确导入组件的CSS文件。

**Q: 事件回调不触发？**
A: 检查事件处理函数是否正确绑定。
```

## 使用指南

### 1. 为新API创建文档
1. 复制对应的模板
2. 填写所有必需字段
3. 提供完整的示例
4. 添加错误处理说明

### 2. 文档维护
- 代码更改时同步更新文档
- 定期审查文档的准确性
- 收集用户反馈并改进文档

### 3. 文档组织
```
docs/
├── api/
│   ├── users.md
│   ├── products.md
│   └── orders.md
├── functions/
│   ├── utilities.md
│   ├── validators.md
│   └── formatters.md
├── components/
│   ├── Button.md
│   ├── Modal.md
│   └── Form.md
└── README.md
```

## 最佳实践

### 1. 文档写作原则
- **清晰性**: 使用简洁明了的语言
- **完整性**: 提供所有必要信息
- **准确性**: 确保示例代码可以运行
- **一致性**: 保持格式和风格统一

### 2. 示例代码要求
- 提供多种语言/框架的示例
- 包含错误处理
- 使用真实的数据示例
- 添加注释说明关键部分

### 3. 维护流程
1. 代码审查时检查文档更新
2. 设置自动化检查确保文档同步
3. 定期进行文档审查
4. 收集和处理用户反馈

## 工具推荐

### 1. 文档生成工具
- **JSDoc**: JavaScript代码注释生成文档
- **Swagger/OpenAPI**: API文档自动生成
- **Storybook**: 组件文档和演示

### 2. 文档托管平台
- **GitBook**: 专业文档网站
- **GitHub Pages**: 免费静态网站托管
- **Netlify**: 现代化部署平台

### 3. 编写工具
- **Markdown编辑器**: Typora, Mark Text
- **在线编辑器**: Notion, GitBook编辑器
- **IDE插件**: 支持Markdown预览的插件