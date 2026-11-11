# 🤖 Dataset-Informed RL for Grid-Based Autonomous Navigation

Performance comparison of **Q-Learning, SARSA, DQN and PPO** on a stochastic 8×8 grid-navigation environment whose obstacle density and action-slip noise are informed by the Kaggle [Autonomous Navigation Control Dataset](https://www.kaggle.com/datasets/freshersstaff/autonomous-navigation-control-dataset).

> MSc Data Science · MAT340 – Reinforcement Learning & Decision Making · SASTRA Deemed University

![Python](https://img.shields.io/badge/Python-3.10+-blue) ![Gymnasium](https://img.shields.io/badge/Gymnasium-green) ![SB3](https://img.shields.io/badge/Stable--Baselines3-orange) ![License](https://img.shields.io/badge/License-MIT-green)

## 🎯 Overview
The dataset has no reward/next-state/episode fields, so it cannot be used as a logged RL dataset. Instead, two of its fields inform a **simulator**:
- `Distance_to_Obstacle_m` (< 15 m threshold) → obstacle density (0.155)
- `Weather_Condition` → episode-level action-slip probability (mean 0.107, via an explicit *assumed* mapping)

## 🌍 Environment
- 8×8 grid, fixed map (seed 123), 7 obstacles, start (0,0) → goal (7,7)
- 4 discrete actions, 100-step episode limit
- Rewards: **+100** goal · **−50** collision · **−3** out of bounds · **−1** per move

## 🧪 Experiments
60,000 environment steps per algorithm × 3 seeds (0, 1, 2); each policy evaluated greedily for 100 episodes.

## 📊 Results (mean ± std over 3 seeds, evaluation success rate)
| Algorithm | Success rate | Train time (CPU) |
|---|---|---|
| **SARSA** | **0.827 ± 0.040** | ~2 s |
| DQN | 0.810 ± 0.022 | ~133 s |
| Q-Learning | 0.580 ± 0.396 | ~2 s |
| PPO | 0.257 ± 0.363 | ~70 s |

SARSA ranks first, but its lead over DQN (0.017) is smaller than the seed-to-seed variation, so results are **indicative, not statistically conclusive**. The weather-to-slip mapping is a modelling assumption; results do not describe real vehicles or robots.

## 📁 Repository structure
```
├── notebooks/RL_Grid_Navigation.ipynb        # full experiment
├── report/RL_Grid_Navigation_Report.pdf      # complete written report
├── requirements.txt
└── README.md
```

## 🚀 How to run
```bash
git clone https://github.com/abirami-1506/rl-grid-navigation.git
cd rl-grid-navigation
pip install -r requirements.txt
jupyter notebook notebooks/RL_Grid_Navigation.ipynb
```
The notebook downloads the dataset via `kagglehub` (a Kaggle account/API token may be required) and writes CSV/JSON results to `outputs/`.

## 🛠 Tech stack
Python · Gymnasium · Stable-Baselines3 · PyTorch · pandas · NumPy · Matplotlib

## 👩‍💻 Author
**Abirami B** – M.Sc. Data Science, SASTRA Deemed University

## 📄 License
MIT
