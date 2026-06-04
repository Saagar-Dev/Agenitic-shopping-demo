# Agenitic-shopping-demo

# 🌴 Kerala Kitchen — Multi-Agent Agentic AI Demo

> Two AI agents independently plan, shop, and cook a Kerala feast. Live. Right now. Using the Claude API.

[![Live Demo](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-brightgreen)](https://saagar-dev.github.io/Agentic-shopping-demo/)
[![Built with Claude](https://img.shields.io/badge/Powered%20by-Claude%20Haiku-blueviolet)](https://anthropic.com)
[![Agentic AI](https://img.shields.io/badge/Type-Multi--Agent-orange)](https://docs.anthropic.com)

---

## What Is This?

This demo shows **Agentic AI in action** — not a chatbot answering a question, but two autonomous AI agents making sequential decisions, using tools, and adapting to real-world constraints to complete a goal.

**Suchithra (Amma, 60)** and **Dolu (her daughter, 30)** are both powered by Claude Haiku. Each agent independently:

1. **Plans** a shopping list based on their assigned dishes and budget
2. **Navigates** a directed graph of Kerala market shops using A* pathfinding
3. **Buys** ingredients, managing a real budget and stamina meter
4. **Adapts** — if budget or stamina runs out, they head home immediately
5. **Cooks** their dishes once shopping is complete

Both agents run **in parallel** via `Promise.all`, sharing a live graph canvas but operating on isolated subgraphs.

---

## Why It's Interesting

| Concept | How It's Demonstrated |
|---|---|
| **Tool use** | Agents call `plan_shopping_list`, `walk_to_shop`, `buy_item`, `cook_dish` |
| **Multi-agent coordination** | Amma and Dolu run simultaneously with separate budgets, stamina, and shop routes |
| **Directed graph traversal** | 6 shops + 2 homes in a fully connected mesh; agents use A* shortest path |
| **Constraint adaptation** | Budget and stamina limits force real-time replanning |
| **Persistent state** | Trail system records every hop — full journey visible after mission |
| **Agentic loop** | Perceive → Reason → Act → Repeat, until goal achieved or resources exhausted |

---

## Architecture

```
┌─────────────────────────────────────────────────────┐
│                  Claude Haiku API                    │
│              (Tier 1 · 50 req/min)                  │
└──────────────┬──────────────────┬───────────────────┘
               │                  │
        Agent: Amma          Agent: Dolu
        Budget: ₹600         Budget: ₹400
        Stamina: 60          Stamina: 100
               │                  │
               ▼                  ▼
    ┌─────────────────────────────────────┐
    │       Directed Shop Graph           │
    │  Fish ─── Rice ─── Veg ─── Masala  │
    │       ╲     │    ╱    ╲    ╱       │
    │        Meat ─── Toddy              │
    │  home_a (Amma)    home_d (Dolu)    │
    └─────────────────────────────────────┘
```

**Key algorithms:**
- **A\* pathfinding** with Euclidean heuristic for shop-to-shop routing
- **Sequential hop queue** prevents duplicate animated dots
- **Per-agent adjacency graphs** — Amma can't use Dolu's routes and vice versa
- **visitedShops Set** prevents revisiting already-accessed nodes

---

## Tech Stack

- **Pure HTML/CSS/JS** — zero build step, zero dependencies
- **Claude Haiku API** — tool use with `plan_shopping_list`, `walk_to_shop`, `buy_item`, `cook_dish`
- **HTML5 Canvas** — custom graph renderer with glow, trails, sparkles, pulsating dots
- **A\* algorithm** — spatial pathfinding through the directed market graph

---

## Running Locally

```bash
# Clone and serve (required — file:// blocks CORS)
git clone https://github.com/saagar-dev/Agentic-shopping-demo
cd Agentic-shopping-demo
npx serve .
# Open http://localhost:3000
```

Enter your Anthropic API key in the intro popup, or set `const API_KEY = 'sk-ant-...'` at the top of the script.

---

## About

Built by **Saagar Devadiga** — Data Engineer & AI Developer, Brisbane, Australia.

Presented at the Snowflake Technical User Group Brisbane 2025.

---

---
