---
title: "How Claude Code works"
source: "https://code.claude.com/docs/en/how-claude-code-works"
author:
published:
created: 2026-06-05
description: "Understand the agentic loop, built-in tools, and how Claude Code interacts with your project."
tags:
  - "clippings"
---
Claude Code는 터미널에서 실행되는 에이전트형 도우미입니다. 코딩 작업에 탁월하지만, 문서 작성, 빌드 실행, 파일 검색, 주제 조사 등 명령줄에서 할 수 있는 거의 모든 작업을 지원합니다.

이 가이드에서는 핵심 아키텍처, 내장 기능 및 [효율적인 작업 팁을](#work-effectively-with-claude-code) 다룹니다. 단계별 진행 방법은 [일반적인 워크플로를](https://code.claude.com/docs/en/common-workflows) 참조하세요. 스킬, MCP, 훅과 같은 확장 기능에 대해서는 [Claude 코드 확장을](https://code.claude.com/docs/en/features-overview) 참조하세요.

## 에이전트 루프

클로드에게 작업을 맡기면, 클로드는 세 단계( **맥락 파악**, **조치 실행**, **결과 검증** )를 거쳐 작업을 진행합니다. 이 단계들은 서로 유기적으로 연결되어 있습니다. 클로드는 파일을 검색하여 코드를 이해하고, 편집하여 변경 사항을 적용하고, 테스트를 실행하여 결과를 검증하는 등 다양한 도구를 활용합니다.

![에이전트형 루프: 사용자의 요청에 따라 클로드는 상황을 파악하고, 조치를 취하고, 결과를 확인하고, 작업이 완료될 때까지 이 과정을 반복합니다. 언제든지 중단할 수 있습니다.](https://mintcdn.com/claude-code/c5r9_6tjPMzFdDDT/images/agentic-loop.svg?w=2500&fit=max&auto=format&n=c5r9_6tjPMzFdDDT&q=85&s=dfee4a0224b22047f2fecdaf8b3eba3e)

에이전트형 루프: 사용자의 요청에 따라 클로드는 상황을 파악하고, 조치를 취하고, 결과를 확인하고, 작업이 완료될 때까지 이 과정을 반복합니다. 언제든지 중단할 수 있습니다.

이 루프는 사용자의 질문에 맞춰 조정됩니다. 코드베이스에 대한 질문은 컨텍스트 수집만 필요할 수 있습니다. 버그 수정은 세 단계를 모두 반복적으로 거칩니다. 리팩토링은 광범위한 검증을 포함할 수 있습니다. 클로드는 이전 단계에서 얻은 정보를 바탕으로 각 단계에 필요한 작업을 결정하고, 수십 개의 작업을 연결하며 필요에 따라 수정합니다.

당신도 이 과정의 일부입니다. 언제든지 개입하여 클로드의 방향을 바꾸거나, 추가적인 맥락을 제공하거나, 다른 접근 방식을 시도하도록 요청할 수 있습니다. 클로드는 자율적으로 작동하지만 당신의 입력에 반응합니다.

에이전트 루프는 추론하는 [모델](#models) 과 실행하는 [도구 라는 두 가지 구성 요소에 의해 구동됩니다. Claude Code는 Claude를 둘러싼](#tools) **에이전트 기반 장치** 역할을 하며, 언어 모델을 유능한 코딩 에이전트로 전환하는 데 필요한 도구, 컨텍스트 관리 및 실행 환경을 제공합니다.

### 모델들

Claude Code uses Claude models to understand your code and reason about tasks. Claude can read code in any language, understand how components connect, and figure out what needs to change to accomplish your goal. For complex tasks, it breaks work into steps, executes them, and adjusts based on what it learns.

[Multiple models](https://code.claude.com/docs/en/model-config) are available with different tradeoffs. Sonnet handles most coding tasks well. Opus provides stronger reasoning for complex architectural decisions. Switch with `/model` during a session or start with `claude --model <name>`.

When this guide says “Claude chooses” or “Claude decides,” it’s the model doing the reasoning.

### Tools

Tools are what make Claude Code agentic. Without tools, Claude can only respond with text. With tools, Claude can act: read your code, edit files, run commands, search the web, and interact with external services. Each tool use returns information that feeds back into the loop, informing Claude’s next decision.

The built-in tools generally fall into five categories, each representing a different kind of agency.

| Category | What Claude can do |
| --- | --- |
| **File operations** | Read files, edit code, create new files, rename and reorganize |
| **Search** | Find files by pattern, search content with regex, explore codebases |
| **Execution** | Run shell commands, start servers, run tests, use git |
| **Web** | Search the web, fetch documentation, look up error messages |
| **Code intelligence** | See type errors and warnings after edits, jump to definitions, find references (requires [code intelligence plugins](https://code.claude.com/docs/en/discover-plugins#code-intelligence)) |

These are the primary capabilities. Claude also has tools for spawning subagents, asking you questions, and other orchestration tasks. See [Tools available to Claude](https://code.claude.com/docs/en/tools-reference) for the complete list.

Claude chooses which tools to use based on your prompt and what it learns along the way. When you say “fix the failing tests,” Claude might:

1. Run the test suite to see what’s failing
2. Read the error output
3. Search for the relevant source files
4. Read those files to understand the code
5. Edit the files to fix the issue
6. Run the tests again to verify

Each tool use gives Claude new information that informs the next step. This is the agentic loop in action.

**Extending the base capabilities:** The built-in tools are the foundation. You can extend what Claude knows with [skills](https://code.claude.com/docs/en/skills), connect to external services with [MCP](https://code.claude.com/docs/en/mcp), automate workflows with [hooks](https://code.claude.com/docs/en/hooks), and offload tasks to [subagents](https://code.claude.com/docs/en/sub-agents). These extensions form a layer on top of the core agentic loop. See [Extend Claude Code](https://code.claude.com/docs/en/features-overview) for guidance on choosing the right extension for your needs.

## What Claude can access

This guide focuses on the terminal. Claude Code also runs in [VS Code](https://code.claude.com/docs/en/vs-code), [JetBrains IDEs](https://code.claude.com/docs/en/jetbrains), and other environments.

When you run `claude` in a directory, Claude Code gains access to:

- **Your project.** Files in your directory and subdirectories, plus files elsewhere with your permission.
- **Your terminal.** Any command you could run: build tools, git, package managers, system utilities, scripts. If you can do it from the command line, Claude can too.
- **Your git state.** Current branch, uncommitted changes, and recent commit history.
- **Your [CLAUDE.md](https://code.claude.com/docs/en/memory).** A markdown file where you store project-specific instructions, conventions, and context that Claude should know every session.
- **[Auto memory](https://code.claude.com/docs/en/memory#auto-memory).** Learnings Claude saves automatically as you work, like project patterns and your preferences. The first 200 lines or 25KB of MEMORY.md, whichever comes first, load at the start of each session.
- **Extensions you configure.** [MCP servers](https://code.claude.com/docs/en/mcp) for external services, [skills](https://code.claude.com/docs/en/skills) for workflows, [subagents](https://code.claude.com/docs/en/sub-agents) for delegated work, and [Claude in Chrome](https://code.claude.com/docs/en/chrome) for browser interaction.

Because Claude sees your whole project, it can work across it. When you ask Claude to “fix the authentication bug,” it searches for relevant files, reads multiple files to understand context, makes coordinated edits across them, runs tests to verify the fix, and commits the changes if you ask. This is different from inline code assistants that only see the current file.

## Environments and interfaces

The agentic loop, tools, and capabilities described above are the same everywhere you use Claude Code. What changes is where the code executes and how you interact with it.

### Execution environments

Claude Code runs in three environments, each with different tradeoffs for where your code executes.

| Environment | Where code runs | Use case |
| --- | --- | --- |
| **Local** | Your machine | Default. Full access to your files, tools, and environment |
| **Cloud** | Anthropic-managed VMs | Offload tasks, work on repos you don’t have locally |
| **Remote Control** | Your machine, controlled from a browser | Use the web UI while keeping everything local |

### Interfaces

You can access Claude Code through the terminal, the [desktop app](https://code.claude.com/docs/en/desktop), [IDE extensions](https://code.claude.com/docs/en/vs-code), [claude.ai/code](https://claude.ai/code), [Remote Control](https://code.claude.com/docs/en/remote-control), [Slack](https://code.claude.com/docs/en/slack), and [CI/CD pipelines](https://code.claude.com/docs/en/github-actions). The interface determines how you see and interact with Claude, but the underlying agentic loop is identical. See [Use Claude Code everywhere](https://code.claude.com/docs/en/overview#use-claude-code-everywhere) for the full list.

## Work with sessions

Claude Code saves your conversation locally as you work. Each message, tool use, and result is written to a plaintext JSONL file under `~/.claude/projects/`, which enables [rewinding](#undo-changes-with-checkpoints), [resuming, and forking](#resume-or-fork-sessions) sessions. Before Claude makes code changes, it also snapshots the affected files so you can revert if needed. For paths, retention, and how to clear this data, see [application data in `~/.claude`](https://code.claude.com/docs/en/claude-directory#application-data).

**Sessions are independent.** Each new session starts with a fresh context window, without the conversation history from previous sessions. Claude can persist learnings across sessions using [auto memory](https://code.claude.com/docs/en/memory#auto-memory), and you can add your own persistent instructions in [CLAUDE.md](https://code.claude.com/docs/en/memory).

### Work across branches

Each Claude Code conversation is a session tied to your current directory. The `/resume` picker shows sessions from the current worktree by default, with keyboard shortcuts to widen the list to other worktrees or projects. See [Manage sessions](https://code.claude.com/docs/en/sessions#use-the-session-picker) for the full list of picker shortcuts and how name resolution works.

Claude sees your current branch’s files. When you switch branches, Claude sees the new branch’s files, but your conversation history stays the same. Claude remembers what you discussed even after switching.

Since sessions are tied to directories, you can run parallel Claude sessions by using [git worktrees](https://code.claude.com/docs/en/worktrees), which create separate directories for individual branches.

### Resume or fork sessions

Resuming a session with `claude --continue` or `claude --resume` reopens it under the same session ID and appends new messages to the existing conversation. Forking with `--fork-session` or `/branch` copies the history into a new session ID, leaving the original unchanged.

![세션 연속성: resume은 동일한 세션을 계속 유지하고, fork는 새로운 ID를 가진 새 브랜치를 생성합니다.](https://mintcdn.com/claude-code/c5r9_6tjPMzFdDDT/images/session-continuity.svg?w=2500&fit=max&auto=format&n=c5r9_6tjPMzFdDDT&q=85&s=d83b5f81e9d6d42d2bff0daa44d6a3ec)

세션 연속성: resume은 동일한 세션을 계속 유지하고, fork는 새로운 ID를 가진 새 브랜치를 생성합니다.

For the resume flags, the `/resume` picker, naming, and what happens when the same session is open in two terminals, see [Manage sessions](https://code.claude.com/docs/en/sessions).

### The context window

Claude’s context window holds your conversation history, file contents, command outputs, [CLAUDE.md](https://code.claude.com/docs/en/memory), [auto memory](https://code.claude.com/docs/en/memory#auto-memory), loaded skills, and system instructions. As you work, context fills up. Claude compacts automatically, but instructions from early in the conversation can get lost. Put persistent rules in CLAUDE.md, and run `/context` to see what’s using space.

For an interactive walkthrough of what loads and when, see [Explore the context window](https://code.claude.com/docs/en/context-window).

#### When context fills up

Claude Code manages context automatically as you approach the limit. It clears older tool outputs first, then summarizes the conversation if needed. Your requests and key code snippets are preserved; detailed instructions from early in the conversation may be lost. Put persistent rules in CLAUDE.md rather than relying on conversation history.

To control what’s preserved during compaction, add a “Compact Instructions” section to CLAUDE.md or run `/compact` with a focus (like `/compact focus on the API changes`).

If a single file or tool output is so large that context refills immediately after each summary, Claude Code stops auto-compacting after a few attempts and shows an error instead of looping. See [Auto-compaction stops with a thrashing error](https://code.claude.com/docs/en/troubleshooting#auto-compaction-stops-with-a-thrashing-error) for recovery steps.

Run `/context` to see what’s using space. MCP tool definitions are deferred by default and loaded on demand via [tool search](https://code.claude.com/docs/en/mcp#scale-with-mcp-tool-search), so only tool names consume context until Claude uses a specific tool. Run `/mcp` to check per-server costs.

#### Manage context with skills and subagents

Beyond compaction, you can use other features to control what loads into context.

[Skills](https://code.claude.com/docs/en/skills) load on demand. Claude sees skill descriptions at session start, but the full content only loads when a skill is used. For skills you invoke manually, set `disable-model-invocation: true` to keep descriptions out of context until you need them. For skills you didn’t write, use [`skillOverrides`](https://code.claude.com/docs/en/skills#override-skill-visibility-from-settings) to do the same from settings.

[Subagents](https://code.claude.com/docs/en/sub-agents) get their own fresh context, completely separate from your main conversation. Their work doesn’t bloat your context. When done, they return a summary. This isolation is why subagents help with long sessions.

See [context costs](https://code.claude.com/docs/en/features-overview#understand-context-costs) for what each feature costs, and [reduce token usage](https://code.claude.com/docs/en/costs#reduce-token-usage) for tips on managing context.

## Stay safe with checkpoints and permissions

Claude has two safety mechanisms: checkpoints let you undo file changes, and permissions control what Claude can do without asking.

### Undo changes with checkpoints

**Every file edit is reversible.** Before Claude edits any file, it snapshots the current contents. If something goes wrong, press `Esc` twice to rewind to a previous state, or ask Claude to undo.

Checkpoints are local to your session, separate from git. They only cover file changes. Actions that affect remote systems (databases, APIs, deployments) can’t be checkpointed, which is why Claude asks before running commands with external side effects.

### Control what Claude can do

Press `Shift+Tab` to cycle through permission modes:

- **Default**: Claude asks before file edits and shell commands
- **Auto-accept edits**: Claude edits files and runs common filesystem commands like `mkdir` and `mv` without asking, still asks for other commands
- **Plan mode**: Claude uses read-only tools only, creating a plan you can approve before execution
- **Auto mode**: Claude evaluates all actions with background safety checks. Currently a research preview

특정 명령어를 허용하면 `.claude/settings.json` Claude가 매번 묻지 않도록 설정할 수도 있습니다. [이는](https://code.claude.com/docs/en/permissions) \` `npm test` sudo `git status`...

---

## 클로드 코드와 효과적으로 협력하세요

이 팁들은 클로드 코드에서 더 나은 결과를 얻는 데 도움이 됩니다.

### 클로드 코드에게 도움을 요청하세요

클로드 코드는 사용법을 알려줍니다. "훅은 어떻게 설정하나요?" 또는 "CLAUDE.md 파일을 구성하는 가장 좋은 방법은 무엇인가요?"와 같은 질문을 하면 클로드가 설명해 줄 것입니다.

내장 명령어를 통해 설정 과정을 안내받을 수 있습니다.

- `/init` 이 문서에서는 프로젝트용 CLAUDE.md 파일을 만드는 과정을 안내합니다.
- `/agents` 사용자 지정 하위 에이전트를 구성하는 데 도움이 됩니다.
- `/doctor` 설치 과정에서 발생하는 일반적인 문제를 진단합니다.

### 대화입니다

클로드 코드는 대화형 방식입니다. 완벽한 프롬프트가 필요하지 않습니다. 원하는 것을 먼저 말하고, 그 다음 다듬어 나가세요.

```text
Fix the login bug
```

\[클로드가 조사하고, 무언가를 시도한다\]

```text
That's not quite right. The issue is in the session handling.
```

\[클로드가 접근 방식을 조정한다\]

첫 시도가 잘못됐다고 해서 처음부터 다시 시작하는 게 아닙니다. 반복 작업을 거치는 겁니다.

#### 중단하고 조종하세요

턴이 끝날 때까지 기다리거나 처음부터 다시 시작할 필요 없이 언제든지 클로드의 방향을 바꿀 수 있습니다.

- **이 버튼을 누르면 `Esc`** 클로드(Claude)가 즉시 중지됩니다. 실행 중인 도구 호출이 취소되고 클로드는 다음 지시를 기다립니다.
- **수정 사항을 입력하고 `Enter`** 전송 버튼을 누르면 실행 중인 도구가 중단되지 않습니다. 클로드는 현재 작업이 완료되는 즉시 수정 사항을 읽고 다음 단계를 결정하기 전에 조정합니다.

### 처음부터 구체적으로 밝히세요

처음 요청하는 내용이 구체적일수록 수정 횟수가 줄어듭니다. 특정 파일을 참조하고, 제약 조건을 언급하며, 예시 패턴을 제시하세요.

```text
The checkout flow is broken for users with expired cards.
Check src/payments/ for the issue, especially token refresh.
Write a failing test first, then fix it.
```

모호한 안내도 효과는 있지만, 방향을 제시하는 데 더 많은 시간을 소모하게 됩니다. 위와 같이 구체적인 안내는 첫 시도에 성공하는 경우가 많습니다.

### 클로드에게 검증할 수 있는 무언가를 주세요

Claude는 자체 작업을 검증할 수 있을 때 성능이 향상됩니다. 테스트 케이스를 포함하거나, 예상되는 UI의 스크린샷을 붙여넣거나, 원하는 출력 형식을 정의해 보세요.

```text
Implement validateEmail. Test cases: 'user@example.com' → true,
'invalid' → false, 'user@.com' → false. Run the tests after.
```

시각적인 작업을 위해 디자인의 스크린샷을 첨부하고 클로드에게 구현된 모습과 비교해 달라고 요청하세요.

### 실행하기 전에 먼저 살펴보세요.

복잡한 문제의 경우, 연구와 코딩을 분리하십시오. `Shift+Tab` 먼저 계획 모드(두 번)를 사용하여 코드베이스를 분석하십시오.

```text
Read src/auth/ and understand how we handle sessions.
Then create a plan for adding OAuth support.
```

계획을 검토하고, 대화를 통해 다듬은 다음, 클로드에게 실행을 맡기세요. 이러한 2단계 접근 방식은 코딩으로 바로 넘어가는 것보다 더 나은 결과를 가져옵니다.

### 지시하지 말고 위임하세요.

유능한 동료에게 업무를 위임하는 것을 생각해 보세요. 상황 설명과 방향을 제시한 다음, 클로드에게 세부 사항은 알아서 처리하도록 맡기세요.

```text
The checkout flow is broken for users with expired cards.
The relevant code is in src/payments/. Can you investigate and fix it?
```

어떤 파일을 읽어야 하는지, 어떤 명령어를 실행해야 하는지 지정할 필요가 없습니다. 클로드가 알아서 처리해 줍니다.

## 다음은 무엇인가요?

## [기능을 추가하여 확장하세요](https://code.claude.com/docs/en/features-overview)

스킬, MCP 연결 및 사용자 지정 명령을 추가합니다.

## [일반적인 워크플로](https://code.claude.com/docs/en/common-workflows)

일반적인 작업에 대한 단계별 가이드

[변경 로그](https://code.claude.com/docs/en/changelog) [클로드 코드 확장](https://code.claude.com/docs/en/features-overview)