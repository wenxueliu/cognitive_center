Learn Basic Memory's knowledge format using standard Markdown with semantic patterns to create a knowledge graph

Understanding how Basic Memory structures knowledge will help you create richer, more connected notes. Here’s how the semantic patterns work.

## File-First Architecture
All knowledge in Basic Memory is stored in plain text Markdown files:

```
Files are the source of truth for all knowledge in Basic Memory
Changes to files automatically update the knowledge graph in the db
You maintain complete ownership and control
Files work with git and other version control systems
Knowledge persists independently of any AI conversation
```

## Core Document Structure
Every document uses this basic structure:

```
---
title: Document Title
type: note
tags: [tag1, tag2]
permalink: custom-path
---

# Document Title
Regular markdown content...

## Observations
- [category] Content with #tags (optional context)

## Relations
- relation_type [[Other Document]] (optional context)
```

### Frontmatter
The YAML frontmatter at the top of each file defines essential metadata:

```
---
title: Document Title    # Used for linking and references
type: note               # Document type
tags: [tag1, tag2]       # For organization and searching
permalink: custom-link   # Optional custom URL path
---
```

The title is particularly important as it’s used to create links between documents.

### Observations
Observations are facts or statements about a topic:

```
- [tech] Uses SQLite for storage #database
- [design] Follows plaint-text architecture #architecture
- [decision] Selected bcrypt for passwords #security (Based on audit)
```

Observations are markdown list items beginning a [category] value. Basic Memory knows to not make Markdown lists: [ ] or [x] into observations.

Each observation contains:

* Category in [brackets] - classifies the information type
* Content text - the main information
* Optional #tags - additional categorization
* Optional (context) - supporting details

Common Categories
[tech]: Technical details
[design]: Architecture decisions
[feature]: User capabilities
[decision]: Choices that were made

Additional Categories
[principle]: Fundamental concepts
[method]: Approaches or techniques
[preference]: Personal opinions


### Relations
Relations connect documents to form the knowledge graph:

```
- implements [[Search Design]]
- depends_on [[Database Schema]]
- relates_to [[User Interface]]
```

Relations are markdown list items beginning a descriptive word, followed by a [[wiki link]] value. The description will by used as the relationship type.

You can also create inline references:

This builds on [[Core Design]] and uses [[Utility Functions]].

Common relation types include:

* implements: Implementation of a specification
* depends_on: Required dependency
* relates_to: General connection
* inspired_by: Source of ideas
* extends: Enhancement
* part_of: Component relationship
* contains: Hierarchical relationship
* pairs_with: Complementary relationship

## Knowledge Graph
Basic Memory automatically builds a knowledge graph from your document connections:

* Each document becomes a node in the graph
* Relations create edges between nodes
* Relation types add semantic meaning to connections
* Forward references can link to documents that don’t exist yet
* This graph enables rich context building and navigation across your knowledge base.

## Permalinks and memory:// URLs
Every document in Basic Memory has a unique permalink that serves as its stable identifier:

### How Permalinks Work
* Automatically assigned: The system generates a permalink for each document
* Based on title: By default, derived from the document title
* Always unique: If conflicts exist, the system adds a suffix to ensure uniqueness
* Stable reference: Remains the same even if the file moves in the directory structure
* Used in memory:// URLs: Forms the basis of the memory:// addressing scheme
You can specify a custom permalink in the frontmatter:
```
---
title: Authentication Approaches
permalink: auth-approaches-2024
---
```
If not specified, one will be generated automatically from the title, if the note has has a frontmatter section.

### Using memory:// URLs
The memory:// URL scheme provides a reliable way to reference knowledge:

```
memory://auth-approaches-2024        # Direct access by permalink
memory://Authentication Approaches   # Access by title (automatically resolves)
memory://project/auth-approaches     # Access by path
```

Memory URLs support pattern matching for more powerful queries:

```
memory://auth*                      # All documents with permalinks starting with "auth"
memory://*/approaches               # All documents with permalinks ending with "approaches"
memory://project/*/requirements     # All requirements documents in the project folder
memory://docs/search/implements/*   # Follow all implements relations from search docs
```

This addressing scheme ensures content remains accessible even as your knowledge base evolves and files are reorganized.

