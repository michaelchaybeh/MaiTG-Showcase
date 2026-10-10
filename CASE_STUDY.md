# MaiTG — AI-Powered Telegram Communication System

**Product:** MaiTG (Mai = My / My AI; TG = Telegram)
**Role:** Sole Creator & Developer
**Development:** Hands-on, AI-assisted engineering
**Stack:** Python, FastAPI, Telethon, ChatGPT, MCP, Auth0, Render
**Status:** Operational, October 2026

## 1. The Problem

I created MaiTG to make Telegram communication easier to manage
with AI.

Important information was spread across customer, partner,
and project conversations. Reviewing histories, searching
for decisions, and preparing responses required manual effort.

I wanted ChatGPT to work with relevant Telegram data directly,
without repeatedly copying conversation histories into it.

## 2. What I Built

MaiTG is a Telegram-to-AI communication system built around:

- A Python backend using Telethon for Telegram connectivity.
- A FastAPI REST interface for structured data retrieval.
- A ChatGPT integration, initially using custom GPT actions.
- A dedicated MCP adapter added as the product evolved.
- Auth0 OAuth and authenticated backend API access.
- Separate Render services for the backend and MCP adapter.

The system allows AI-assisted conversation review, search,
history retrieval, summaries, and contextual reply drafting.

The MCP tool interface is read-only. It cannot send, edit,
delete, or mark Telegram messages as read.

## 3. How I Developed It

I am the sole human developer of MaiTG. No other developer
implemented or independently reviewed the project.

My workflow combined direct technical execution with
AI assistance from ChatGPT.

I worked in Windows PowerShell and used Python, Git,
GitHub CLI, Render CLI, and other command-line tools.

The development loop was:

1. Define a feature, problem, or desired behavior.
2. Discuss the approach with ChatGPT.
3. Receive Python code, scripts, or PowerShell commands.
4. Execute the commands myself in my local environment.
5. Examine test output, logs, errors, and Git changes.
6. Share the results with ChatGPT for debugging.
7. Apply corrections and repeat until verified.
8. Commit, push, configure, and deploy the changes.

ChatGPT helped generate and explain code, identify potential
failure causes, prepare fixes, and construct test procedures.

I directed the work, operated the tools, managed deployment,
and remained responsible for the results.

## 4. Architecture

    ChatGPT
       |
    Auth0 OAuth
       |
    MaiTG MCP Adapter
       |
    Authenticated HTTPS
       |
    MaiTG FastAPI Backend
       |
    Telethon
       |
    Telegram

The Telegram backend and AI-facing MCP adapter run as
separate Render services.

## 5. Engineering Decisions

### Separate backend and MCP service

I retained the Telegram backend and built the MCP adapter
as a separate service instead of replacing the backend or
combining all responsibilities in one application.

This preserved the Telegram integration and allowed the
AI-facing interface to evolve independently.

### Structured tools instead of manual data copying

I used API endpoints and named AI tools to retrieve
Telegram data in a consistent, structured way.

### Authentication at two boundaries

Auth0 OAuth protects the MCP connection, while separate
backend authentication protects the Telegram REST API.

### Read-only AI operations

I limited the initial MCP interface to retrieval and
search rather than exposing message-writing operations.

This supports analysis and drafting while preserving
a clear boundary around actions affecting Telegram.

These decisions describe the implemented architecture.
They are not claims that every alternative underwent
formal benchmarking.

## 6. Problems Diagnosed and Resolved

### Telegram identifier mismatches

Telegram dialogs and peers can use different identifier
formats. Backend matching was updated to handle signed
dialog IDs and canonical peer IDs consistently.

Targeted privacy and identifier regression tests passed.

### Conversation privacy

Direct history retrieval and conversation discovery
required consistent exclusion handling.

Backend access and exclusion checks were strengthened
to reduce the risk of bypassing protected conversations.

### Timeouts

Some initial MCP requests timed out. The upstream HTTP
timeout was increased from 20 to 45 seconds.

Subsequent live tool calls returned data successfully.

### HTTP 429 responses

Some expensive Telegram requests encountered HTTP 429
errors. Safe response diagnostics were added without
logging tokens or private message contents.

Intermittent rate limiting remains a known limitation;
it was not conclusively eliminated.

### Telegram folders

A folder request failed because the backend requires
manually included peers for folder-chat retrieval.

Testing with a suitable folder succeeded. Support for
fully automatic folder membership remains future work.

## 7. Verified Results

Seven MCP tools passed initial live functional tests:

| Tool | Result |
|---|---|
| getTelegramFolders | 27 folders retrieved |
| searchTelegramChats | Request succeeded; zero test matches |
| getPendingMessages | 3 conversations retrieved |
| getChatHistory | 3 messages retrieved |
| getTelegramChatMessages | 3 messages retrieved |
| getFolderChats | 3 conversations retrieved |
| searchTelegramMessages | 3 matching messages retrieved |

Seven local backend privacy and peer-ID regression
tests also passed.

Auth0 authentication, backend connectivity, and Render
deployment were verified during integration testing.

These tests confirm initial functionality, not
exhaustive reliability or security certification.

## 8. Current Limitations

- No AI-triggered sending, editing, or deletion.
- No mark-as-read MCP operation.
- Automatically populated folders are not fully supported.
- Some requests have encountered intermittent HTTP 429.
- Backend dialog scanning may have configured limits.
- No independent human code review or external security audit.
- No formally measured time savings or commercial impact.

## 9. Evidence and Repository Scope

This public repository contains portfolio documentation
only. The production source repository remains private.

Selected engineering evidence from the private project:

- `telegram_assistant.py`: FastAPI/Telethon backend.
- `mcp_adapter/`: MCP integration.
- `mcp_adapter/test_privacy.py`: Privacy regression tests.
- `mcp_adapter/test_integration.py`: Integration test code.
- Backend privacy release: `9713a70`.
- Verified MCP application release: `3def961`.
- Final backend documentation deployment: `05e61bd`.

The original source history, Telegram session files,
tokens, environment configuration, and private messages
are deliberately not published.

Public demonstrations should use synthetic conversations
and sanitized screenshots.

## 10. Outcome

I independently built and deployed MaiTG as an
AI-powered Telegram communication system.

The project demonstrates Python backend development,
Telegram API integration, authenticated AI tool design,
MCP engineering, cloud operations, practical debugging,
and iterative AI-assisted software development.

The essential distinction is that I used ChatGPT
as a coding and technical guidance partner while
personally executing, testing, managing, and deploying
the system.

MaiTG is an original software project, not simply
a migration from one integration protocol to another.
