# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is an **Obsidian knowledge management vault** integrated with **Basic Memory** knowledge graph system. The repository uses Zettelkasten methodology for atomic note-taking and includes comprehensive knowledge management automation through Basic Memory MCP integration.

## Technical Architecture

### Core Systems Integration
- **Obsidian Vault**: Primary knowledge management interface with zettelkasten methodology
- **Basic Memory**: Knowledge graph system providing semantic relationships and memory:// URLs
- **Claude Code**: AI assistant for automated knowledge processing and content generation
- **MCP Integration**: Secure API-based knowledge operations with Basic Memory

### Directory Structure and Purpose
```
/output/
├── zettelkasten/    # Atomic knowledge notes (tech entities, core concepts)
├── create/         # Generated content, decisions, and knowledge workflows
├── template/       # Standardized note templates
└── BASE/          # Database views and systematic knowledge management

/.claude/           # Claude Code environment configuration
/.obsidian/         # Obsidian vault configuration and plugins
```

## Key Systems Integration

### Basic Memory Knowledge Graph
- **Project**: "认知中心" (Cognitive Center)
- **Standards**: Full Basic Memory 2.0 spec compliance
- **Memory URLs**: Support for memory:// scheme and pattern matching
- **Knowledge Types**: entity, decision, process, note with standardized frontmatter
- **Relations**: implements, depends_on, requires, relates_to, extends, pairs_with
- **Observations**: [tech], [design], [decision], [issue], [method], [principle]

### Automation Capabilities
```bash
# Knowledge graph operations
list_memory_projects        # View BASIC Memory projects
create_memory_project       # Initialize new knowledge projects
write_note & edit_note      # Create/manage knowledge documents
view_note                   # Retrieve knowledge with relations

# File search and management
fd "search-term" -e md      # Search markdown files by name
rg "content" --type md      # Search within markdown content
rg -i "keyword" --type md   # Case-insensitive search
```

## Development Standards

### Note Creation Process
1. **Select appropriate template** from `/output/template/`
2. **Follow Basic Memory frontmatter standards**:
   ```yaml
   ---
   title: "文档标题"
   type: entity | decision | process | note
   tags: [分类, 技术, 状态]
   permalink: unique-identifier
   status: active | draft | deprecated
   aliases: ["别名1", "别名2"]
   ---
   ```
3. **Structure content with standard sections**:
   - Main content using markdown
   - `## Relations` for knowledge graph connections
   - `## Observations` for categorized insights
4. **Ensure valid memory:// URLs** before creating cross-references

### Knowledge Graph Standards
```markdown
## Relations (standard format)
- implements [[技术概念]]
- depends_on [[系统依赖]]
- relates_to [[相关概念]]
- extends [[扩展知识]]
- pairs_with [[配套技术]]

## Observations (categorized)
- [tech] 技术实现细节 #tag (上下文说明)
- [design] 架构设计决策 #tag (选择依据)
- [decision] 关键决策点 #tag (理由分析)
- [issue] 问题和限制 #tag (影响评估)
```

## Common Development Tasks

### Knowledge Processing
```bash
# Auto-convert technical content to knowledge graph
"分析并转换为标准 Basic Memory 格式：[技术内容]"

# Create standardized entities
"按实体模板创建：[技术名称] - 类型:entity - 分类:[领域]"

# Establish knowledge relationships
"建立关系：[源实体] → [关系类型] → [目标实体]"

# Generate systematic knowledge databases
"为 [主题] 创建 BASE 数据库，包含 [属性1]、[属性2] 视图"
```

### Content Management
```bash
# Search before creating links (critical step)
fd "目标文档" -e md    # Verify document exists
rg "搜索关键词"       # Check content relevance

# Validate knowledge graph consistency
grep -r "memory://" --include="*.md" .  # Check URL references
grep -r "\[\[" --include="*.md" .       # Verify wiki-links
```

## Testing and Validation

### Knowledge Graph Integrity
- Verify all memory:// URLs reference existing content
- Ensure bidirectional relationships are established when meaningful
- Validate frontmatter completeness and consistency
- Check for orphaned knowledge nodes and broken connections

### Content Quality Standards
- Maintain atomicity: one concept per note
- Use consistent categorization (type, tags, status)
- Provide meaningful cross-references through Relations
- Include context and reasoning in Observations
- Prefer specific technical terms over general descriptions

## Important Configuration

### Basic Memory Integration
```json
// .claude/settings.local.json 权限配置
{
  "permissions": {
    "allow": [
      "mcp__basic-memory__list_memory_projects",
      "mcp__basic-memory__create_memory_project",
      "mcp__basic-memory__write_note",
      "mcp__basic-memory__edit_note",
      "mcp__basic-memory__view_note"
    ]
  }
}
```

### Obsidian Plugins
- **Core Plugins**: 文件浏览器, 全局搜索, 反向链接, 模板, 属性等
- **Community Plugins**: Copilot (AI辅助), calendar (日历视图)

## Error Handling

### Common Issues
1. **文档链接不存在**: 使用 fd/rg 搜索确认文档存在性
2. **UTF-8字符问题**: 注意多字节字符编码兼容性
3. **关系建立失败**: 检查memory:// URL有效性
4. **BASE数据库异常**: 验证YAML语法和过滤器逻辑

### Quality Control
- Always search before creating cross-references
- Verify permalink uniqueness and format
- Test BASE databases with sample data first
- Validate knowledge graph connectivity after major changes
- Maintain consistent terminology across related documents

## Usage Context
This knowledge base primarily serves as a **technical knowledge management system** with focus on:
- Software architecture and design patterns
- Technology evaluation and decision tracking
- Personal knowledge synthesis and connection
- Automated knowledge generation through AI assistance
- Structured relationship mapping between concepts

The repository demonstrates production-ready knowledge management workflows combining modern AI tools with traditional knowledge management methodologies.