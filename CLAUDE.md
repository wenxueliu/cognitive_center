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
output/
├── zettelkasten/    # Hierarchy directory, Atomic knowledge notes (tech entities, core concepts and so on)
├── create/         # Generated content, decisions, and knowledge workflows
├── template/       # Standardized note templates

.claude/           # Claude Code environment configuration
.obsidian/         # Obsidian vault configuration and plugins
```

## Key Systems Integration

### Basic Memory Knowledge Graph
- **Project**: "认知中心" (Cognitive Center)
- **Standards**: Full Basic Memory 2.0 spec compliance
- **Memory URLs**: Support for memory:// scheme and pattern matching
- **Knowledge Types**: note, entity, decision, process, spec, meeting, person, project and so on
- **Relations**: implements, depends_on, requires, relates_to, extends, pairs_with, part_of, contains, inspired_by, contrasts_with, leads_to, caused_by and so on
- **Observations**: [tech], [design], [decision], [issue], [method], [principle], [fact], [idea], [technique], [requirement], [problem], [solution], [insight], [feature], [preference] and so on

### Automation Capabilities
```bash
# File search and management
fd "search-term" -e md      # Search markdown files by name
rg "content" --type md      # Search within markdown content
rg -i "keyword" --type md   # Case-insensitive search
```

## Development Standards

### Note Creation Process
1. **Search before creating** to avoid duplicates
2. append to exist note or create note, if create new note, continue
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
   - `## Context` for background information (optional)
   - Main content using markdown
   - `## Observations` for 3-5 categorized insights minimum
   - `## Relations` for 2-3 knowledge graph connections minimum
   - `## source` the content source
5. **Ensure valid memory:// URLs** before creating cross-references
6. mkdir suitable hierarchy directory in output/zettelkasten and write content under zettellkasten dir, move exists document to suitable directory if need

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
- Verify all memory:// URLs reference existing content, make sure uniqueness and format
- Ensure bidirectional relationships are established when meaningful
- Validate frontmatter completeness and consistency
- Check for orphaned knowledge nodes and broken connections

### Content Quality Standards
- Maintain atomicity: one concept per note
- Use consistent categorization (type, tags, status)
- Provide meaningful cross-references through Relations
- Include context and reasoning in Observations
- Prefer specific technical terms over general descriptions

## Error Handling

### Common Issues
1. **文档链接不存在**: 使用 fd/rg 搜索确认文档存在性
2. **UTF-8字符问题**: 注意多字节字符编码兼容性
4. **BASE数据库异常**: 验证YAML语法和过滤器逻辑

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

## Usage Context
This knowledge base primarily serves as a **technical knowledge management system** with focus on:
- Software architecture and design patterns
- Technology evaluation and decision tracking
- Personal knowledge synthesis and connection
- Automated knowledge generation through AI assistance
- Structured relationship mapping between concepts

## 约束
使用中文回答

