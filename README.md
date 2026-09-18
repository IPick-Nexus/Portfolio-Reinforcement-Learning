# Reinforcement Learning

Stock-picking agents that improve from realized market feedback. Two agents are specified to start, with room for more.

## Overview

Each agent selects stocks, records the buy, waits a feedback window, and uses the realized return over that window as the reward to improve future picks.

### Agents

**Power picks** — the dominant stock within a track: well-known, fast-growing, the "most powerful" name in its space (e.g. NVIDIA in compute chips). Lower risk, more modest growth ceiling. Allocated **~1% of portfolio weight** per pick.

**Hidden gems** — smaller, less-known companies with breakout potential: underdogs, high volatility, higher risk. Allocated **~0.5% of portfolio weight** per pick.

**Additional (planned):** a pump-and-dump / short-target agent that flags likely-fraudulent names (e.g. a stock that 10x'd on nothing) as short candidates.

## How it works

1. Define each agent's candidate universe — power picks: dominant stock per track; hidden gems: small, high-volatility names.
2. Set allocation weights — ~1% per power pick, ~0.5% per hidden gem.
3. Bootstrap the policy on historical data via the backtesting harness.
4. Make picks, record the buy, and start the feedback window (1 week to a few weeks).
5. Collect the realized return over that window as the reward signal.
6. Update the policy from the reward, then repeat.

## Tech stack

- **Language:** Python
- **RL / agent framework:** TBD
- **Market data:** weekly price feed for the feedback signal
- **Offline training:** backtesting harness over historical data

## Getting started

\`\`\`bash
git clone <repo-url>
cd rl-agents

python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
\`\`\`

> Fill in `requirements.txt` once the RL framework is chosen (e.g. `stable-baselines3`), plus `pandas`, `numpy`, and a backtesting library.

## Suggested project structure

\`\`\`
rl-agents/
├── src/
│   ├── agents/
│   │   ├── power_picks.py
│   │   ├── hidden_gems.py
│   │   └── short_target.py   # planned
│   ├── env.py                # candidate universe + reward from realized return
│   ├── train.py              # offline bootstrap on historical data
│   └── feedback.py           # collect realized returns over the window
├── data/                     # historical price data
├── requirements.txt
└── README.md
\`\`\`

## Roadmap

- [ ] Choose the RL / agent framework
- [ ] Define candidate universes for each agent
- [ ] Reward = realized return over the feedback window
- [ ] Offline bootstrap on historical data (backtesting)
- [ ] Live feedback loop + policy updates
- [ ] Short-target agent

## Resources

- Hugging Face — Deep RL Course (free, 8 units, hands-on with Stable-Baselines3): https://huggingface.co/learn/deep-rl-course/en/unit0/introduction
- Sutton & Barto — *Reinforcement Learning: An Introduction* (the standard reference; free PDF from the authors)
- backtesting.py — docs & quick-start guide for the backtesting harness: https://kernc.github.io/backtesting.py/