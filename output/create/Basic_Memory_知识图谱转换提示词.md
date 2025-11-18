---
title: Basic_Memory_知识图谱转换提示词
type: note
permalink: output/create/basic-memory-知识图谱转换提示词
---

# 认知中心 Basic Memory 自动知识图谱转换系统

## 🎯 系统目标
自动将输入文本转换为结构化的知识图谱，存储为 Markdown 文件，维护实体间的关系。

## 🔧 核心功能

### 1. 内容分析与实体提取
```
任务：分析输入文本并提取
- 🔍 核心概念/实体
- 🔗 概念间关系
- 🏷️ 相关性标签
- 📁 建议存储位置
```

### 2. 检测的关系类型
- `implements` - 实现关系
- `requires` - 依赖关系  
- `relates_to` - 一般关联
- `part_of` - 层级关系
- `extends` - 扩展关系
- `pairs_with` - 配对关系

### 3. 观察分类自动标记
- `[decision]` - 决策记录
- `[requirement]` - 需求说明
- `[technique]` - 技术方法
- `[issue]` - 问题识别
- `[observation]` - 一般观察

## 📝 转换流程

### 步骤1：初步内容分析
```
分析输入："{{输入内容}}"

提取清单：
1. 主要实体（2-5个）：_________
2. 核心关系：_________
3. 适用文件目录：/output/zettelkasten/ 或 /output/create/
4. 建议文件名：_________
```

### 步骤2：创建实体笔记
```yaml
---
title: "实体名称"
created: {{当前时间}}
tags: [核心标签, 次要标签]
type: entity  
status: active
aliases: ["别名1", "别名2"]
---

# 实体名称

## 基本信息
- **类型**: concept/system/person/etc
- **领域**: 所属知识领域
- **重要性**: 高/中/低

## 描述
{{实体描述}}

## 相关实体
- [[memory://related-entity-1|相关实体1]] - implements
- [[memory://related-entity-2|相关实体2]] - requires
```

### 步骤3：建立关系映射
```yaml
---
title: "关系映射: {{源实体}} → {{目标实体}}"
created: {{当前时间}}
tags: [relationship, mapping]
source: "{{源实体}}"
target: "{{目标实体}}"  
relation_type: "{{关系类型}}"
---

# 关系分析

## 源实体
[[memory://{{源实体路径}}|{{源实体名称}}]]

## 目标实体  
[[memory://{{目标实体路径}}|{{目标实体名称}}]]

## 关系类型
`{{关系类型}}`

## 关系描述
{{详细描述两个实体间的具体关系}}

## 影响评估
- **重要性**: ___________
- **复杂度**: ___________  
- **维护需求**: ___________
```

### 步骤4：观察记录分类
```yaml
---
title: "{{观察标题}}"
created: {{当前时间}}
tags: [observation, {{具体分类}}]
observation_type: "{{decision|requirement|technique|issue}}"
context: "{{应用背景}}"
---

# 观察记录

## 分类标记
[{{observation_type}}] {{核心内容}}

## 上下文背景
{{详细背景描述}}

## 应用建议  
{{如何将这个观察应用到实践中}}

## 相关实体
{{连接到相关的实体笔记}}
```

## 🚀 使用示例

### 输入示例
"我们决定采用 JWT 令牌实现无状态认证系统，需要在用户表中添加刷新令牌字段。"

### 输出结构
1. **实体文件**: `/output/zettelkasten/JWT认证系统.md`
2. **决策记录**: `/output/create/auth_decision_2025.md`
3. **关系映射**: `/output/zettelkasten/关系映射_JWT-用户表.md`

### 自动化处理
```
检测模式：
✓ "决定采用" → [decision] 标记 + implements 关系
✓ "需要" → [requirement] 标记
✓ "添加字段" → 数据库操作标记
✓ "无状态认证" → 技术特征提取
```

## 📁 文件组织

### 主要目录
- `/output/zettelkasten/` - 原子化知识笔记
- `/output/create/` - 创作性和决策性内容  
- `/output/BASE/` - 数据库和系统性知识

### 命名规范
- 实体文件：`概念名称.md`
- 关系文件：`关系映射_源-目标.md`
- 观察记录：`观察类型_主题_日期.md`

## 🔄 质量检查

### 自动验证
- ✅ WikiLink 语法正确性
- ✅ YAML Frontmatter 完整性
- ✅ 关系双向确认
- ✅ 文件路径存在性

### 知识完整性
- 📊 实体覆盖率
- 🔗 关系密度
- 🏷️ 标签一致性
- 📈 知识网络连通性

---
*创建时间: 2025-11-19*
*文件路径: /output/create/Basic_Memory_知识图谱转换提示词.md*