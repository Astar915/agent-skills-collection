---
name: note-taking-sap
description: Convert resolved SAP questions, debugging sessions, implementation findings, and practical SAP knowledge into concise, structured personal SAP notes that match the user's existing note-taking style. Automatically identify the relevant SAP module, product, technology, or cross-domain area; preserve practical operation steps, code, screenshots placeholders, external references, and links to related existing notes. Use this skill when the user explicitly asks to "记笔记", "整理成笔记", "生成SAP笔记", or equivalent.

---

# SAP Note Taking Skill

## Shared Obsidian Conventions

Before creating or updating a note, read and follow the shared rules in the shared Obsidian note-taking reference: use `../../_shared/obsidian-note-taking-reference.md` in this repository, or the adjacent `obsidian-note-taking-reference.md` after installation. This reference is the authoritative common layer for all note-taking skills; the SAP-specific rules below add domain behavior and take precedence only when they are more specific. If duplicated generic guidance conflicts with the shared reference, follow the shared reference.

## Mission

Convert a completed SAP discussion into a reusable personal SAP knowledge note.

The goal is **not** to write a generic SAP tutorial.

The goal is to preserve and organize:

- What the user asked.
- What caused the problem.
- What was confirmed.
- What solution was found.
- How the SAP function is actually used.
- Important code.
- Important operation paths.
- Screenshots and image assets that should be inserted directly when available.
- Links to existing SAP notes only when the current note cannot stand alone without a specific dependency or evidence path.
- Useful external references.
- Practical lessons that the user can reuse later.

The resulting note should feel like a natural continuation of the user's existing SAP notes.

---

# 1. Trigger Condition

Use this skill when the user explicitly asks for note-taking after an SAP discussion.

Typical triggers include:

- `记笔记`
- `整理成笔记`
- `把刚才的内容记下来`
- `整理刚才的问题`
- `生成SAP Note`
- `把这个写进笔记`
- `记录一下`
- `这个也记下来`

Do not automatically create a note merely because an SAP question was answered.

The user must indicate that the information should be recorded.

## 1.1 默认记录范围：完整覆盖当前对话

当用户明确要求记 SAP 笔记，但没有指定课程、主题或范围时，默认整理当前对话从开始到当前请求中的全部 SAP 知识内容，不得只记录最近一条消息或最后一节课程。

必须覆盖：用户提供的课程原文、对话中的中文讲解与更正、补充说明、操作路径、SAP 术语、代码、示例数据、截图中可复用的界面和文字信息、已确认结论、限制、易错点以及相关笔记关系。

如果当前对话包含多个课程或主题，可以按主题拆分或合并到合适的多篇笔记中，但每个有价值的知识点都必须有明确归档位置。重复内容可以去重，但不得因为去重而遗漏新增事实、例子或更正。

写入前必须回顾当前对话并进行覆盖检查；只有用户明确指定“只记录某一方面/某一节课”或明确排除范围时，才缩小记录范围。“全部内容”不等于逐字复制寒暄、重复旁白或无信息量文字，但所有可复用知识和证据都应保留，并继续遵守敏感信息脱敏规则。

---

## 1.2 Quiz错题整理规则

当用户要求记录 SAP Quiz 错题时，必须先把错题提炼成可复用的 SAP 知识点，再写入笔记。

- 不要直接粘贴原题干、完整选项、答案编号、判题反馈或测验截图。
- 先识别题目考查的概念，再记录概念定义、对象/规则之间的区别、正确使用方式，以及容易混淆的原因。
- 可以保留一句极简的错因说明，但不要让笔记变成题目复刻；笔记应当在脱离原题后仍能用于复习和解决类似问题。
- 将整理后的知识点归入最相关的既有笔记和标题，避免单独堆积“错题记录”章节。
- 测验截图默认只作为分析依据，不复制到笔记；只有截图本身是独立有复用价值的 SAP 操作或界面证据时，才按截图规则保存。

---

# 2. Primary Objective

The note must answer:

> "If I encounter this topic again several months later, can I quickly understand what this is, how to use it, what I previously discovered, and what I should pay attention to?"

Prioritize:

1. Reusability.
2. Searchability.
3. Practical operation.
4. Technical accuracy.
5. Relationship to existing knowledge.
6. Concise explanation.
7. Consistency with the user's existing notes.

Do not optimize for textbook completeness.

---

## 2.1 Avoid Course-Outline Language

Write the note as direct, reusable SAP knowledge, not as a course introduction or lesson plan. Do not add generic learning-framework headings or filler such as `学习目标`, `课程目标`, `总体关系`, `核心关系`, `本节概述`, `学习内容`, or `学习成果`; do not restate these ideas under slightly different generic labels. Omit course-purpose statements and broad summaries that do not add a concrete SAP fact. If a heading consists only of a generic label such as `Overview`, `概述`, `总览`, `核心问题`, `核心作用`, `课程时间线`, or `学习路线`, replace it with the specific SAP product, mechanism, process, or operation described; delete it when the section only states course purpose, sequence, or repeated summary without reusable facts. Keep a label like `业务流程概览` only when the body explains that named process.

Use headings that name the actual SAP products, components, objects, processes, or functions being explained. If a relationship is useful, state the specific responsibility or interaction between the named items in the body, and use a concrete heading such as `AI Foundation、Generative AI Hub 与 AI Core 的职责` instead of `总体关系` or `核心关系`. Preserve a course objective only when it contains a concrete, reusable SAP fact; rewrite that fact under its actual topic rather than retaining learning-objective wording.

For example, omit a block like:

```markdown
# 学习目标与总体关系

课程目标：识别 SAP AI Foundation 及 Generative AI Hub。

核心关系：AI Foundation 是……；Generative AI Hub 是……
```

and organize any useful facts directly under headings for the SAP components and their specific responsibilities. Do not add this kind of course-outline section by default, even for notes created from SAP Learning courses.

---

# 3. Classification Before Writing

Before generating the note, dynamically identify the most appropriate SAP module, product, technology, or functional area. Do not restrict classification to a fixed list. Possible examples include:

- FI
- CO
- MM
- SD
- PP
- QM
- PM
- PS
- WM
- EWM
- HCM
- SuccessFactors
- Ariba
- SAP BTP
- SAP HANA
- ABAP
- RAP
- CDS
- OData
- Fiori
- UI5
- CAP
- Integration Suite
- SAP Security
- Authorization
- Workflow
- Basis
- BW
- SAC
- S/4HANA
- Clean Core
- AI
- SAP Build
- or any other relevant SAP domain.

