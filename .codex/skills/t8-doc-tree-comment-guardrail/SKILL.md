---
name: t8-doc-tree-comment-guardrail
description: Enforce documentation structure rules for the t8 project. Use when creating or editing any t8 design/spec/architecture Markdown document that includes a directory tree. Require every directory line in the tree to include an inline comment that explains folder contents and responsibilities.
---

# T8 Directory Tree Annotation Guardrail

Apply this skill to t8 documentation tasks that include directory trees.

## Rule

When a Markdown document contains a directory tree, annotate every folder line with an inline comment that explains:

- what the folder contains
- what responsibility/function it serves

Do not leave any directory line unannotated.

## Workflow

### 1) Detect directory trees

Inspect the document for tree blocks, usually in `text`/`bash` code fences or indented tree lists.

Typical signals:

- lines ending with `/`
- nested indentation that represents folders

### 2) Annotate every directory line

Use one consistent inline style:

- `folder/  # 内容与职责说明`

Rules:

- Write comments in Chinese by default for t8 docs.
- Keep comments short and specific.
- Keep sibling comments at similar granularity.
- If a line is a file (not a folder), comment is optional unless user requests file comments too.

### 3) Enforce completeness

Before finishing, verify:

- all folder lines have comments
- comments describe both content and function (not only one side)
- no placeholder text remains

If any folder line lacks annotation, block completion and fix the document first.

## Output Contract

In the final response, include:

1. updated document path(s)
2. confirmation that all directory entries are annotated
3. note of any exceptions (if none, state `none`)

## Example

```text
core/                     # 内核层根目录，承载核心业务能力
  domain/                 # 领域层，定义业务实体和值对象
    execution/            # 执行域，管理任务与运行生命周期
```
