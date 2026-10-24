# Agent Skills Collection

一组面向 Codex 的可复用 Skills，涵盖 SAP、AI、日本簿记、Obsidian 笔记，以及少量需要配套项目或桌面工具的工作流。Skills 是给 AI agent 使用的说明包，不是独立应用；每个技能的入口文件是 `SKILL.md`，可选的 `agents/`、`references/` 和 `assets/` 文件也应一起保留。

## 快速安装

先在 GitHub 页面点 **Code → Download ZIP** 并解压，然后在解压后的仓库根目录打开终端。下面的脚本会把所有 Skills 安装到当前用户目录；已存在同名目录时会跳过，避免覆盖已有配置。

### Windows（PowerShell）

```powershell
$repo = (Get-Location).Path
$sourceRoot = Join-Path $repo '02 skills'
$destinationRoot = Join-Path $HOME '.agents\skills'
$sharedReference = Join-Path $sourceRoot '_shared\obsidian-note-taking-reference.md'

if (-not (Test-Path -LiteralPath $sourceRoot)) {
    throw '请先切换到仓库根目录再运行。'
}
New-Item -ItemType Directory -Force -Path $destinationRoot | Out-Null

Get-ChildItem -LiteralPath $sourceRoot -Recurse -Filter 'SKILL.md' | ForEach-Object {
    $source = $_.Directory
    $name = $source.Name
    $target = Join-Path $destinationRoot $name

    if (Test-Path -LiteralPath $target) {
        Write-Warning "跳过已存在的 Skill：$name（如需更新，请先备份并处理旧目录）"
    } else {
        New-Item -ItemType Directory -Force -Path $target | Out-Null
        Get-ChildItem -LiteralPath $source.FullName -Force | ForEach-Object {
            Copy-Item -LiteralPath $_.FullName -Destination $target -Recurse -Force
        }
        if ($name -like 'note-taking-*') {
            Copy-Item -LiteralPath $sharedReference -Destination (Join-Path $target 'obsidian-note-taking-reference.md')
        }
        Write-Host "已安装：$name"
    }
}
```

### macOS / Linux（Bash）

在仓库根目录运行：

```bash
set -euo pipefail
repo="$(pwd)"
source_root="$repo/02 skills"
destination_root="$HOME/.agents/skills"
shared_reference="$source_root/_shared/obsidian-note-taking-reference.md"

if [[ ! -d "$source_root" ]]; then
  echo '请先切换到仓库根目录再运行。' >&2
  exit 1
fi
mkdir -p "$destination_root"
while IFS= read -r -d '' skill_file; do
  source="${skill_file%/SKILL.md}"
  name="$(basename "$source")"
  target="$destination_root/$name"
  if [[ -e "$target" ]]; then
    printf '跳过已存在的 Skill：%s\n' "$name"
    continue
  fi
  mkdir -p "$target"
  cp -R "$source/." "$target/"
  if [[ "$name" == note-taking-* ]]; then
    cp "$shared_reference" "$target/obsidian-note-taking-reference.md"
  fi
  printf '已安装：%s\n' "$name"
done < <(find "$source_root" -type f -name 'SKILL.md' -print0)
```

需要只安装一个时，复制对应的 Skill 文件夹到 `~/.agents/skills/`。例如，把 `02 skills/answering/sap-abap-agent/` 整个目录复制到 `~/.agents/skills/sap-abap-agent/`。若安装的是 `note-taking-*`，还要把 `02 skills/_shared/obsidian-note-taking-reference.md` 复制到目标 Skill 目录下。