## File Organization
Organize files in any structure that suits your needs:

```
docs/
  architecture/
    design.md
    patterns.md
  features/
    search.md
    auth.md
```

You can:
* Group by topic in folders
* Use a flat structure with descriptive filenames
* Tag files for easier discovery
* Add custom metadata in frontmatter
* Include dates in time-sensitive notes
* Archive old content regularly

Basic Memory uses special memory:// URLs to reference knowledge:

URL Formats
memory://title                   # Reference by title
memory://folder/title            # Reference by folder and title
memory://permalink               # Reference by permalink
memory://path/relation_type/*    # Follow all relations of type
memory://path/*/target           # Find entities with relations to target


## Knowledge Graph Structure
The knowledge graph consists of three core elements: entities, observations, and relations.

### Entities
Each markdown file represents an entity with:

* Title: Unique identifier
* Permalink: Auto-generated from title
* Frontmatter: YAML metadata (tags, type, dates)
* Observations: Categorized facts
* Relations: Links to other entities

Entity types:

* note - General knowledge (default)
* person - People and contacts
* project - Projects and initiatives
* meeting - Meeting notes
* decision - Documented decisions
* spec - Technical specifications

### Observations
Observations are categorized facts with optional tags.

Syntax: - [category] content #tag1 #tag2

Common categories:

* [fact] - Objective information
* [idea] - Thoughts and concepts
* [decision] - Choices made
* [technique] - Methods and approaches
* [requirement] - Needs and constraints
* [problem] - Issues identified
* [solution] - Resolutions
* [insight] - Key realizations

Examples:
```
## Observations
- [decision] Use JWT tokens for authentication #security
- [technique] Hash passwords with bcrypt before storage #best-practice
- [requirement] Support OAuth 2.0 providers #auth
- [fact] Session timeout set to 24 hours #configuration
```

### Relations
Relations are directional links between entities.

Syntax: - relation_type [[Target Entity]]

Common relation types:

* relates_to - General connection
* implements - Implementation relationship
* requires - Dependency
* extends - Enhancement
* part_of - Hierarchical membership
* contrasts_with - Alternative approach
* leads_to - Sequential relationship
* caused_by - Causal relationship

Examples:
```
## Relations
- implements [[Authentication Spec v2]]
- requires [[User Database Schema]]
- extends [[Base Security Model]]
- part_of [[API Backend Services]]
- contrasts_with [[API Key Authentication]]
```

## Forward References
Reference entities that don’t exist yet - relations resolve automatically when targets are created:

```
# Create note with forward reference
await write_note(
    title="API Implementation",
    content="## Relations\n- implements [[API Specification]]",
    folder="api",
    project="main"
)

## Forward reference created

# Later, create referenced entity
await write_note(
    title="API Specification",
    content="# API Specification\n...",
    folder="specs",
    project="main"
)
# Forward reference automatically resolved
```

## Best Practices
1. Project Discovery
Always start with discovery:

```
# First action in conversation
projects = await list_memory_projects()

# Ask user which to use
# Store for session
# Use consistently
```

2. Rich Knowledge Graphs
Every note should have:

* Clear, descriptive title
* 3-5 observations minimum
* 2-3 relations minimum
* Appropriate categories and tags

Good structure:
```
---
title: Clear Descriptive Title
tags: [relevant, tags]
type: note
---

# Title

## Context
Brief background

## Observations
- [category] Specific fact #tag1 #tag2
- [category] Another fact #tag3
- [category] Third fact #tag4

## Relations
- relation_type [[Related Entity 1]]
- relation_type [[Related Entity 2]]
```

3. Search Before Creating
Always search first to avoid duplicates:

```
# Before writing new note
existing = await search_notes(
    query="topic name",
    project="main"
)

if existing["total"] > 0:
    # Update existing
    await edit_note(
        identifier=existing["results"][0]["permalink"],
        operation="append",
        content=new_information,
        project="main"
    )
else:
    # Create new
    await write_note(...)
```

4. Exact Entity Titles in Relations
Use exact titles when creating relations:
```
# Search for exact title
results = await search_notes(query="Authentication System", project="main")
exact_title = results["results"][0]["title"]

# Use in relation
content = f"## Relations\n- relates_to [[{exact_title}]]"
```

