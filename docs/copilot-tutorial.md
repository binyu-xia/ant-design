# GitHub Copilot 使用教程

## 目录

1. [教程目标与适用人群](#1-教程目标与适用人群)
2. [Copilot 简介](#2-copilot-简介)
3. [环境准备](#3-环境准备)
4. [基础使用](#4-基础使用)
5. [高效提问方法](#5-高效提问方法)
6. [典型场景示例](#6-典型场景示例)
7. [质量与安全实践](#7-质量与安全实践)
8. [团队协作规范](#8-团队协作规范)
9. [常见问题与排错](#9-常见问题与排错)
10. [进阶能力与最佳实践](#10-进阶能力与最佳实践)

---

## 1. 教程目标与适用人群

### 1.1 教程目标

本教程帮助开发者快速上手 GitHub Copilot，掌握从安装配置到高效使用的完整流程，提升日常开发效率。完成本教程后，你将能够：

- 独立完成 Copilot 的安装、登录与基础配置
- 熟练使用内联补全、Copilot Chat、Inline Chat 三种交互方式
- 根据不同场景选用合适的提示词策略
- 在团队中推广 Copilot 并制定合理的使用规范

### 1.2 适用人群

| 人群 | 推荐章节 | 预期收益 |
|------|----------|----------|
| **新手开发者** | 全部章节 | 借助 Copilot 加速学习，快速理解代码结构与最佳实践 |
| **个人开发者** | 3 → 4 → 5 → 6 | 减少重复劳动，聚焦业务逻辑，提升开发速度 |
| **技术 Leader** | 7 → 8 → 10 | 制定团队规范，评估 AI 工具收益，管控使用风险 |
| **团队/企业** | 3 → 7 → 8 → 9 | 统一编码规范，降低沟通成本，加快 Code Review 效率 |

### 1.3 前提条件

- 拥有 GitHub 账号（个人或企业组织账号均可）
- 具备基本的编程基础（了解至少一门编程语言）
- 使用支持 Copilot 的 IDE（VS Code、JetBrains 系列、Neovim 等）
- 网络能够访问 `github.com`（企业内网用户参见 [9.4 代理配置](#94-公司网络代理问题)）

### 1.4 学习路径建议

```
快速上手（30 分钟）
└── 第 3 章：环境准备 → 第 4 章：基础使用

日常提效（1 小时）
└── 第 5 章：高效提问 → 第 6 章：典型场景示例

团队落地（2 小时）
└── 第 7 章：质量与安全 → 第 8 章：团队协作规范

进阶掌握（按需）
└── 第 10 章：进阶能力与最佳实践
```

---

## 2. Copilot 简介

### 2.1 什么是 GitHub Copilot

GitHub Copilot 是由 GitHub 与 OpenAI 联合开发的 AI 编程助手，基于大型语言模型（LLM）训练而成，能够根据上下文自动补全代码、生成函数、回答编程问题。它深度集成在主流 IDE 中，以"结对程序员"的形式辅助日常开发工作。

**发展历程：**

| 时间 | 里程碑 |
|------|--------|
| 2021 年 6 月 | Copilot 技术预览，面向部分开发者开放 |
| 2022 年 6 月 | 正式向所有开发者开放，推出订阅制 |
| 2023 年 3 月 | Copilot X 发布，引入 Chat、Voice、PR 等能力 |
| 2023 年 7 月 | Copilot for Business 正式商用，企业管控增强 |
| 2024 年 | Copilot Workspace、多模型支持、Copilot Edits 上线 |
| 2025 年 | Agent 模式（全自动任务执行）正式推出 |

### 2.2 产品版本对比

| 功能 | Free | Individual | Business | Enterprise |
|------|------|------------|----------|------------|
| 代码补全 | ✅（有限次） | ✅ 无限 | ✅ 无限 | ✅ 无限 |
| Copilot Chat | ✅（有限次） | ✅ | ✅ | ✅ |
| 代码审查 | ❌ | ❌ | ✅ | ✅ |
| 组织管理策略 | ❌ | ❌ | ✅ | ✅ |
| 不用于训练模型 | ❌ | ❌ | ✅ | ✅ |
| 自定义知识库 | ❌ | ❌ | ❌ | ✅ |
| 私有化部署 | ❌ | ❌ | ❌ | 部分支持 |

### 2.3 Copilot 能做什么

- ✅ **代码补全**：根据当前代码上下文智能提示下一行或整个函数
- ✅ **自然语言转代码**：通过注释描述需求，自动生成对应代码
- ✅ **代码重构**：识别代码模式，提供更优化的写法建议
- ✅ **生成测试**：根据现有函数自动生成单元测试
- ✅ **代码解释**：用自然语言解释复杂代码逻辑
- ✅ **修复 Bug**：分析错误信息，给出修复方案
- ✅ **编写文档**：自动生成函数注释和 README
- ✅ **多文件重构**：通过 Copilot Edits 跨文件批量修改
- ✅ **自动化任务**：通过 Agent 模式执行复杂的多步骤任务

### 2.4 Copilot 不能做什么

- ❌ 不能保证生成代码完全正确，需要人工审查
- ❌ 不能替代架构设计和技术决策
- ❌ 不了解你的业务背景，需要提供充分上下文
- ❌ 不适合处理涉密或敏感数据（见 [7.3 敏感信息防护](#73-敏感信息防护)）
- ❌ 生成的代码可能存在安全漏洞，需要安全审查
- ❌ 不能访问实时互联网信息（内置知识有截止日期）
- ❌ 无法直接操作数据库、文件系统等生产环境资源

---

## 3. 环境准备

### 3.1 注册 GitHub 账号

如果还没有 GitHub 账号：

1. 访问 [github.com/signup](https://github.com/signup)
2. 填写邮箱、用户名、密码
3. 完成邮箱验证
4. 建议开启两步验证（`Settings → Password and authentication → Two-factor authentication`）

### 3.2 获取 Copilot 订阅

1. 访问 [github.com/features/copilot](https://github.com/features/copilot)
2. 选择适合的订阅计划：
   - **Free**：免费，每月有限次补全和对话，适合评估试用
   - **Individual**：个人开发者（月付 $10 / 年付 $100）
   - **Business**：企业团队（$19/用户/月），提供更多管控能力
   - **Enterprise**：大型企业（$39/用户/月），支持自定义知识库
3. **免费资格申请**：在校学生和活跃开源项目维护者可通过 [GitHub Education](https://education.github.com/) 申请免费使用

> 企业用户：订阅后管理员需在 `Organization Settings → Copilot → Policies` 中为成员开启使用权限。

### 3.3 安装 VS Code 插件

1. 打开 VS Code，进入扩展面板（`Ctrl+Shift+X` / `Cmd+Shift+X`）
2. 搜索 `GitHub Copilot` 并点击安装
3. 同时搜索并安装 `GitHub Copilot Chat`（支持对话和 Inline Chat 功能）
4. 安装完成后，VS Code 右下角状态栏会出现 Copilot 图标
5. 点击图标 → `Sign in to GitHub`，在弹出的浏览器窗口中完成授权

**验证登录成功：** 状态栏 Copilot 图标变为白色（非划线状态）即表示已登录。

### 3.4 JetBrains 系列 IDE 安装

适用于 IntelliJ IDEA、WebStorm、PyCharm、GoLand 等：

1. 进入 `File → Settings → Plugins → Marketplace`（macOS：`IntelliJ IDEA → Preferences → Plugins`）
2. 搜索 `GitHub Copilot` 并安装
3. 重启 IDE
4. 进入 `Tools → GitHub Copilot → Login to GitHub`，按提示完成授权

### 3.5 Neovim 安装（可选）

使用 [copilot.vim](https://github.com/github/copilot.vim) 插件：

```vim
" 使用 vim-plug 安装
Plug 'github/copilot.vim'
```

安装后执行 `:Copilot setup` 完成账号授权。

### 3.6 企业 SSO 配置

若公司使用 SAML SSO，授权 Copilot 访问：

1. 访问 `github.com/settings/tokens`
2. 找到 Copilot 相关 OAuth App
3. 点击 `Configure SSO → Authorize` 为所在组织授权

### 3.7 验证安装

新建一个文件，输入注释或函数签名，若出现灰色提示文字则表示 Copilot 已正常工作：

```javascript
// 计算两个数的最大公约数，使用欧几里得算法
function gcd(a, b) {
  // 出现灰色建议文字后按 Tab 接受 ↑
}
```

Copilot 应补全为：

```javascript
function gcd(a, b) {
  while (b !== 0) {
    [a, b] = [b, a % b];
  }
  return a;
}
```

---

## 4. 基础使用

### 4.1 代码补全

Copilot 会在你输入时自动触发建议，显示为灰色内联文字（Ghost Text）。

**VS Code 快捷键：**

| 操作 | Windows/Linux | macOS |
|------|---------------|-------|
| 接受建议 | `Tab` | `Tab` |
| 拒绝建议 | `Esc` | `Esc` |
| 接受单词 | `Ctrl+→` | `Cmd+→` |
| 查看下一个建议 | `Alt+]` | `Option+]` |
| 查看上一个建议 | `Alt+[` | `Option+[` |
| 打开建议面板（多选） | `Ctrl+Enter` | `Ctrl+Enter` |

**完整示例：输入函数签名，Copilot 补全实现**

```typescript
// 输入：
function debounce(fn: Function, delay: number) {

// Copilot 补全结果：
function debounce(fn: Function, delay: number) {
  let timer: ReturnType<typeof setTimeout> | null = null;
  return function (this: unknown, ...args: unknown[]) {
    if (timer) clearTimeout(timer);
    timer = setTimeout(() => {
      fn.apply(this, args);
      timer = null;
    }, delay);
  };
}
```

**触发技巧：**
- 光标停留片刻会自动触发；若未出现建议，按 `Alt+\`（`Option+\`）手动触发
- 打开相关文件（如类型定义文件）可提升建议质量
- 在文件顶部写明导入语句，Copilot 会参考已有依赖生成更贴切的代码

### 4.2 通过注释生成代码

用自然语言描述需求，Copilot 会将注释转化为完整的代码实现。

**Python 示例：**

```python
# 读取 CSV 文件，过滤出年龄大于 18 的记录，并按姓名升序排序后返回 DataFrame
import pandas as pd

def filter_adults(file_path: str) -> pd.DataFrame:
    df = pd.read_csv(file_path)
    return df[df['age'] > 18].sort_values('name').reset_index(drop=True)
```

**TypeScript 示例：**

```typescript
// 深度克隆一个对象，支持 Date、RegExp、Array 等特殊类型
function deepClone<T>(obj: T): T {
  if (obj === null || typeof obj !== 'object') return obj;
  if (obj instanceof Date) return new Date(obj.getTime()) as unknown as T;
  if (obj instanceof RegExp) return new RegExp(obj.source, obj.flags) as unknown as T;
  if (Array.isArray(obj)) return obj.map(item => deepClone(item)) as unknown as T;
  const cloned = {} as T;
  for (const key in obj) {
    if (Object.prototype.hasOwnProperty.call(obj, key)) {
      cloned[key] = deepClone(obj[key]);
    }
  }
  return cloned;
}
```

**注释写作技巧：**
- 注释写得越具体，生成质量越高；避免模糊词如"处理数据"
- 在注释中明确输入类型、输出类型、边界情况（如"空数组返回 0"）
- 英文注释通常能获得更稳定的补全效果

### 4.3 Copilot Chat 对话

在 VS Code 中打开 Copilot Chat 面板（侧边栏 Copilot 图标 或 `Ctrl+Shift+I` / `Ctrl+Alt+I`），用自然语言直接提问。

**内置斜杠指令：**

| 指令 | 用途 | 使用方式 |
|------|------|----------|
| `/explain` | 解释选中代码的逻辑 | 选中代码 → Chat 输入 `/explain` |
| `/fix` | 修复选中代码的问题 | 选中问题代码 → `/fix` |
| `/tests` | 为选中函数生成单元测试 | 选中函数 → `/tests` |
| `/doc` | 为选中代码生成文档注释 | 选中函数/类 → `/doc` |
| `/simplify` | 简化选中的复杂代码 | 选中代码 → `/simplify` |
| `/new` | 创建新文件或项目骨架 | `/new React 组件` |

**上下文变量（在提示词中引用）：**

| 变量 | 含义 |
|------|------|
| `#file:路径` | 引用特定文件 |
| `#selection` | 当前选中的代码 |
| `#codebase` | 整个代码库（需要索引） |
| `#terminal` | 终端最近输出 |
| `#problems` | 编辑器当前报错列表 |

**示例：**

```
#file:src/utils/api.ts 中的 fetchUser 函数存在竞态条件，请分析原因并给出修复方案
```

### 4.4 内联对话（Inline Chat）

在编辑器中选中代码后按 `Ctrl+I`（`Cmd+I`），可直接针对选中代码发出修改指令，结果以差异对比形式展示。

**操作流程：**

```
1. 选中目标代码（可以是一行或多行）
2. 按 Ctrl+I（Cmd+I）打开内联输入框
3. 输入修改描述，如："将 callback 风格改为 async/await"
4. 按 Enter 生成修改建议
5. 审查差异后按 Accept（接受）或 Discard（放弃）
```

**常用 Inline Chat 指令：**

```
将这个 for 循环改为 Array.reduce
为这个函数添加错误处理和 try/catch
给这段代码添加 TypeScript 类型注解
将魔法数字提取为有意义的常量
```

### 4.5 代码重构

Copilot 擅长识别代码异味并给出重构建议。

**示例：重构嵌套回调（Callback Hell）**

选中以下代码，通过 Inline Chat 输入"将嵌套回调改为 async/await 并处理错误"：

```javascript
// 重构前
function loadUserData(userId, callback) {
  getUser(userId, function(err, user) {
    if (err) return callback(err);
    getOrders(user.id, function(err, orders) {
      if (err) return callback(err);
      getShipping(orders[0].id, function(err, shipping) {
        if (err) return callback(err);
        callback(null, { user, orders, shipping });
      });
    });
  });
}

// Copilot 重构后
async function loadUserData(userId: string) {
  const user = await getUser(userId);
  const orders = await getOrders(user.id);
  const shipping = await getShipping(orders[0].id);
  return { user, orders, shipping };
}
```

---

## 5. 高效提问方法

### 5.1 提示词的核心原则

高质量的提示词通常包含以下要素：

```
角色（可选）+ 任务 + 上下文 + 约束条件 + 输出格式
```

**对比示例：**

```
❌ 差：写一个排序函数

✅ 好：用 TypeScript 实现一个稳定的归并排序函数。
      输入：number[] 类型的数组
      输出：排序后的新数组（不修改原数组）
      要求：时间复杂度 O(n log n)，处理空数组和单元素数组的边界情况
```

### 5.2 提示词模板库

#### 生成新功能

```
用 [语言/框架] 实现 [功能名称]。
输入：[参数名称]: [类型] — [描述]
输出：[返回类型] — [描述]
要求：
  - [约束1，如：使用 XXX 库]
  - [约束2，如：兼容 IE11]
  - [约束3，如：处理 XXX 边界情况]
参考风格：[可选，如：参考 #file:src/utils/xxx.ts]
```

#### 代码审查

```
请以资深工程师的视角审查以下代码，重点关注：
1. 潜在的 [性能问题 / 内存泄漏 / 安全漏洞]
2. 可读性和可维护性
3. 是否符合 [JavaScript / Python / Java] 最佳实践
对每个问题给出：问题描述、风险等级（高/中/低）、改进建议。
```

#### 修复 Bug

```
以下代码在 [具体场景] 下出现了 [错误信息或异常行为]。

期望行为：[描述]
实际行为：[描述]
已尝试的方案：[描述，可选]

请：
1. 分析根本原因
2. 给出修复方案
3. 说明如何避免类似问题
```

#### 生成单元测试

```
为以下 [函数/类/模块] 编写单元测试，使用 [Jest/Vitest/PyTest/JUnit]。
需要覆盖：
  - 正常流程：[描述]
  - 边界情况：空值、极值、类型错误
  - 异常情况：[网络错误/权限不足等]
测试风格参考项目中已有的 [xxx.test.ts] 文件。
```

#### 生成文档

```
为以下代码生成 [JSDoc / Python docstring / JavaDoc] 风格的文档注释，包括：
- 函数描述（一句话）
- 每个参数的名称、类型、描述
- 返回值类型和描述
- 至少一个使用示例
- 可能抛出的异常（如有）
```

#### 代码重构

```
重构以下代码，目标：
- [提高可读性 / 减少重复 / 改善性能]
- 保持接口不变（不改变函数签名和返回值）
- 不引入新的外部依赖
重构后说明做了哪些改动以及原因。
```

### 5.3 上下文提供技巧

| 技巧 | 说明 | 示例 |
|------|------|------|
| **打开相关文件** | Copilot 会读取已打开的文件作为上下文 | 同时打开接口定义 `.d.ts`、类型文件 |
| **引用具体文件** | 在 Chat 中用 `#file:` 精确引用 | `#file:src/types/user.ts` |
| **提供输入输出示例** | 用具体数据说明期望行为 | `输入 [1,3,2] → 输出 [1,2,3]` |
| **说明技术栈版本** | 避免生成过时 API | `使用 React 18 的 useTransition` |
| **拆分复杂问题** | 一次一个子任务，避免一次要求太多 | 先生成骨架，再补充细节 |
| **给出错误上下文** | 粘贴完整错误堆栈 | 粘贴 `TypeError: Cannot read...` |
| **说明已有约束** | 避免建议引入不允许的依赖 | `项目不使用 lodash，请用原生实现` |

### 5.4 迭代优化提示词

当 Copilot 生成的结果不理想时，不要重新开始，而是在对话中追加：

```
上面的实现有个问题：[描述具体问题]，请修改。

另外，请同时：[补充之前遗漏的需求]
```

**示例对话流程：**

```
你：用 React 实现一个分页组件，支持上一页/下一页按钮

Copilot：[生成基础实现]

你：好的，但请追加以下功能：
    1. 支持直接跳转到指定页码
    2. 显示"第 X 页 / 共 Y 页"
    3. 第一页时禁用上一页按钮，最后一页时禁用下一页按钮

Copilot：[生成更完整的实现]
```

---

## 6. 典型场景示例

### 6.1 写新功能：带防抖的搜索输入组件

**目标：** 实现一个 React 搜索框，输入停止 300ms 后触发搜索，搜索中显示 loading 状态。

**步骤 1：** 在文件顶部写注释描述需求，触发 Copilot 生成组件骨架。

**步骤 2：** 接受并完善实现：

```tsx
import React, { useState, useEffect, useRef } from 'react';

interface SearchInputProps {
  onSearch: (query: string) => void;
  debounceMs?: number;
  placeholder?: string;
}

const SearchInput: React.FC<SearchInputProps> = ({
  onSearch,
  debounceMs = 300,
  placeholder = '请输入搜索关键词...',
}) => {
  const [value, setValue] = useState('');
  const [loading, setLoading] = useState(false);
  const timerRef = useRef<ReturnType<typeof setTimeout> | null>(null);

  useEffect(() => {
    return () => {
      if (timerRef.current) clearTimeout(timerRef.current);
    };
  }, []);

  const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
    const newValue = e.target.value;
    setValue(newValue);
    setLoading(true);

    if (timerRef.current) clearTimeout(timerRef.current);
    timerRef.current = setTimeout(() => {
      onSearch(newValue);
      setLoading(false);
    }, debounceMs);
  };

  return (
    <div style={{ position: 'relative', display: 'inline-block' }}>
      <input
        type="text"
        value={value}
        onChange={handleChange}
        placeholder={placeholder}
        style={{ paddingRight: loading ? '24px' : '8px' }}
      />
      {loading && (
        <span style={{ position: 'absolute', right: '8px', top: '50%', transform: 'translateY(-50%)' }}>
          ⏳
        </span>
      )}
    </div>
  );
};

export default SearchInput;
```

**步骤 3：** 通过 Inline Chat（`Ctrl+I`）追加需求，如"添加清空按钮"，Copilot 会在现有代码基础上做差量修改。

### 6.2 写单元测试：为工具函数生成完整测试

**目标：** 为日期格式化函数生成覆盖边界情况的测试。

**步骤 1：** 打开函数文件，选中函数，在 Chat 输入 `/tests`。

**步骤 2：** Copilot 生成如下测试（以 Vitest 为例）：

```typescript
// src/utils/formatDate.test.ts
import { describe, it, expect } from 'vitest';
import { formatDate } from './formatDate';

describe('formatDate', () => {
  it('应格式化正常日期', () => {
    expect(formatDate(new Date('2024-03-15'))).toBe('2024-03-15');
  });

  it('应处理月份和日期的前导零', () => {
    expect(formatDate(new Date('2024-01-05'))).toBe('2024-01-05');
  });

  it('传入无效日期应返回空字符串', () => {
    expect(formatDate(new Date('invalid'))).toBe('');
  });

  it('传入 null 应返回空字符串', () => {
    expect(formatDate(null as unknown as Date)).toBe('');
  });

  it('应正确处理闰年 2 月 29 日', () => {
    expect(formatDate(new Date('2024-02-29'))).toBe('2024-02-29');
  });

  it('应支持自定义分隔符', () => {
    expect(formatDate(new Date('2024-03-15'), '/')).toBe('2024/03/15');
  });

  it('应处理年份边界：公元 1 年', () => {
    const date = new Date('0001-01-01T00:00:00Z');
    expect(formatDate(date)).toMatch(/^\d{4}-\d{2}-\d{2}$/);
  });
});
```

**步骤 3：** 检查测试用例，手工补充业务特有的场景（如时区处理），然后运行 `npm run test` 确认全部通过。

### 6.3 修复 Bug：处理竞态条件

**目标：** 修复搜索接口因快速连续触发导致结果乱序的问题。

**操作：** 选中问题代码，Inline Chat 输入"这个异步请求存在竞态条件，快速连续调用时旧请求的响应会覆盖新结果，请修复"。

```typescript
// 修复前（存在竞态条件）
async function searchUsers(query: string) {
  const result = await api.search(query);
  setResults(result.data); // 旧请求可能在新请求之后返回，覆盖正确结果
}

// Copilot 修复后（使用 AbortController 取消旧请求）
const abortControllerRef = useRef<AbortController | null>(null);

async function searchUsers(query: string) {
  // 取消上一次未完成的请求
  if (abortControllerRef.current) {
    abortControllerRef.current.abort();
  }
  abortControllerRef.current = new AbortController();

  try {
    const result = await api.search(query, {
      signal: abortControllerRef.current.signal,
    });
    setResults(result.data);
  } catch (err) {
    if ((err as Error).name === 'AbortError') {
      // 请求被主动取消，忽略
      return;
    }
    setError(err as Error);
  }
}

// 组件卸载时清理
useEffect(() => {
  return () => abortControllerRef.current?.abort();
}, []);
```

### 6.4 编写文档：批量生成 JSDoc

**目标：** 为工具模块中的所有公共函数添加文档注释。

**操作：** 选中函数，执行 `/doc`，Copilot 生成标准 JSDoc：

```typescript
/**
 * 将字节数格式化为人类可读的文件大小字符串。
 *
 * @param bytes - 文件大小（字节），必须为非负整数
 * @param decimals - 小数位数，默认为 2，范围 0-10
 * @returns 格式化后的大小字符串，如 `"1.46 KB"`、`"2.30 MB"`
 * @throws {RangeError} 当 `decimals` 超出 0-10 范围时抛出
 *
 * @example
 * formatBytes(0)        // => "0 Bytes"
 * formatBytes(1024)     // => "1.00 KB"
 * formatBytes(1536, 1)  // => "1.5 KB"
 * formatBytes(1073741824) // => "1.00 GB"
 */
function formatBytes(bytes: number, decimals = 2): string {
  if (bytes === 0) return '0 Bytes';
  if (decimals < 0 || decimals > 10) throw new RangeError('decimals must be between 0 and 10');

  const k = 1024;
  const sizes = ['Bytes', 'KB', 'MB', 'GB', 'TB', 'PB'];
  const i = Math.floor(Math.log(bytes) / Math.log(k));
  return `${parseFloat((bytes / Math.pow(k, i)).toFixed(decimals))} ${sizes[i]}`;
}
```

### 6.5 集成第三方 API

**目标：** 用 Copilot 快速接入 GitHub REST API，获取仓库 Issue 列表。

```typescript
// 在 Chat 中输入：
// 用 fetch 调用 GitHub API 获取仓库的 Issue 列表，
// 支持分页（page, per_page），需要传入 token 认证，返回类型使用 TypeScript 接口定义

interface GitHubIssue {
  id: number;
  number: number;
  title: string;
  state: 'open' | 'closed';
  user: { login: string; avatar_url: string };
  created_at: string;
  updated_at: string;
  html_url: string;
}

interface FetchIssuesOptions {
  owner: string;
  repo: string;
  token: string;
  page?: number;
  perPage?: number;
  state?: 'open' | 'closed' | 'all';
}

async function fetchIssues(options: FetchIssuesOptions): Promise<GitHubIssue[]> {
  const { owner, repo, token, page = 1, perPage = 30, state = 'open' } = options;

  const url = new URL(`https://api.github.com/repos/${owner}/${repo}/issues`);
  url.searchParams.set('page', String(page));
  url.searchParams.set('per_page', String(perPage));
  url.searchParams.set('state', state);

  const response = await fetch(url.toString(), {
    headers: {
      Authorization: `Bearer ${token}`,
      Accept: 'application/vnd.github.v3+json',
    },
  });

  if (!response.ok) {
    throw new Error(`GitHub API error: ${response.status} ${response.statusText}`);
  }

  return response.json() as Promise<GitHubIssue[]>;
}
```

---

## 7. 质量与安全实践

### 7.1 代码审查原则

Copilot 生成的代码**必须**经过人工审查后才能合入主分支。审查时按以下 Checklist 逐项检查：

**功能正确性**
- [ ] 逻辑是否符合需求，边界情况（空值、极值、并发）是否处理
- [ ] 返回值类型和格式是否与接口约定一致
- [ ] 异常路径（网络错误、超时、鉴权失败）是否有合理的处理

**性能**
- [ ] 是否存在 N+1 查询或循环中的重复 API 调用
- [ ] 大数据集处理是否使用分页、流式或懒加载
- [ ] 是否有不必要的深拷贝或重复计算

**安全**
- [ ] 用户输入是否经过校验和转义（防 XSS、SQL 注入）
- [ ] 敏感信息（密钥、Token）是否写入代码或日志
- [ ] 权限校验逻辑是否在服务端执行（不依赖前端判断）

**代码质量**
- [ ] 命名是否清晰，是否有魔法数字
- [ ] 代码风格是否符合项目 ESLint/Prettier 规范
- [ ] 是否引入了不必要的新依赖

### 7.2 测试验证流程

```
1. 接受 Copilot 建议
        ↓
2. 运行现有测试套件（确保无回归）
   npm test / pytest / mvn test
        ↓
3. 运行新生成的测试（确认测试有意义）
        ↓
4. 检查测试覆盖率（核心分支 > 80%）
   npm run test:coverage
        ↓
5. 手动测试关键路径（不能完全依赖自动化测试）
```

**测试覆盖率参考命令：**

```bash
# JavaScript/TypeScript（Vitest）
npx vitest run --coverage

# Python
pytest --cov=src --cov-report=html

# Java（Maven）
mvn jacoco:report
```

### 7.3 敏感信息防护

**绝对不要**将以下内容粘贴到 Copilot Chat 或让其出现在代码中：

| 类型 | 示例 | 正确做法 |
|------|------|----------|
| API 密钥 | `sk-abc123...` | 使用环境变量 `process.env.OPENAI_API_KEY` |
| 数据库密码 | `password=Abc@123` | 使用密钥管理服务（Vault、AWS Secrets Manager） |
| 用户个人数据 | 真实姓名、身份证号 | 使用脱敏数据（`张**`、`1**0`） |
| 私钥/证书 | `-----BEGIN RSA PRIVATE KEY-----` | 存储在安全的密钥存储中 |
| 内部 IP/域名 | `192.168.1.x`、`internal.corp.com` | 使用占位符 `<internal-host>` |

**`.env` 文件规范：**

```bash
# .env.example（提交到版本控制，用于说明所需变量）
DATABASE_URL=postgres://user:password@host:5432/dbname
API_KEY=your-api-key-here

# .env（本地实际值，加入 .gitignore）
DATABASE_URL=postgres://admin:secret@localhost:5432/myapp
API_KEY=sk-realkey123

# .gitignore 中确保包含：
.env
.env.local
.env.production
```

### 7.4 安全漏洞检查

对安全敏感的代码，在 Copilot Chat 中进行安全审查：

```
请以安全工程师的角度审查以下代码，检查是否存在：
1. SQL 注入（字符串拼接 SQL）
2. XSS（未转义的用户输入直接插入 DOM）
3. CSRF（状态变更接口缺少 Token 校验）
4. 路径遍历（文件路径未校验）
5. 不安全的反序列化

对每个发现的问题，给出漏洞等级（高/中/低）和修复代码。
```

**高风险代码模式检测（提示词）：**

```typescript
// 示例：让 Copilot 检查 SQL 拼接风险
// 在 Chat 中选中以下代码后输入 "/fix 检查 SQL 注入风险"

// ❌ 危险
const query = `SELECT * FROM users WHERE name = '${userName}'`;

// ✅ 安全（参数化查询）
const query = 'SELECT * FROM users WHERE name = $1';
const result = await db.query(query, [userName]);
```

### 7.5 依赖安全

当 Copilot 建议引入新的 npm/pip 包时，使用以下命令检查已知漏洞：

```bash
# npm
npm audit

# yarn
yarn audit

# Python
pip-audit

# 查看某个包的漏洞信息
npm audit --json | jq '.vulnerabilities'
```

---

## 8. 团队协作规范

### 8.1 使用边界约定

在项目 `CONTRIBUTING.md` 或 `docs/ai-usage-policy.md` 中明确 Copilot 的使用范围：

| 场景 | 推荐策略 |
|------|----------|
| 样板代码、CRUD 生成 | ✅ 推荐使用 |
| 单元测试、文档注释 | ✅ 推荐使用 |
| 算法核心逻辑 | ⚠️ 辅助使用，需仔细审查 |
| 鉴权、加密实现 | ⚠️ 仅用于参考，必须安全审查 |
| 数据库迁移脚本 | ⚠️ 生成后人工逐行核查 |
| 架构设计决策 | ❌ 不依赖 Copilot |
| 生产数据处理脚本 | ❌ 禁止直接使用，需全面测试 |

### 8.2 自定义团队指令（Copilot Instructions）

在仓库根目录创建 `.github/copilot-instructions.md`，Copilot 会自动读取此文件作为所有对话的系统提示，从而遵循团队规范：

```markdown
<!-- .github/copilot-instructions.md -->

# 项目编码规范

## 技术栈
- 前端：React 18 + TypeScript 5 + Vite
- 状态管理：Zustand（不使用 Redux）
- 样式：CSS Modules + Tailwind CSS
- 测试：Vitest + Testing Library
- 代码规范：ESLint（@antfu/eslint-config）+ Prettier

## 命名规范
- 组件文件：PascalCase（`UserCard.tsx`）
- 工具函数：camelCase（`formatDate.ts`）
- 类型/接口：以大写字母开头，不加 `I` 前缀（`User`，不是 `IUser`）
- 常量：SCREAMING_SNAKE_CASE（`MAX_RETRY_COUNT`）

## 代码风格
- 使用函数组件和 Hooks，不使用 Class 组件
- 导入顺序：Node 内置 → 第三方库 → 内部模块 → 类型
- 所有异步函数使用 async/await，不使用 .then()/.catch() 链
- 错误处理：使用 try/catch，不吞掉错误

## 测试规范
- 测试文件与源文件同目录，命名为 `xxx.test.ts`
- 使用 `describe` 分组，`it` 描述具体行为（用"应..."开头）
- Mock 外部依赖，不调用真实 API
```

### 8.3 代码风格一致性

确保 Copilot 生成的代码通过自动检查：

```bash
# 提交前自动 lint 和格式化（通过 husky + lint-staged）
# package.json
{
  "lint-staged": {
    "*.{ts,tsx}": ["eslint --fix", "prettier --write"],
    "*.{css,md}": ["prettier --write"]
  }
}
```

在 Copilot Chat 中提问时主动引用规范：

```
按照 #file:.github/copilot-instructions.md 中的规范，
重构以下组件，确保符合 ESLint 规则和命名约定。
```

### 8.4 PR 流程建议

**PR 模板中添加 AI 辅助声明（可选）：**

```markdown
<!-- .github/PULL_REQUEST_TEMPLATE.md 中添加 -->

## AI 辅助声明（可选）
- [ ] 本 PR 的部分代码使用了 GitHub Copilot 辅助生成
- [ ] 所有 AI 生成的代码已经过人工审查和测试验证
```

**Reviewer 注意事项：**
- AI 生成的代码同样需要严格 Review，不因"AI 写的"而降低标准
- 重点关注：边界条件、错误处理、安全漏洞、与现有代码的一致性
- 对于复杂逻辑，要求 PR 作者解释代码意图，而非仅提交代码

**提交粒度建议：**

```bash
# ✅ 好：小粒度提交，便于追溯
git commit -m "feat: add debounce hook"
git commit -m "test: add tests for useDebounce"
git commit -m "docs: add JSDoc for useDebounce"

# ❌ 差：一次提交大量 AI 生成的代码
git commit -m "add lots of stuff with copilot"
```

### 8.5 知识产权与合规

- **数据隐私**：GitHub Copilot for Business/Enterprise 默认不将用户代码用于模型训练（可在组织设置中确认）
- **版权合规**：Copilot 提供"引用来源匹配"功能，可过滤与开源代码相似度过高的建议（`Settings → Copilot → Suggestions matching public code`）
- **开源项目**：对于开源贡献，了解目标项目对 AI 生成代码的接受政策（部分项目要求声明）
- **内部政策**：遵循公司的 AI 工具使用政策，使用 Enterprise 版本确保代码不离开组织边界

---

## 9. 常见问题与排错

### 9.1 没有代码建议

**诊断与解决：**

| 症状 | 可能原因 | 解决方案 |
|------|----------|----------|
| 状态栏图标有红色斜线 | 插件未登录或登录失效 | 点击图标 → `Sign in to GitHub`，重新授权 |
| 图标正常但无建议 | 当前文件类型被禁用 | `Settings → Extensions → GitHub Copilot` 确认语言已启用 |
| 订阅相关提示 | 订阅已过期或未激活 | 访问 `github.com/settings/billing` 检查订阅状态 |
| 网络超时 | 代理或防火墙拦截 | 参见 [9.4 代理配置](#94-公司网络代理问题) |
| 插件崩溃 | 版本兼容问题 | 更新插件至最新版，或降级 VS Code |
| 组织策略限制 | 管理员未开启权限 | 联系 GitHub 组织管理员（参见 [9.5](#95-权限被组织禁用)） |

**快速自检步骤：**

```bash
# 1. 检查 VS Code 扩展状态
# 扩展面板 → 搜索 "GitHub Copilot" → 确认已启用（非灰色）

# 2. 查看 Copilot 日志
# View → Output → 下拉选择 "GitHub Copilot"
# 查找 "error" 或 "unauthorized" 关键字

# 3. 重新加载窗口
# Ctrl+Shift+P → Developer: Reload Window
```

### 9.2 建议质量差

**提升质量的方法（按优先级）：**

1. **丰富上下文**：同时打开类型定义文件、相关模块、已有的类似实现
2. **优化注释**：将模糊的注释改为具体描述（输入输出、约束条件）
3. **多看候选项**：按 `Ctrl+Enter` 打开建议面板，从多个选项中选最优
4. **切换到 Chat**：对于复杂需求，用对话方式比内联补全效果更好
5. **提供示例**：在注释中写出期望的输入输出示例
6. **拆分任务**：复杂功能拆成多个小函数，逐个生成

```typescript
// ❌ 差的注释（太模糊）
// 处理用户数据

// ✅ 好的注释（具体）
// 将后端返回的用户列表（UserResponse[]）转换为前端显示格式（UserViewModel[]）
// 过滤掉 status 为 'deleted' 的用户，并将 created_at 转换为 'YYYY-MM-DD' 格式
```

### 9.3 Copilot Chat 无响应或报错

**排查步骤：**

```bash
# 步骤 1：确认能访问 GitHub API
curl -I https://api.github.com
# 期望：HTTP/2 200 或 301

# 步骤 2：确认 Copilot 服务可达
curl -I https://copilot-proxy.githubusercontent.com
# 期望：HTTP/2 200（不能有 connection refused）

# 步骤 3：查看 VS Code 输出日志
# View → Output → "GitHub Copilot Chat"
# 查找具体错误信息

# 步骤 4：退出登录并重新登录
# Ctrl+Shift+P → "GitHub Copilot: Sign Out"
# 等待 30 秒后重新 Sign In

# 步骤 5：完全重启 VS Code（非 Reload Window）
```

**常见错误信息解读：**

| 错误信息 | 含义 | 解决方案 |
|----------|------|----------|
| `401 Unauthorized` | Token 过期或权限不足 | 重新登录 GitHub |
| `403 Forbidden` | 组织策略限制 | 联系管理员开启权限 |
| `429 Too Many Requests` | 请求频率超限 | 等待几分钟后重试 |
| `Network Error` | 网络不通 | 检查代理和防火墙设置 |
| `context_length_exceeded` | 对话上下文过长 | 开启新的 Chat 会话 |

### 9.4 公司网络/代理问题

**VS Code `settings.json` 代理配置：**

```json
{
  "http.proxy": "http://your-proxy-server:port",
  "http.proxyStrictSSL": false,
  "http.proxyAuthorization": null,
  "github.copilot.advanced": {
    "debug.overrideProxyUrl": "http://your-proxy-server:port",
    "debug.testOverrideProxyUrl": "http://your-proxy-server:port"
  }
}
```

**需要在防火墙/代理白名单中允许的域名：**

```
github.com
api.github.com
copilot-proxy.githubusercontent.com
default.exp-tas.com
```

**使用系统代理（macOS/Linux）：**

```bash
# 在终端中设置，然后从终端启动 VS Code
export HTTPS_PROXY=http://proxy-server:port
export HTTP_PROXY=http://proxy-server:port
code .
```

### 9.5 权限被组织禁用

当账号属于 GitHub 组织且管理员未开启 Copilot 权限时：

**员工操作：**
1. 确认账号所属组织（`github.com/settings/organizations`）
2. 联系组织管理员，请其在以下位置开启权限：
   - `Organization Settings → Copilot → Access → Enabled for: All members / Selected members`

**管理员操作：**
1. 进入组织设置 → `Copilot → Policies`
2. 选择 `Enabled for all members` 或按团队分配
3. 配置内容排除规则（如屏蔽特定文件的建议）：
   ```
   # 排除所有 .env 文件
   **/.env*
   # 排除 secrets 目录
   **/secrets/**
   ```

### 9.6 JetBrains 特有问题

```
问题：建议延迟高或不出现
解决：
1. Help → Find Action → "GitHub Copilot: Enable/Disable"，确保已启用
2. 检查 IDE 内存设置：Help → Change Memory Settings → 提高到 2048MB 以上
3. 清除缓存：File → Invalidate Caches → Invalidate and Restart
```

---

## 10. 进阶能力与最佳实践

### 10.1 多文件改动（Copilot Edits）

Copilot Edits 允许你用自然语言描述跨文件的改动目标，Copilot 会同时修改多个文件并展示 diff。

**使用步骤：**

1. 在 VS Code 侧边栏点击 Copilot 图标，切换到 **Edits** 标签页
2. 点击 `+ Add Files` 将相关文件加入工作集（建议不超过 10 个文件）
3. 在输入框描述改动目标，回车执行
4. 逐文件审查 diff，点击 `Accept` 接受或 `Discard` 放弃某文件的修改
5. 点击 `Accept All` 一次性接受全部修改

**实际示例：将 moment.js 迁移至 dayjs**

```
工作集：
  src/utils/date.ts
  src/components/DatePicker/index.tsx
  src/components/Timeline/index.tsx
  package.json

提示词：
将工作集中所有使用 moment.js 的地方替换为 dayjs。
- 更新 import 语句：import dayjs from 'dayjs'
- dayjs 对象不可变，链式调用无需变动
- 格式化 token 基本兼容，注意 DD 表示月中日期（dayjs 与 moment 相同）
- 从 package.json 中移除 moment，添加 dayjs
```

### 10.2 Agent 模式（自动化任务执行）

Copilot Agent 模式可以自主执行多步骤任务：读取文件、运行命令、修改代码、运行测试，形成自动化循环。

**启用方式（VS Code）：**

在 Chat 输入框的模式选择器中切换为 `Agent`（或在提示词中@agent）。

**适合 Agent 模式的任务：**

```
# 示例 1：自动化代码迁移
将项目中所有的 class 组件迁移为函数组件和 Hooks，
完成后运行测试确保无回归，如果测试失败请自动修复。

# 示例 2：自动化添加日志
为 src/services/ 目录下所有公共方法添加结构化日志（使用 logger 模块），
包含：方法名、入参摘要、执行时长、异常信息。

# 示例 3：自动化创建 CRUD
在 src/features/product/ 目录创建完整的产品管理模块，
包括：API 服务层、Zustand store、列表页面、详情页面和对应的测试文件。
参考 src/features/user/ 目录的结构和风格。
```

> ⚠️ Agent 模式会自动执行命令，建议在使用前确认工作区已提交到 Git，以便回滚。

### 10.3 任务拆解策略

面对复杂任务时，推荐以下工作流：

**第一步：规划**

```
在 Copilot Chat 输入：
"我需要实现 [功能]，请列出实现步骤，每步说明要做什么、涉及哪些文件，
不要生成代码，只给出实现计划。"
```

**第二步：逐步实现**

```
步骤1完成后，提交 Git → 继续步骤2
每完成一个步骤：
  1. 运行测试，确认无回归
  2. git add . && git commit -m "feat: [步骤描述]"
  3. 继续下一步
```

**第三步：测试驱动（TDD）**

```
1. 先让 Copilot 生成测试（描述预期行为）
2. 运行测试，确认全部失败（Red）
3. 让 Copilot 生成实现代码
4. 运行测试，修复直到全部通过（Green）
5. 用 Copilot 协助重构（Refactor）
```

### 10.4 效率提升清单

将以下习惯融入日常开发工作流：

**编码阶段**
- [ ] 写代码前先用注释描述意图，让 Copilot 辅助生成
- [ ] 利用 `Ctrl+Enter` 查看多个候选建议，选择最优
- [ ] 对复杂逻辑使用 Inline Chat 而非反复修改注释

**测试阶段**
- [ ] 完成功能后立即用 `/tests` 生成测试框架
- [ ] 检查生成的测试是否覆盖了边界情况，手工补充
- [ ] 使用 Copilot Chat 解释不理解的测试逻辑

**Review 阶段**
- [ ] 提交 PR 前用 Copilot Chat 进行自审（安全、性能、可读性）
- [ ] 利用 `#problems` 变量让 Copilot 解释编辑器报错

**文档阶段**
- [ ] 新功能完成后用 `/doc` 批量生成文档注释
- [ ] 用 Copilot Chat 辅助更新 README 和 CHANGELOG

**学习阶段**
- [ ] 遇到陌生代码用 `/explain` 快速理解
- [ ] 让 Copilot 解释第三方库的用法（"如何使用 Zod 校验嵌套对象"）
- [ ] 定期更新 Copilot 插件，使用最新模型能力

### 10.5 ROI 评估与效果追踪

帮助团队量化 Copilot 带来的价值：

| 指标 | 测量方法 | 参考基准 |
|------|----------|----------|
| 代码接受率 | VS Code Copilot 使用统计 | 行业平均 ~30% |
| 功能交付速度 | Story Point 完成效率 | 提升 20-40%（因场景而异） |
| 单元测试覆盖率 | `npm run test:coverage` | 目标 > 80% |
| Code Review 时长 | PR 开启到合并的时间 | 建立基线后对比 |

**VS Code 使用数据查看：**
- `Ctrl+Shift+P` → `GitHub Copilot: Open Completions Usage`
- 或访问 `github.com/settings/copilot` 查看使用统计

### 10.6 与其他 AI 工具配合

| 场景 | 推荐工具 |
|------|----------|
| 日常代码补全 | GitHub Copilot（内联建议） |
| 复杂问题分析、架构讨论 | Copilot Chat |
| 大范围跨文件重构 | Copilot Edits |
| 全自动任务执行 | Copilot Agent 模式 |
| PR 代码审查 | GitHub Copilot Code Review（github.com） |
| 代码搜索与理解 | GitHub Copilot 代码搜索（`@github` in Chat） |

### 10.7 持续学习资源

- 📖 [GitHub Copilot 官方文档](https://docs.github.com/copilot)
- 📝 [Copilot 提示词工程最佳实践](https://github.blog/developer-skills/github/how-to-use-github-copilot-in-your-ide-tips-tricks-and-best-practices/)
- 🔔 [GitHub Copilot 更新日志](https://github.blog/changelog/label/copilot/)
- 🎓 [GitHub Skills：使用 Copilot 编写代码](https://skills.github.com/)
- 💬 [GitHub Community Discussions - Copilot](https://github.com/orgs/community/discussions/categories/copilot)

---

> **免责声明：** GitHub Copilot 生成的代码仅供参考，开发者需对最终代码质量负责。在生产环境部署前，请务必进行完整的测试和安全审查。生成代码中涉及的第三方库版本以官方文档为准。
