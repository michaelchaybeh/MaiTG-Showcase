# MaiTG

**AI-Powered Telegram Communication System**

MaiTG is a custom-built AI communication system that connects Telegram with ChatGPT.

The name combines **Mai** (My / My AI) and **TG** (Telegram).

## What I Built

I designed, developed, tested, and deployed MaiTG as the sole human developer, with assistance from ChatGPT.

The system combines:

- Python and FastAPI backend
- Telethon integration with Telegram
- Authenticated REST API
- ChatGPT integration
- Model Context Protocol (MCP) adapter
- Auth0 OAuth authentication
- Cloud deployment on Render

## Development Process

I worked directly with Windows PowerShell, Python, Git, GitHub, and CLI tools.

ChatGPT helped generate code and PowerShell commands, explain implementations, debug errors, and plan testing.

I executed the commands, reviewed the results, made development decisions, and managed deployments myself.

No other human developer contributed to the project or independently reviewed its code.

## Architecture

ChatGPT -> Auth0 OAuth -> MaiTG MCP -> FastAPI -> Telethon -> Telegram

## Verified Features

Seven read-only MCP tools passed initial live tests:

- getPendingMessages
- getChatHistory
- getTelegramFolders
- getFolderChats
- searchTelegramChats
- searchTelegramMessages
- getTelegramChatMessages

Seven local backend privacy and identifier regression tests also passed.

## Security

The system uses OAuth authentication, authenticated backend requests, conversation exclusions, and read-only MCP permissions.

## Limitations

- No AI-triggered sending, editing, or deleting Telegram messages.
- Automatically populated Telegram folders are not fully supported.
- Some requests have encountered intermittent HTTP 429 errors.
- No independent third-party security audit has been performed.

## Repository Scope

This is a public portfolio showcase, not the production code repository.

The production source code, Git history, Telegram sessions, credentials, and private messages are intentionally excluded.

## Project Status

Operational as of October 2026.