安装后让 Codex 刷新 Skills；如果列表里还没有出现，重启 Codex。Codex 也支持把 Skill 放在项目的 `.agents/skills/` 中，让它只在该项目可用。安装位置和 Skill 的结构说明见[官方 Build skills 文档](https://learn.chatgpt.com/docs/build-skills)。

## 使用方式

- 在 Codex CLI 或 IDE 扩展中，可输入 `$` 并选择 Skill，例如 `$sap-abap-agent`；也可以直接描述任务，让 Codex 按 Skill 的 `description` 判断是否启用。
- 在支持 Skills 的 Codex 客户端中查看已发现的 Skills；若任务与某个 Skill 的描述相符，Codex 也可能自动选择它。
- 一个 Skill 没出现时，先确认目标文件夹的根部有 `SKILL.md`，再确认安装位置正确并重启 Codex。

## Skill 导览

| Skill | 适用场景 | 使用前要知道 |
| --- | --- | --- |
| [ai-knowledge-guide](02%20skills/answering/ai-knowledge-guide/SKILL.md) | AI、机器学习、论文、实验与工程问题 | 可先检索使用者自己的 AI 笔记；没有笔记时按问题和证据继续回答。 |
| [japanese-bookkeeping-guide](02%20skills/answering/japanese-bookkeeping-guide/SKILL.md) | 日本簿记和日本会计问题 | 可结合使用者自己的日本簿记笔记；税务或法律问题需要单独核验。 |
| [sap-abap-agent](02%20skills/answering/sap-abap-agent/SKILL.md) | SAP、ABAP、RAP 诊断 | 附带 `references/`；若有自己的 SAP 笔记，可配置为补充资料。 |
| [note-taking-ai](02%20skills/note-taking/note-taking-ai/SKILL.md) | 整理 AI 学习资料为 Obsidian 笔记 | 需要一个 Obsidian vault；安装脚本会附带共享记笔记规范。 |
| [note-taking-japanese-bookkeeping](02%20skills/note-taking/note-taking-japanese-bookkeeping/SKILL.md) | 整理日本簿记资料、分录和计算 | 需要一个 Obsidian vault；默认以日语组织笔记。 |
| [note-taking-sap](02%20skills/note-taking/note-taking-sap/SKILL.md) | 把已解决的 SAP 问题整理成笔记 | 需要一个 Obsidian vault；安装脚本会附带共享记笔记规范。 |
| [sap-course-capture](02%20skills/sap-course-capture/SKILL.md) | 学习 SAP Learning 课程 | 需要课程访问权限及可用的浏览器/截图能力；素材保存路径按自己的设备配置。 |
| [novel-audio-video-pipeline](02%20skills/media-production/novel-audio-video-pipeline/SKILL.md) | Word 小说转中文配音视频并准备投稿 | 需要 Word、配音/剪辑工具和自己的视频账号；运行前设置输入、背景视频、导出路径、头像，并检查配音、字幕、标签和排期是否适合自己。发布与定时投稿须由当前使用者授权。 |
| [household-bookkeeping](02%20skills/answering/household-bookkeeping/SKILL.md) | 家庭账本操作和核对 | 面向配套记账项目；本仓库不包含该应用、账本数据库或用户配置。使用者应先检查并改好项目文档和账务规则。 |
| [household-bookkeeping-software](02%20skills/answering/household-bookkeeping-software-v0-2/SKILL.md) | 家庭记账软件中的自然语言解析 | 仅供包含兼容解析器的记账软件内部使用，不是通用聊天记账 Skill。 |

共享 Obsidian 规范的原始文件位于 [`02 skills/_shared/`](02%20skills/_shared/obsidian-note-taking-reference.md)。安装脚本会把它复制到三个笔记 Skill 旁边，使安装后的 Skill 可以单独读取。更新共享规范时，也要同步更新这三个已安装副本。

## 使用者需要配置的内容

- 检索类 Skills 可结合自己的笔记库；不同使用者的目录结构不同，使用前应确认 Codex 能访问自己的笔记目录。
- 小说视频工作流中的 `{NOVEL_INPUT_DIR}`、`{BACKGROUND_VIDEO_FILE}`、`{VIDEO_OUTPUT_DIR}` 和 `{BILIBILI_AVATAR_REFERENCE}` 是占位符。请换成自己有权使用的路径和素材，不要沿用原作者设备上的位置。本仓库不分发原作者的头像参考图；请提供自己的账号参考图。上传、投稿或定时发布前，需要当前使用者明确授权。
- SAP 课程采集 Skill 是进阶工作流，需要 SAP Learning 访问权限、浏览器/截图能力，以及处理分段交接的工作环境；它会把截图和字幕写到当前使用者选择的本地目录。不要把浏览器登录信息、访问令牌或私人课程文件提交到公开仓库。
- 家庭记账 Skills 不附带真实账本或账户数据。第一次用于自己的记账项目时，先阅读该项目的 `AGENTS.md`、迁移说明和软件说明，并确认账户、币种、账期及账务规则。

## 许可证

本仓库内容采用 [MIT License](LICENSE)。你可以使用、修改、再发布本仓库内容，也可以将其用于商业用途；请保留版权声明和许可证文本。完整条款见 [`LICENSE`](LICENSE)。
