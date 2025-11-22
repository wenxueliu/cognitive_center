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
├── zettelkasten/    # Atomic knowledge notes (tech entities, core concepts and so on)
├── create/         # Generated content, decisions, and knowledge workflows
├── template/       # Standardized note templates

/.claude/           # Claude Code environment configuration
/.obsidian/         # Obsidian vault configuration and plugins
```

## Key Systems Integration

### Basic Memory Knowledge Graph
- **Project**: "第二大脑" (Seconde Brain)
- **Standards**: Full Basic Memory 2.0 spec compliance
- **Memory URLs**: Support for memory:// scheme and pattern matching
- **Knowledge Types**: note, entity, decision, process, spec, meeting, person, project and so on
- **Relations**: implements, depends_on, requires, relates_to, extends, pairs_with, part_of, contains, inspired_by, contrasts_with, leads_to, caused_by and so on
- **Observations**: [tech], [design], [decision], [issue], [method], [principle], [fact], [idea], [technique], [requirement], [problem], [solution], [insight], [feature], [preference] and so on

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
1. **Search before creating** to avoid duplicates
2. **Select appropriate template** from `/output/template/`
3. **Follow Basic Memory frontmatter standards**:
   ```yaml
   ---
   title: "Clear Descriptive Title"
   type: note | entity | decision | process | spec | meeting | person | project
   tags: [分类, 技术, 状态, 中文标签]
   permalink: unique-identifier    # Optional: auto-generated from title if not specified
   status: active | draft | deprecated
   aliases: ["别名1", "别名2"]         # Optional
   ---
   ```
4. **Structure content with standard sections**:
   - Main content using markdown
   - `## Context` for background information (optional)
   - `## Observations` for 3-5 categorized insights minimum
   - `## Relations` for 2-3 knowledge graph connections minimum
5. **Ensure valid memory:// URLs** before creating cross-references

### Knowledge Graph Standards
```markdown
## Relations (rich semantic connections)
- implements [[技术概念]]           # Implementation relationship
- depends_on [[系统依赖]]           # Required dependency
- requires [[需求规范]]             # Explicit requirements
- relates_to [[相关概念]]           # General connection
- extends [[扩展知识]]              # Enhancement relationship
- pairs_with [[配套技术]]           # Complementary relationship
- part_of [[更大系统]]              # Hierarchical membership
- contains [[子组件]]               # Component containment
- inspired_by [[灵感来源]]          # Source of ideas
- contrasts_with [[替代方案]]       # Alternative approach
- leads_to [[后续步骤]]             # Sequential relationship
- caused_by [[根本原因]]            # Causal relationship
- ...

## Observations (comprehensive categorization)
- [tech] 技术实现细节 #tag (上下文说明)     # Technical details
- [design] 架构设计决策 #tag (选择依据)      # Architecture decisions
- [decision] 关键决策点 #tag (理由分析)      # Choices made
- [issue] 问题和限制 #tag (影响评估)        # Problems identified
- [method] 方法和技巧 #tag (实现细节)        # Approaches and techniques
- [principle] 基础原理 #tag (理论依据)       # Fundamental concepts
- [fact] 客观事实 #tag (数据来源)            # Objective information
- [idea] 概念和想法 #tag (创新点)            # Thoughts and concepts
- [technique] 实现方法 #tag (最佳实践)        # Implementation methods
- [requirement] 需求和约束 #tag (必要条件)   # Needs and constraints
- [problem] 识别的风险 #tag (影响范围)       # Issues identified
- [solution] 解决方案 #tag (效果评估)        # Resolutions
- [insight] 关键洞察 #tag (价值体现)         # Key realizations
- [feature] 功能特性 #tag (用户价值)         # User capabilities
- [preference] 个人偏好 #tag (选择理由)       # Personal opinions
- ...
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

### memory:// URL Reference Patterns
```bash
# Direct access by permalink or title
memory://unique-permalink
memory://Document Title

# Pattern matching for powerful queries
memory://auth*                       # All documents starting with "auth"
memory://*/approaches                # All documents ending with "approaches"
memory://project/*/requirements      # All requirements in project folder
memory://docs/search/implements/*    # Follow all implements relations from search docs
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

## Best Practices

### Knowledge Creation Workflow
1. **Discovery**: Always start with `list_memory_projects()` to identify working project
2. **Search**: Use `search_notes()` to avoid duplicates before creating new content
3. **Rich Structure**: Every note should include:
   - Clear, descriptive title
   - 3-5 observations minimum with specific categories
   - 2-3 relations minimum with semantic meaning
   - Appropriate tags and metadata
4. **Progressive Elaboration**: Build knowledge incrementally:
   ```
   write_note → edit_note (append/prepend) → move_note → view_note
   ```
5. **Context Building**: Use `build_context()` with memory:// URLs to gather related insights

### Key Workflows

**Knowledge Processing Flow:**
```
Search → Analyze Context → Create/Update → Establish Relations → Validate
```

**Research and Discovery Flow:**
```
search_notes → read_note → build_context → write_note
```

**Organization Flow:**
```
list_directory → search_notes → move_note → validate_structure
```

### Common Commands
```bash
# Project discovery
list_memory_projects                    # View available projects

# Knowledge operations
write_note project="认知中心"           # Create new knowledge
edit_note identifier="title"            # Update existing content
view_note identifier="title"            # Retrieve with relations
search_notes query="关键词" project="认知中心"  # Find knowledge
build_context url="memory://pattern"    # Load related content

# Content organization
list_directory project="认知中心"         # Explore structure
move_note identifier="title"           # Reorganize content
```

## Usage Context
This knowledge base primarily serves as a **technical knowledge management system** with focus on:
- Software architecture and design patterns
- Technology evaluation and decision tracking
- Personal knowledge synthesis and connection
- Automated knowledge generation through AI assistance
- Structured relationship mapping between concepts

The repository demonstrates production-ready knowledge management workflows combining modern AI tools with traditional knowledge management methodologies.