The Skill must not assume that the above list is exhaustive.

Record the main topic, subtopic, relevant T-code, relevant development object, and relevant version or architecture when known. If the topic belongs to multiple areas, record the relationship.

Example:

```text
领域：SAP RAP / OData V4 / Fiori Elements
主题：Validation错误消息显示
````

If the exact classification cannot be confidently determined, do not invent one. Use `[待确认]` or record only the confidently known area.

Examples:

```
领域：FI
主题：会计凭证
T-code：F-02
```

or:

```
领域：SAP RAP
主题：Behavior Definition
技术点：Determination
```

or:

```
领域：SAP CDS
主题：常见语法
技术点：CAST
```

Do not invent T-codes or technical classifications.

---

# 3.1 Obsidian Tag Naming

When creating or updating YAML frontmatter tags in an Obsidian note, replace every space in a tag with a hyphen (`-`). Obsidian tags must not contain spaces.

```yaml
tags:
  - ABAP-Unit
```

This rule applies to tag values only. Note titles, aliases, headings, and internal links may still contain spaces when that matches the user's existing naming style.

---

# 4. Heading-Level Rules

The user's existing notes use different heading structures depending on the nature of the content.

## 4.1 Module / Business Function Notes

For SAP module notes, use hierarchical headings.

Typical structure:

```
# 科目表主数据

## FS00字段详解
```

or:

```
# 会计凭证

## F-02字段介绍

## 会计凭证的变更

## FB50：总账记账
```

The module/business topic is normally a level-1 heading.

Specific T-code, function, or knowledge point is normally a level-2 heading.

If the topic needs another level:

```
# 会计凭证

## F-02字段介绍

### 传票日付

### 転記日付
```

Do not create excessive heading levels.

## 4.3 注意点与补充内容的归属

“注意点”“Tip”“易错点”等内容如果能够明确对应已有的一级或二级标题，应直接放在该标题的相关说明、代码或表格之后，不要另建一个独立的“注意点”一级或二级标题。只有在内容确实横跨多个主题且无法自然归属于已有标题时，才考虑单独组织章节。

更新已有笔记时，必须检查现有的“注意点”“补充”“易错点”等集中章节：逐条判断其内容对应的一级或二级标题，并将可归属内容移动到对应章节中。不要因为原来已有该章节就继续把可归属内容留在集中区；如果移动后集中章节为空，应删除该章节，并同步维护目录编号、标题锚点和 Canvas 导航。只有确实横跨多个主题、无法自然放入任一已有章节的内容，才可以保留集中章节。

提醒、使用前提和易错点默认使用 Obsidian 的 `Tip` callout，而不是普通段落：

```markdown
> [!TIP] Tip
> 注意使用前要按与查找键一致的字段顺序 `SORT` 排序。
```

---

## 4.2 Technical Notes

For technical knowledge such as:

- ABAP
- RAP
- CDS
- OData
- BTP
- HANA
- Fiori
- UI5
- CAP

the user's existing notes often use direct level-1 topic headings.

For example:

```
# Determination

# Validation

# DRAFT

# EARLY NUMBERING早期编号
```

or:

```
# 关联

# 拼接字段concat

# 类型转化cast
```

Preserve this style.

Do not force every technical topic into:

```
# ABAP
## RAP
### Determination
```

unless the user's existing file structure clearly calls for it.

---

# 5. Directory / TOC

Add a directory near the beginning of every note unless the total number of actual level-1 and level-2 headings is no more than two. Count only headings in the note itself, not headings shown inside examples or code blocks.

When a directory is required, place it immediately after the YAML frontmatter when frontmatter exists; otherwise place it at the beginning of the note.

Follow the user's existing style:

```
## 目录

1 科目表主数据
   --1-1 FS00字段详解
2 会计凭证
   --2-1 F-02字段介绍
   --2-2 会计凭证的变更
   --2-3 FB50：总账记账
3 税
4 其他
   --4-1 FBL3N总账科目明细
   --4-2 FAGLB03总账余额查看
