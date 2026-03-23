# Limit Order Book Simulation and Market Microstructure Analysis

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A complete implementation of a **limit order book** in Python, simulating the core mechanics of financial markets. The project demonstrates how limit and market orders interact, how bid‑ask spreads evolve, and how to compute key market microstructure metrics. It includes a random order flow simulation and visualises the dynamics of spread and mid‑price over time.

---

## Overview

This project builds a limit order book from scratch – the central component of any exchange. It processes:

- **Limit orders** that add liquidity to the book.
- **Market orders** that consume liquidity and execute immediately.
- **Cancellations** that remove orders from the book.

The simulation generates a stream of random orders (70% limit, 30% market) to observe how the book evolves, how the spread tightens or widens, and how the mid‑price moves. The output includes:

- The state of the book (best bid/ask, spread, depth) after each order.
- A list of executed trades with prices and quantities.
- Plots showing the evolution of the bid‑ask spread and the mid‑price.

---

## Features

- **Pure Python implementation** – no external financial data required.
- **Efficient data structures** – uses dictionaries for price levels and heaps (`heapq`) for fast best bid/ask retrieval.
- **Price‑time priority** – orders are matched by price, then time of arrival.
- **Marketable limit orders** – limit orders that cross the spread are executed immediately (like market orders).
- **Cancellation support** – partial or full cancellation of limit orders.
- **Metrics** – spread, mid‑price, depth, trade history, average trade price.
- **Simulation engine** – generates random order flow to stress‑test the book.
- **Visualisation** – plots the spread and mid‑price over the order sequence.

---

## How It Works

### Order Book Data Structure
- **Bids** (buy orders) are stored in a dictionary mapping price → total quantity, and a max‑heap (implemented with negative prices) to quickly get the highest bid.
- **Asks** (sell orders) are stored similarly, with a min‑heap for the lowest ask.
- When a new limit order arrives, it is first checked for marketability (i.e., a buy limit order with price ≥ best ask, or a sell limit order with price ≤ best bid). If marketable, it executes immediately; otherwise, it is added to the book.

### Matching Logic
- **Market buy** – consumes the lowest ask levels until the order is filled or the book runs out of asks.
- **Market sell** – consumes the highest bid levels.
- Each trade is recorded with price and quantity.

### Simulation
- Initial liquidity is seeded with a few limit orders.
- A loop generates random orders (limit or market, buy or sell, with random quantities).
- After each order, the current spread and mid‑price are recorded.
- After the simulation, the final book state and trade statistics are printed, and plots are generated.

---

## Output

Initial book: LOB: best bid=99.5, best ask=100.5, spread=1.0
Depth (bid, ask): (200, 300)

Final book state:
LOB: best bid=98.21, best ask=98.8, spread=0.5900000000000034
Total trades executed: 169
Average trade price: 99.73