5. Meaningful Categories and Relations
Use semantic categories:
* [decision] for choices made
* [fact] for objective information
* [technique] for methods
* [requirement] for needs
* [insight] for realizations

Use specific relation types:

* implements for implementation
* requires for dependencies
* part_of for hierarchy
* extends for enhancement
* contrasts_with for alternatives

Not generic:
* Avoid overusing relates_to
* Be specific about relationships

6. Progressive Elaboration

Build knowledge over time:
```
# Session 1: Create foundation
await write_note(
    title="Topic",
    content="Basic structure with initial observations",
    folder="notes",
    project="main"
)

# Session 2: Add details
await edit_note(
    identifier="Topic",
    operation="append",
    content="Additional observations",
    project="main"
)

# Session 3: Add relations
await edit_note(
    identifier="Topic",
    operation="append",
    content="Relations to related topics",
    project="main"
)
```

7. Consistent Organization

Folder structure:

* specs/ - Specifications
* decisions/ - Decision records
* meetings/ - Meeting notes
* conversations/ - AI conversations
* implementations/ - Code/implementations
* docs/ - Documentation

File naming:

* Use descriptive titles
* Consistent format
* Avoid special characters

## Common Workflows

### Knowledge Creation Flow:

write_note → edit_note (append/prepend) → move_note → view_note

Start with basic note, enhance incrementally, organize, then review

Example conversation
You: "I want to document my thoughts on the new API design"
Claude: I'll create a note for your API design thoughts.
[Uses write_note to create initial note]

You: "Add a section about authentication concerns"
Claude: I'll append an authentication section to your API design note.
[Uses edit_note with append operation]

You: "This should go in my architecture folder"
Claude: I'll move the API design note to your architecture folder.
[Uses move_note to relocate the file]

You: "Show me the final note"
Claude: Here's your complete API design note formatted for easy reading.
[Uses view_note to display formatted artifact]

### Research and Discovery Flow:

search_notes → read_note → build_context → write_note

Find existing knowledge, explore context, create new insights

Example conversation
You: "I'm working on database optimization, what have I learned before?"
Claude: Let me search your knowledge base for database optimization content.
[Uses search_notes to find relevant notes]

You: "Tell me more about that PostgreSQL indexing note"
Claude: I'll read the full PostgreSQL indexing note for you.
[Uses read_note to load complete content and context]

You: "Load the context from my database performance work"
Claude: I'll gather related notes about database performance to build context.
[Uses build_context with memory:// URLs to load related content]

You: "Create a new note combining these insights for my current project"
Claude: I'll create a comprehensive note that synthesizes your database optimization knowledge.
[Uses write_note to capture new insights with full context]

### Project Discovery Flow:

list_memory_projects → recent_activity (discovery mode) → project selection

Discover projects, view cross-project activity, choose working project

Example conversation
You: "What projects do I have available?"
Claude: Here are all your Basic Memory projects with their current status.
[Uses list_memory_projects to show available projects]

You: "Show me recent activity across all projects"
Claude: Here's recent activity across all your projects to help you choose which to work with.
[Uses recent_activity without project parameter for discovery mode]

You: "I want to work with my research project"
Claude: I'll use the 'research' project for our work. All subsequent operations will specify this project.
[Remembers project choice for conversation context]

You: "What have I been working on recently in this project?"
Claude: Here's your recent activity in the research project.
[Uses recent_activity with project="research" parameter]

### Content Organization Flow:

list_directory → search_notes → move_note → list_directory

Explore structure, find content, reorganize, verify changes

Example conversation
You: "Show me what's in my projects folder"
Claude: Here's the structure of your projects folder.
[Uses list_directory to explore folder contents]

You: "Find all notes about the mobile app project"
Claude: I found several notes related to your mobile app project.
[Uses search_notes to locate relevant content]

You: "Move the mobile app notes to a dedicated folder"
Claude: I'll move all mobile app notes to a new 'mobile-app' folder.
[Uses move_note to reorganize content]

You: "Show me the updated folder structure"
Claude: Here's your reorganized projects folder with the new mobile-app directory.
[Uses list_directory to verify the changes]