```

The exact numbering style should follow the user's existing note where possible. The directory must reflect every level-1 and level-2 heading that it covers and use clickable Obsidian anchors when the note format supports them.

---

# 5.1 本 Skill 的笔记固定格式

本 Skill 创建或更新的所有 SAP 笔记，都遵循上一节的目录阈值：一级标题和二级标题总数超过 2 个时必须添加目录；总数不超过 2 个时可以省略。需要添加目录时：

- 在 YAML frontmatter 后添加“目录”，并使用 Obsidian 锚点链接；
- 删除与文件标题重复的原一级标题；
- 原二级标题提升为一级标题，原三级标题提升为二级标题；
- 小标题编号中的点改为短横线，例如 `2.1` 改为 `2-1`、`3.2` 改为 `3-2`；
- 锚点编号必须与目录编号一致：一级章节使用 `^2`，其子章节使用 `^2-1`、`^2-2`，不要使用连续的 `^1`、`^2`、`^3` 代替层级编号；
- 二级目录项前加两个短横线 `--`，例如 `--[[#^2-1|2-1 FS00字段详解]]`，用于体现目录层级；
- 目录显示文本和实际标题中的编号必须保持一致；
- 若目录中引用了相关笔记或 Skill，应使用可点击的 Obsidian Wiki Link。

# 5.2 笔记内容修改后的编号同步规则

以后只要新增、删除、合并或调整笔记章节，必须同步检查并维护该笔记的编号体系：

- 目录显示编号、标题中的编号和标题锚点（`^...`）必须保持一致；
- 同一层级的章节编号默认保持连续；删除或插入章节后，按现有层级同步重排后续编号，除非用户明确要求保留旧编号；
- 子章节编号必须跟随父章节编号调整；
- 如果 Canvas、索引笔记或其他笔记引用了受影响的章节锚点，必须同步更新或删除失效引用；
- 修改完成后，扫描旧编号、重复编号、缺失锚点和失效目录链接。

# 6. Preserve the User's Personal Note Style

The user's notes are practical learning notes rather than formal documentation. Write primarily in Chinese while preserving SAP English technical terms, Japanese SAP UI labels, T-code names, and code identifiers. For SAP terminology, use Japanese terms verified in official SAP Japanese localized documentation (such as SAP Help Portal or official SAP product/course documentation), matching the product and context where possible. Never infer or invent a Japanese translation from English or substitute a generic dictionary equivalent. If an official Japanese equivalent cannot be verified, leave the SAP term in English. At the first meaningful occurrence in each note, add the verified Japanese term in parentheses, for example `company code（会社コード）`; do the same for key terms in preserved English source passages. Keep exact technical identifiers, field names, API names, code, and UI labels verbatim; add a verified Japanese explanation in adjacent prose instead of changing the identifier.

Therefore:

Prefer:

```
mapping for：用于连接database table和interface层cds字段的连接。
```

over:

```
The mapping for statement establishes the correspondence between database persistence fields and CDS interface fields.
```

Prefer:

```
点击publish后会显示你的程序之间是否有报错。
如果没有报错则发布成功。
```

over a generic conceptual explanation.

The Skill should preserve the user's natural style where it remains understandable.

Do not unnecessarily rewrite everything into polished academic Chinese.

Do not translate or alter exact technical identifiers, field names, API names, or code. Add the Japanese professional term to the adjacent explanatory text instead. Japanese UI labels should remain when useful for finding the corresponding button in a Japanese SAP system.

---

# 7. Operation-Oriented Notes

For SAP GUI, Fiori, Eclipse, ADT, or other practical operations, prioritize the actual operation sequence.

Capture:

```
在哪里进入
↓
输入什么
↓
选择什么
↓
点击什么
↓
看到什么
↓
下一步怎么做
↓
如何确认结果
```

Example:

```
## FBL3N总账科目明细

输入科目编码和公司代码，以及筛选项之后即可查看。

[图片：FBL3N筛选界面]

双击凭证编号可以查看行项目明细。

[图片：行项目明细界面]

此时点击「伝票概要呼出」可以查看会计凭证明细。
```

Do not replace practical operation instructions with generic SAP theory.

## 7.1 SAP业务模块前台与后台的边界（强制）

记录 SAP 业务模块时，必须先判断每段内容属于 **前台业务操作**、**后台配置**、**概念说明**，还是混合内容，并在笔记中明确区分；不得把前台操作和后台配置混在同一个无标识的步骤段落中。

- **前台**：用户日常使用的 Fiori 应用、SAP GUI 业务事务和菜单操作，例如创建/维护 G/L Account 主数据、过账、查看行项目、清账和报表查询（如 `FS00`、`FSS0`、`FBL3N`）。
- **后台**：IMG/SPRO Customizing、配置活动和组织分配，例如定义或分配 Company Code、Chart of Accounts、Group/Country Chart、Field Status Variant、Ledger 和其他全局设置。
- `SPRO` 路径、Customizing 活动和配置对象应归入后台配置笔记；Fiori/SAP GUI 的业务操作步骤应归入前台业务笔记。不要因为两者都使用 SAP GUI 或同一个业务对象，就把它们视为同一层。
- 既有概念又有操作时，可以在业务笔记中保留简短概念和结果；后台配置步骤应单独放在后台配置笔记中，避免重复整段前台操作说明。只有读者必须跳转查看未重复的配置细节时，才加一条直达 Wiki Link；否则保持两篇笔记自包含，不强制互链。
- 为每个新增或移动的段落补充清晰的类型标识，例如 `类型：前台操作`、`类型：后台配置` 或 `类型：概念 + 后台配置`。无法可靠判断时使用 `[待确认]`，不要凭标题或截图外观猜测。

完成整理前，逐项检查：所有 `SPRO/IMG` 路径是否只出现在后台配置部分，所有过账/查询/主数据维护步骤是否只出现在前台部分，前后台之间是否通过链接关联而非重复复制。

### 7.1-1 前台/后台路径补全

- 如果截图、课程文字或用户提供的资料只显示了菜单末级节点，或省略了前面的上级路径，应结合同一资料中的上下文、SAP 菜单层级和已确认的模块信息，尽量补齐可可靠确认的前台或后台路径。
- 补全后的路径必须保留原始 SAP 菜单名称、Customizing 活动名称和事务代码；不要为了完整而臆造无法确认的层级。
- 无法可靠确认的上级节点使用 `[待确认]` 标记，并区分“资料明确显示”与“根据上下文补全”的内容。
- 路径补全后重新检查前台/后台边界，确保 `SPRO/IMG` 及 Customizing 路径仍归入后台配置，业务维护、查询和过账路径仍归入前台操作。

---

# 8. T-Code Preservation

When a T-code appears in the discussion, preserve it exactly whenever possible.

Examples:

```
FS00
F-02
FB02
FB03
FB08
FB50
FBL3N
FAGLB03
F.01
```

T-codes are important search keywords.

Do not replace:

```
F-02
```

with:

```
会计凭证创建事务
```

The T-code should remain visible.

If several T-codes are related, preserve their relationship.

Example:

```
FB02：更改允许修改的文本性数据
FB08：取消会计凭证
FB03：查看会计凭证
```

If the demonstrated SAP operation can also be started or completed directly with a known T-code, record the T-code in addition to the demonstrated menu path and screen-by-screen steps. Do not replace the practical demonstration with the T-code; preserve both so the note supports users who learn from the UI and users who prefer direct transaction entry.

Prefer making the entry point explicit, for example:

```text
事务代码：F-02
操作路径：SAP菜单 → 会计 → 财务会计 → 总账 → 过账 → 一般过账
```

Only add a T-code when it is provided, confirmed, or reliably established from the discussion or available evidence. Do not infer or invent one; use `[待确认]` when the direct transaction code is uncertain.

---

# 9. Code Formatting

All SAP code must be placed inside code blocks.

Examples:

```
determination calcTotalAmount on modify {
  field i_quan, i_unit_price;
}
```

For CDS:

```
cast(
  bseg.sgtxt as abap.char(1)
) as sgtxt,
```

For Behavior Definition:

```
define behavior for ZZI_PUR_REQ_H
persistent table zzpur_req_h
lock master
authorization master ( instance )
{
  create;
  update;
  delete;
}
```

Do not place important code inline in normal paragraphs.

---

# 10. Preserve Code Explanation Style

The user frequently explains code using comments such as:

```
concat( bseg.shkzg, bseg.hkont ) as zzshhkont
// ↑ as后面接自定义的新字段名称
```

Preserve this style when appropriate.

It is acceptable to annotate code with:

```
field( readonly ) h_req_number;
// ↑ 将字段设置为只读
```

or:

```
draft determine action Prepare
{
  validation validateStatus;
  // ↑ 在Draft Prepare阶段执行Validation
}
```

Do not remove useful explanatory comments merely to make the code look cleaner.

## 10.1 Quick Fix / 自动修复规则

当用户提供的内容中包含 `Quick Fix`、`Quick Assist`、自动修复、向导生成或类似操作时，默认优先给出可以直接编写或修改的对应代码，而不是优先建议使用 Quick Fix。

- 除非手动编写代码非常困难、非常繁琐，或手动处理容易遗漏关键生成内容，否则不要把 Quick Fix 作为首选解决方案。
- 如果能够确定对应的代码修改，应直接提供完整且可执行的代码片段，并说明需要放在哪个对象、哪个方法或哪个位置。
- 记笔记时，必须同时记录该代码的解析：说明关键语句、字段、参数、生命周期位置以及代码实际解决的问题；不要只记录“点击 Quick Fix 即可”这类操作描述。
- 如果最终仍需要使用 Quick Fix，应说明为什么手动代码方案不适合，并尽量记录 Quick Fix 实际生成或应当生成的代码及其作用。
- 代码尚未经过实际系统验证时，明确标记为建议或 `[待确认]`，不要把推测代码写成已确认结果。

---

# 11. Screenshot / Image Rules

When an actual screenshot or image attachment/local file is available and the image provides reusable visual value beyond clear text, code, or tables, insert it directly into the note and place a copy in the appropriate `Assets` folder. Do not leave a manual placeholder when a genuinely useful image file is accessible.

Exception for quiz screenshots: when the user asks to turn a quiz mistake into knowledge points, do not embed the original quiz screenshot. Treat it as analysis evidence and preserve only the distilled knowledge unless the screenshot independently documents a reusable SAP operation or UI.

Never fabricate an image.

Whenever a screenshot, UI image, Eclipse screenshot, SAP GUI screenshot, error screenshot, execution result, or visual reference would materially help the note, use the actual image if it is accessible. Copy the image into the `Assets` folder belonging to the note's subject area, following the existing vault directory convention; if the note area has a dedicated `Assets` folder, use that folder. If clear text, code, or a table communicates the information just as well, do not force an image into the note.

Use an informative filename containing the topic and, when useful, a sequence number. In the Markdown note, embed the copied file with an Obsidian embed such as:

```
![[10. SAP notes/ABAP/Assets/ABAP-3-1-1_标准排序哈希表.png]]
```

Do not link directly to temporary directories, clipboard paths, or unstable external attachment paths. Preserve the original file extension and avoid overwriting an existing asset unless it is clearly the same image and replacement is intended.

For every embedded image, add a nearby explanation in the note before or after the embed. Explain the important objects, arrows, fields, screen regions, sequence, hierarchy, or visual evidence and connect them to the SAP concept, configuration decision, operation step, or troubleshooting conclusion. An image must not be left without searchable interpretation.

Use:

```
[图片：FS00字段界面]
```

or:

```
[图片：Service Binding创建界面]
```

or:

```
[图片：Validation错误在UI中的显示结果]
```

Only when the image cannot be accessed, copied, or confidently identified, use a placeholder:

```
[图片：此处插入相关截图]
```

Do not fabricate an image or claim that it contains information that was not actually observed.

## 11.1 多图片时优先代码化并减少图片数量

当用户一次提供了较多图片时，先逐张判断图片中的内容是否可以准确解析为代码、文本、表格或结构化说明，再决定是否保留图片。目标是减少笔记中的图片数量，同时保留真正依赖视觉信息的内容。

- 对代码、配置、字段清单、日志、报错文本、可复现的操作步骤以及其他能够准确读取的结构化内容，尽量转换为对应的 Markdown、SAP 代码块、表格或普通文本；多张图片中的相同或连续内容应尽量合并整理，避免重复嵌图。
- 流程图、画面图/UI截图、结构图、架构图、布局关系图、视觉结果图等依赖位置、连线、层级或整体画面的内容，不要求解析为代码，可以保留并按普通图片规则保存和嵌入。
- 如果一张图片同时包含可代码化内容和重要视觉信息，提取可代码化部分，并视其视觉信息是否仍有复用价值决定是否保留原图。
- 图片内容模糊、遮挡、无法可靠识别或转换后会丢失重要信息时，不要猜测或强行代码化；保留原图，必要时标记 `[待确认]`。
- 对内容重复的图片，优先保留一张最清晰且信息最完整的代表图，并在正文中补充从其他图片准确提取出的差异内容。

## 11.2 集中 Assets 时的图片引用与失效排查

将图片放入笔记所属区域的 `Assets` 文件夹后，先检查同一笔记库中已经正常显示的图片嵌入，并沿用该库实际可用的语法和路径格式。不要仅凭文件在磁盘上存在，就判断 Obsidian 一定能解析嵌入。

选择路径时遵循以下规则：

- `![[文件名.png]]` 只有在目标文件名在当前库中唯一、且这种写法在当前笔记库中可以解析时才使用。集中 `Assets` 的库通常可用这种写法，但要先核对文件是否重名。
- `![[文件夹/文件名.png]]` 中的文件夹路径按 Obsidian 的 Wiki Link 规则从当前 Vault 根目录开始，不是相对于当前笔记目录。需要带目录时，先确认当前实际打开的 Vault 根目录，再从根目录计算路径；不要把 `Assets/...` 想当然地当成笔记旁的相对路径。
- 若使用 Markdown 图片语法，按当前 Vault 的 `Files & Links` 链接设置和同库可用示例生成路径；不要为试错而在 Wiki Link 与 Markdown 路径间反复猜改。
- 所有链接都必须指向 Vault 内的实际文件，保留准确的文件名和扩展名；不要使用操作系统绝对路径、剪贴板临时路径或 Vault 外部的临时目录。

```markdown
![[Excel-Overview-image71.png]]
```

写入前后按以下方式排查并验证：

- 确认图片确实位于当前打开的 Vault 内，并核对实际 Vault 根目录、笔记路径、Assets 路径、文件名大小写/字符和扩展名；检查全库是否有同名文件。
- 对照一条在同一笔记库中已正常显示的嵌入，确认新嵌入采用相同且适用的链接格式。Obsidian 对 Wiki Link 的目录路径按 Vault 根目录解析；需要时参照[官方链接说明](https://obsidian.md/help/links)。
- 在 Obsidian 中打开笔记并确认图片实际渲染。只用文件系统检查（例如 `Test-Path`）只能证明文件存在，不能证明 Obsidian 已解析该链接。
- 如果文件在磁盘上存在、链接格式与路径也核实正确，但 Obsidian 仍显示“找不到文件”，检查当前打开的是否为预期 Vault；对外部复制到 Vault 的新附件，刷新/重新打开笔记，必要时在 Obsidian 中重建 Vault 缓存，再确认渲染结果。
- 不要连续尝试多个未经核实的路径变体，也不要在未看到 Obsidian 正常渲染时报告“图片已修复”。如果无法检查 Obsidian 预览，应明确说明仅完成了文件路径核对，渲染尚未验证。

完成笔记整理或迁移后，必须批量扫描所有图片嵌入：确认每个引用都能按当前 Vault 的链接格式解析，目标图片位于对应 Assets 文件夹，且没有临时目录、剪贴板路径或旧 Assets 路径。不能只检查用户截图中显示的单张图片。

---

# 12. Remove Screenshot Residue

The user's original notes may contain standalone numbers caused by screenshot insertion or editing.

Examples:

```
321
475
661
652
628
```

If the number is clearly not meaningful SAP knowledge and is only a screenshot/editing residue, remove it.

Replace it with an appropriate image placeholder when necessary:

```
[图片：相关界面]
```

Do not remove numbers that are clearly meaningful technical values.

For example:

```
40表示总账借方
50表示总账贷方
```

must remain.

---

# 13. Note Linking and Cross-Domain Relationships

默认不添加笔记之间的内部 Wiki Link；先让每篇笔记自包含。只有读者必须跳转到另一篇现有笔记，才能理解、验证或完成当前笔记中的具体内容时，才添加最少的一条直达链接。关系存在本身不足以加链。

### 链接必要性与图谱密度

用“这个链接能否帮助读者理解、验证或完成当前知识点”判断是否建立内部链接。仅仅同属 SAP、同属 ABAP/RAP/BTP、出现在同一索引、关键词相似或在同一次讨论中出现，不足以建立笔记间的链接。

只有下列情况可能需要建立链接：

- 当前说明明确依赖另一篇笔记中的概念、技术对象、操作步骤、排错方法或证据；
- 业务与开发内容因职责不同而分别归档，需要从一篇笔记跳转到另一篇查看未重复的细节；
- 明确的前置、后续或跨模块依赖能帮助读者执行操作、作出判断或验证结果。

确需跳转时，把一条链接放在说明具体依赖的位置，并指向读者必须查看的笔记。仅供回顾、延伸阅读、一般导航或主题相关的链接通常省略；已有索引和 Canvas 负责一般导航。不要仅因同属一个索引，就让同级笔记彼此互链或列出同组全部笔记。

避免在多个段落重复同一链接，也不要只为图谱对称而例行添加反向链接。反向链接只有在从目标笔记出发时也能提供独立、具体的帮助，才添加。

如果当前笔记没有复述读者必须使用的前置条件、操作细节或验证证据，可加一条直达链接；若相关内容已在当前笔记中足以理解和使用，则省略链接。

写入前检查每个新链接的具体用途和目标是否存在；无法说明链接为何能帮助当前读者时，不要添加。

Do not create standalone headings such as `# 相关笔记` or `## 相关笔记` to list related notes. The mere existence of a related note does not require a link; add one only when the reader must open it for a specific detail omitted from the current note.

Never invent the name of a note if the actual note name is unknown.

If the exact note name is uncertain, write:

```
[相关笔记：需要手动确认]
```

instead of fabricating a Wiki Link.

Some SAP topics belong to multiple technical areas. Do not split one coherent problem into separate notes merely because it spans domains. If separate notes are necessary, add a direct link only when the reader must consult the other note for a specific omitted detail; otherwise record the needed context in each note and omit cross-links.

For example:

```
RAP
↓
Behavior Definition
↓
Validation
↓
OData V4
↓
Fiori Elements
```

Example:

```
**领域：** SAP RAP / OData V4 / Fiori Elements

**主题：** Validation错误消息显示
```

## Canvas同步要求

每次创建、更新、合并、改名或调整 SAP 笔记后，必须在同一任务中定位并同步更新对应的 Obsidian Canvas；不能只更新 Markdown 笔记而遗漏 Canvas 导航。

同步至少包括：

1. 新增或变更笔记的根文档链接。
2. 新增、删除或改名章节对应的 Canvas 主题节点及章节链接（如果该 Canvas 使用章节导航）。
3. 文件名、Wiki Link、章节锚点和父子层级关系。
4. Canvas JSON 合法性、节点引用、链接目标、颜色、位置和箭头连接。

### 无现有 Canvas 时必须创建

如果目标笔记文件夹内没有对应 Canvas，不得把 [待确认] 当作常规处理结果，也不得只在最终回复中说明缺失。默认必须在同一任务中于该笔记文件夹创建一个 Canvas，文件名优先使用“文件夹名.canvas”。尤其是用户首次要求在一个文件夹内记笔记时，创建首篇 Markdown 笔记的同时就要建立 Canvas；不要等用户再次提醒。

新建 Canvas 时：
1. 以当前文件夹的主题作为根节点。
2. 为文件夹内所有相关的现有笔记和本次新增/更新的笔记建立入口；不能只收录本次新增笔记而漏掉同文件夹的旧笔记。
3. 多章节笔记继续按第 13.1 节建立主要章节主题子节点，并检查父子边方向。
4. 如果存在上级索引，添加指向 Canvas 的索引链接；Canvas 根节点也应提供返回索引的入口。
5. 采用邻近 SAP Canvas 的颜色、字体和层级惯例；不重排无关文件夹或整个 Vault。
6. 完成后验证 JSON、节点引用、笔记文件链接、章节导航、边方向和索引链接。

只有在确实无法创建或写入目标文件时，才报告 [待确认] 并说明具体阻塞原因。目标目录中不存在 Canvas 本身不是跳过创建的理由。

# 13.1 Canvas 与文件夹 / 目录关系

当笔记库使用 Obsidian Canvas 作为目录导航时，Canvas 是文件夹、索引笔记和实际笔记之间的可视化导航层。创建或更新笔记、合并笔记、改名笔记或调整章节后，需要核对这三层关系：

```text
索引笔记
  ↓ 链接到
Canvas
  ↓ 链接到
文件夹中的实际笔记
  ↓ 章节锚点对应
笔记目录中的一级标题
```

检查范围：

1. 当前文件夹中的 `.md` 笔记是否都在对应 Canvas 中有合理入口。
2. Canvas 中的 Wiki Link 是否指向现有文件，是否仍使用旧文件名。
3. Canvas 中带 `#` 的章节链接或 `#^anchor` 块链接是否仍存在。
4. 上级索引笔记指向的 Canvas 文件是否真实存在；改名后要同步更新索引。
5. Canvas 节点的主题名称是否与当前笔记目录中的一级标题一致。
6. 空白 Canvas 应标记为“待建设/占位”，不要仅因为存在空白 Canvas 就自动创建内容。

对于本笔记库当前使用的 Canvas 风格：

- 表示一篇实际笔记的父级文字框只保留一个指向该笔记根文档的链接，不要同时在同一个父框中重复链接根文档和某个子章节。
- 连接到某个父级笔记的子文字框，应代表该笔记目录中的一级标题；如果笔记目录已经有编号，Canvas 小文字框可以只显示标题，不必重复显示编号。
- 如果用户要求 Link 描述带编号，将编号放在 Wiki Link 的显示别名中，例如 `[[ABAP-3-4 内表查找与输出过滤|ABAP-3-4 内表查找与输出过滤]]`，不要擅自把编号加到所有 Canvas 文字框。
- 合并子笔记后，应把 Canvas 链接改为合并后笔记的章节锚点或根文档链接，并删除旧的独立笔记链接。

父子层级要求：

- 当一篇实际笔记作为 Canvas 的直接子节点，且该笔记包含多个有意义的一级或二级章节时，Canvas 不能在该笔记节点处停止；必须在该笔记父节点下面继续建立对应的章节主题子节点。
- 直接笔记节点只保留一个指向笔记根文档的 Wiki Link；章节子节点默认只显示标题文字，不添加 Wiki Link、章节锚点或块链接。
- 章节子节点应覆盖笔记中具有复习或导航价值的主要章节；“外部参考”等辅助性章节可以不单独建立节点。
- 如果笔记只有一个短主题或没有可分解的章节，可以省略第二层章节节点。

Canvas箭头方向要求：

- 对于父子层级关系，箭头必须由子节点指向父节点：`fromNode` 必须是子节点，`toNode` 必须是父节点；不得反过来由父节点指向子节点。
- 反转已有父子边时，同时交换 `fromNode` / `toNode` 及对应的 `fromSide` / `toSide`，保持画布上的实际连接位置不变。
- 只有确认边表示父子层级时才应用此规则；同级流程、时序或普通引用边不要仅凭节点位置擅自反转。

# 13.2 Canvas 的视觉层级与修改规则

修改 Canvas 时，先观察同一 Canvas 已有的颜色、位置和箭头连接，不要只修正文字而破坏视觉层级。当前 ABAP Canvas 的约定是：

| Canvas对象 | 当前约定 |
| --- | --- |
| 根主题框 | 颜色 `1` |
| 直接连接的笔记/父级框 | 颜色 `4` |
| 父级框下面的主题框 | 颜色 `5` |
| 直接笔记框到根主题的箭头 | 颜色 `1` |
| 子主题框到父级笔记框的箭头 | 颜色 `4` |

这些颜色是当前笔记库的本地约定；如果用户已有其他 Canvas 的颜色体系，应优先保持该 Canvas 的现有风格。

位置和箭头检查：

- 同一级文字框应放在相近的层级和方向上。
- 新节点应放在对应父节点附近，并避开已有节点和箭头。
- 如果一个节点逻辑上直接属于根主题，箭头必须连接根主题，不能为了位置方便连接到旁边的兄弟节点。
- 修改 `fromSide`、`toSide` 和箭头颜色时，要与同一层级的现有箭头保持一致。
- 调整文字框宽度或高度时，确保 Link 描述不会遮挡其他节点或造成箭头穿过文字框。

# 13.3 Canvas章节节点默认不加 Link

当 Canvas 中的子主题框只是表示实际笔记中的一级或二级标题时，默认只保留标题文字，不添加 Wiki Link、章节锚点或块链接。即使该标题在笔记中是一级标题（`#`），在 Canvas 中也作为父级笔记下的普通子主题框处理。

只有在用户明确要求，或现有 Canvas 明确规定该节点承担导航作用时，才添加 Link。笔记正文中的目录链接和相关笔记链接不受此规则影响。

# 13.4 Skill文件修改时同步到 Obsidian

每次修改本 `note-taking-sap` skill 后，默认将相同的实质性修改同步到 Obsidian 中的技能副本：

```text
00 Agent skills/skills/note-taking/note-taking-sap/SKILL.md
```

修改完成后需要核对两份文件内容是否一致。只有当用户明确说明某次修改不需要同步到 Obsidian 时，才只修改 Codex 当前使用的 skill 文件，并保留 Obsidian 副本原状。

授权边界：

- 用户只要求“检查 Canvas”时，只读扫描并报告 JSON、链接、锚点、文件夹覆盖和视觉层级问题，不修改 Canvas。
- 用户明确要求“检查 Canvas”时，只读扫描并报告 JSON、链接、锚点、文件夹覆盖和视觉层级问题，不修改 Canvas；如果用户要求创建、修正或修改 Canvas，按要求执行。
- 在笔记文件夹缺少 Canvas 时，按本节“无现有 Canvas 时必须创建”的默认规则创建，并同步更新必要的索引链接。
- 不要因为发现空白 Canvas、布局偏好或可优化项而擅自重排整个 Canvas。

修改后至少验证：

1. Canvas 是合法 JSON。
2. 所有 edge 的 `fromNode` 和 `toNode` 都指向现有节点。
3. Canvas 中的笔记链接目标存在。
4. 章节链接对应的标题或块锚点存在。
5. 改名或合并后没有旧文件名、旧 Canvas 文件名或旧章节链接残留。
6. 节点颜色、箭头颜色、位置和连接层级符合该 Canvas 原有结构。

# 14. External References

If the original discussion used external sources, preserve useful references.

When external documentation was used to verify an answer or explain a technical point, add a concise `## 外部参考` section to the primary note only when there is at least one useful external link to preserve. If there are no external links, omit the heading entirely; do not leave an empty section or a placeholder heading. Prefer direct links to the exact official page rather than search-result pages. Keep the link close to the relevant topic when that improves searchability, and do not duplicate the same URL across multiple notes unless each note uses it for a different purpose.

Prefer:

- Official SAP documentation.
- SAP Help.
- SAP Learning.
- Official technical documentation.

Community articles may also be preserved when they were genuinely useful.

Example:

```
## 外部参考

- SAP Help：[相关主题]
- CSDN：[相关主题]
```

For SAP technical notes, prefer the following source order:

1. SAP Help / ABAP Keyword Documentation.
2. SAP Learning or other official SAP documentation.
3. SAP Community or other reliable secondary sources only when they add practical value.

If a source was used only for verification, record it as an external reference and keep the conclusion phrased as a general SAP rule. Do not imply that the user's own system was tested unless the user provided system evidence.

External information must remain distinguishable from the user's own experience.

Do not present an external claim as if it were confirmed by the user's own system.

If the user personally observed:

```
在我的系统中，激活后会报这个错误。
```

preserve it as an observed experience.

If an external source says:

```
SAP官方文档说明……
```

identify it as external/general information.

If something is only a hypothesis:

```
可能是……
```

do not rewrite it as:

```
原因是……
```

unless it was subsequently confirmed.

---

# 15. Problem / Root Cause / Solution Notes

When the note comes from debugging, structure it around the actual problem.

Recommended pattern:

````
# 问题名称

**领域：** SAP RAP

## 问题

描述实际现象。

## 原因

确认后的根因。

## 解决方法

具体修改。

```abap
...
````

## 为什么

解释SAP框架为什么会产生这个行为。

## 注意点

记录以后容易再次踩坑的地方。

相关概念的 Wiki Link 应直接嵌入上面的说明或注意点中，不单独创建“相关笔记”标题。

````

Do not include a root cause as confirmed if the original discussion only established it as a hypothesis.

---

# 16. Debugging Evidence

For debugging notes, preserve useful observations such as:

- Breakpoint result.
- Field value before modification.
- Field value after modification.
- `FAILED`.
- `REPORTED`.
- `MAPPED`.
- `%TKY`.
- Transaction buffer state.
- Draft state.
- Database state.
- OData response.
- UI behavior.

Example:

```text
Validation已经命中断点，但是UI没有显示错误。

进一步确认：

Validation执行
→ FAILED有数据
→ REPORTED有%MSG
→ OData Response返回消息
→ UI未显示

因此问题不一定在Validation本身，而可能在前端消息处理。
````

Do not simplify away evidence that may help future debugging.

---

# 17. RAP-Specific Note Rules

For RAP notes, preserve important technical distinctions.

Examples:

- Behavior Definition.
- Behavior Pool.
- Managed / Unmanaged.
- Projection Behavior.
- Draft.
- Determination.
- Validation.
- Action.
- EML.
- `READ ENTITIES`.
- `MODIFY ENTITIES`.
- `IN LOCAL MODE`.
- `%tky`.
- `%control`.
- `FAILED`.
- `REPORTED`.
- `MAPPED`.
- ETag.
- Early Numbering.
- Lock.
- Authorization.
- Mapping.
- Save sequence.

Example:

```
MODIFY ENTITIES OF ZZI_PUR_REQ_H IN LOCAL MODE
  ENTITY Header
  UPDATE FIELDS ( h_status )
  WITH updates
  FAILED DATA(failed)
  REPORTED DATA(reported).
```

Do not omit important RAP lifecycle details merely to make the note shorter.

---

# 18. Module-Specific Notes

For business modules, preserve practical business meaning.

For example, FI notes may contain:

```
FSP0：科目表层科目主数据
FSS0：公司代码层科目主数据
FS00：集中维护
```

and:

```
40：总账借方
50：总账贷方
D：借方
C：贷方
```

Do not replace these with generic accounting theory.

If a module has specific business terminology, preserve the original SAP terminology.

Japanese SAP UI terminology may also be preserved:

```
伝票日付
転記日付
伝票概要呼出
シミュレーション
転記
```

---

# 19. Do Not Over-Explain

The note should be concise.

Do not add:

- Long introductions.
- Generic SAP history.
- Definitions that the user does not need.
- Repeated conclusions.
- Large documentation-style sections.
- Low-probability edge cases that were not relevant to the original problem.

The note should preserve useful knowledge, not everything discussed.

---

# 20. Do Not Invent Missing Information

If the original discussion does not provide enough information, use:

```
[待确认]
```

or:

```
[需要实际系统确认]
```

For approved placeholders related to company/project-specific facts, use the appropriate placeholder when applicable:

```
[Approved company fact required]
[Verified case-study evidence required]
[Approved service scope required]
[Legal review required]
[Privacy review required]
[Security confirmation required]
[HR approval required]
[Translation/localization review required]
```

For SAP personal notes, prefer:

```
[待确认]
```

when no stronger placeholder applies.

---

# 21. Note Location

When a related existing note is found, update that note instead of creating a new standalone note. Place the new material under the most relevant existing level-1 (`#`) or level-2 (`##`) heading. If the exact heading does not exist, create a new heading under the related note only when the topic clearly belongs there.

When no related note exists, inspect the user's indexes, canvases, folder names, and neighboring notes to determine the appropriate directory. Create the new note in that related directory and follow its naming and structure conventions. Do not default to the top-level notes directory when a more specific, confident directory is available.

If the correct directory cannot be determined confidently, use the top-level notes directory and mark the classification or location as `[待确认]` rather than inventing a folder.

Do not modify unrelated existing notes or reorganize the user's folder structure.

## 21.1 BAPI与ABAP笔记归档规则

涉及以下内容时，优先归档到 ABAP 相关笔记，而不是 SAP FI 业务笔记：

- BAPI、Function Module、RFC、SE37、SE11 Structure 的技术说明；
- Import、Export、Tables 参数和字段映射；
- `CALL FUNCTION` 调用代码、更新标识（例如 `X` 结构）、`COMMIT`/`ROLLBACK` 处理；
- BAPI 接口限制、版本差异以及通过 `Z` RFC 封装的实现建议。

如果同一个问题同时包含业务和开发内容，应按职责分别归档：FI 笔记保留业务含义、事务代码和操作流程，ABAP 笔记保留 BAPI/Structure/代码等实现内容。两边不要重复复制整段内容；只有业务笔记的读者必须查看未重复的实现细节时，才添加一条指向已确认 ABAP 笔记的直达链接。

移动已有内容时，应从原业务笔记中删除重复的 BAPI 技术段落，只保留必要的业务说明；内部链接按第 13 节的必要性标准决定，可省略。

---

# 22. File Naming

Choose a concise, searchable filename.

Prefer:

```
RAP Validation错误消息不显示.md
CDS cast类型转换.md
FI F-02字段介绍.md
Service Binding创建与预览.md
```

The filename should contain important searchable keywords.

Do not use meaningless names such as:

```
note1.md
SAP学习.md
new.md
```

If an existing naming convention is visible in the repository, follow it.

---

# 23. Preserve Existing Notes

Never overwrite an existing note merely because the new topic appears similar.

Before creating a note:

1. Search for potentially related existing notes.
2. Determine whether the new information should:
    - become a new note,
    - extend an existing note,
    - or remain a separate note with a relationship link.

If modifying an existing note is necessary, preserve the user's existing content unless the user explicitly asks for rewriting.

## Related Note Placement and Deduplication

Before writing, search existing notes by filename, headings, keywords, technical objects, and concepts. Apply the following priority:

1. If the topic is already covered by an existing level-1 or level-2 heading, extend that heading with only the new information.
2. If the topic clearly belongs to an existing note but has no suitable heading, add a concise new level-1 or level-2 heading within that note.
3. If several notes are related, choose one primary note for the content and add meaningful links to secondary notes; do not copy the same explanation into every related note.
4. If no relevant note exists, create a new note in the directory determined from the relevant index or folder structure.

If the material about to be recorded duplicates or is equivalent to content already in a note, add only the new information under the original note, item, or relevant heading. Do not record fully identical content again or create a duplicate item or note.

Do not record explanations, code, operation steps, or screenshots that are already present. Preserve existing wording and screenshots unless the new material corrects or materially extends them. Reuse an existing embedded image when it refers to the same screenshot; if a new accessible screenshot is needed, copy it into the appropriate `Assets` folder and embed it directly. Use a new placeholder only when the actual image is unavailable.

---

# 24. Note Generation Process

Follow this sequence:

```
Step 1
Read the completed SAP discussion.

↓

Step 2
Identify the actual knowledge worth preserving.

↓

Step 3
Determine SAP module/product/technology/domain.

↓

Step 4
Determine whether it is:
- operation knowledge
- configuration knowledge
- development knowledge
- debugging knowledge
- conceptual knowledge
- troubleshooting knowledge
- mixed knowledge

↓

Step 5
Search existing notes for related concepts, filenames, headings, and keywords.

↓

Step 6
Choose the primary existing note and its most relevant level-1 or level-2 heading. If no related note exists, determine the appropriate directory from the user's index or folder structure. For a new note, count the actual level-1 and level-2 headings and add a directory unless their combined count is no more than two.

↓

Step 7
Write the note in the user's style.

↓

Step 8
Insert code blocks.

If the discussion includes Quick Fix or a similar automatic operation, apply Section 10.1: provide the direct code solution first when feasible and explain the code in the note.

↓

Step 9
For each accessible screenshot or image, first apply the multi-image code-extraction and deduplication rules in Section 11.1. Convert accurately readable code/text/structured content where appropriate; then copy only the images that still provide meaningful visual value into the appropriate `Assets` folder. Choose and verify each embed using Section 11.2; confirm it renders in Obsidian when available. Use `[图片：...]` only when the actual image is unavailable.

↓

Step 10
Do not add internal note-to-note links by default. Add the minimum direct link only when a specific dependency, operation detail, or evidence in another note is necessary to understand, verify, or use this note. Use existing indexes/Canvas for general navigation; omit optional “related” and review links.

↓

Step 11
Add useful external references when applicable.

↓

Step 12
Check factual accuracy and distinguish confirmed facts from assumptions.

↓

Step 13
Save the merged content in the selected existing note, or save a new note in the appropriate directory determined from the user's index or folder structure.

↓

Step 14
Report the created note and its classification.
```

---

# 25. Final Quality Check

Before finishing, verify:

## Classification

- Is the SAP module/product/technology correctly identified?
- Was the classification unnecessarily restricted?
- If multiple domains are involved, are they represented?

## Structure

- Does the heading hierarchy match the type of note?
- Was a directory added when the actual level-1 and level-2 heading count is greater than two?
- Was the directory omitted only when that count is no more than two?
- Are T-codes searchable?

## Content

- Did the note preserve the actual problem?
- Did it preserve the actual solution?
- Did it preserve important technical evidence?
- Did it avoid unnecessary textbook material?

## Code

- Is all important code inside code blocks?
- Were useful code comments preserved?
- If Quick Fix or a similar automatic operation was mentioned, was a direct code solution provided first when feasible?
- Does the note explain the corresponding code and why it solves the problem?
- If Quick Fix was retained, was the reason and generated code recorded?

## Images

- Were accessible screenshots copied into the appropriate `Assets` folder?
- Were copied images embedded using a link format valid for the active Vault, with the path checked against its root and existing working embeds?
- Was each image confirmed to render in Obsidian, or clearly marked as unverified when only the disk path could be checked?
- When many images were provided, was readable code/text/structured content extracted and consolidated to reduce unnecessary images?
- Were flowcharts, UI/画面图, structure/architecture diagrams, and other inherently visual content appropriately preserved as images?
- Were temporary or unstable image paths avoided?
- Were placeholders used only when the actual image was unavailable?
- Was any image content fabricated?

## Links

- Are related notes linked where genuinely useful?
- Does each note-to-note link support a concrete concept, operation, dependency, or evidence path rather than mere topical similarity?
- Are category indexes handling general navigation, with sibling-note links limited to specific useful relationships?
- Were genuinely useful direct links retained instead of omitted or replaced by a broad index just to make the graph sparse?
- Were redundant link lists, repeated links, and reverse links added only for symmetry removed?
- Were nonexistent note names avoided?

## External sources

- Are external references separated from personal experience?
- Is `## 外部参考` omitted when there are no external links to preserve?
- Are links preserved where useful?

## Accuracy

- Were assumptions kept separate from confirmed facts?
- Was missing information marked as `[待确认]`?

## File handling

- Was the note placed at the top-level notes directory?
- Were unrelated files untouched?
- Was existing content preserved?

---

# 26. Output Style After Note Creation

After creating the note, provide a concise confirmation.

Example:

```
已创建笔记：

文件：
RAP Validation错误消息不显示.md

领域：
SAP RAP / OData V4 / Fiori Elements

类型：
问题排查

关联笔记：仅在必须跳转查看具体细节时列出；无需时省略此项。

已添加：
- 代码块
- 图片占位
- 必要时才添加的内部链接
```

Do not reproduce the entire note in the final response unless the user asks to review it.

---

# Final Principle

The most important rule of this Skill is:

> **不要替用户写“漂亮的SAP教材”，而是把用户刚刚解决的问题，整理成用户以后真的能拿来复习和解决问题的个人SAP笔记。**

The note should preserve the user's practical knowledge, terminology, operation path, code, evidence, screenshots, and relationships to existing knowledge.

When uncertain, preserve the uncertainty rather than inventing information.
