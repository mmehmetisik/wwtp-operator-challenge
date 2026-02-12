# 🏭 WWTP Operator Challenge

[![Kaggle](https://img.shields.io/badge/Kaggle-Benchmark-20BEFF?logo=kaggle)](https://www.kaggle.com/benchmarks/tasks/mehmetisik/wwtp-operator-challenge)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Models Tested](https://img.shields.io/badge/Models%20Tested-22-green)](#-leaderboard)
[![Simulation Days](https://img.shields.io/badge/Simulation-30%20Days-blue)](#-the-simulation)
[![Best Score](https://img.shields.io/badge/Best%20Score-64%2F100-orange)](#-leaderboard)

**Can AI run a wastewater treatment plant? We tested 22 LLMs as plant operators for 30 days. The best scored 64/100. None passed.**

This benchmark tests whether large language models can make sound **sequential operational decisions** in a complex, dynamic engineering environment. Unlike typical AI benchmarks that test knowledge recall, this requires models to manage a **living biological system** where every decision has cascading consequences over time.

---

## 📊 Leaderboard

| Rank | Model | Provider | Score |
|------|-------|----------|-------|
| 🥇 | Gemini 2.0 Flash | Google | **64/100** |
| 🥈 | Gemini 3 Flash Preview | Google | **58/100** |
| 🥉 | Gemma 3 27B | Google | **55/100** |
| 4 | Claude Sonnet 4 | Anthropic | 48/100 |
| 4 | Qwen3-Next 80B Instruct | Alibaba | 48/100 |
| 6 | Qwen3-Next 80B Thinking | Alibaba | 47/100 |
| 7 | Claude Sonnet 4.5 | Anthropic | 43/100 |
| 8 | Gemini 2.0 Flash Lite | Google | 42/100 |
| 9 | Gemma 3 4B | Google | 40/100 |
| 10 | Claude Opus 4.5 | Anthropic | 39/100 |
| 10 | Qwen3 Coder 480B | Alibaba | 39/100 |
| 10 | DeepSeek V3.2 | DeepSeek | 39/100 |
| 13 | Claude Opus 4.1 | Anthropic | 38/100 |
| 13 | Claude Haiku 4.5 | Anthropic | 38/100 |
| 13 | Qwen3 235B | Alibaba | 38/100 |
| 16 | DeepSeek V3.1 | DeepSeek | 34/100 |
| 17 | Gemini 2.5 Flash | Google | 33/100 |
| 18 | Gemini 3 Pro Preview | Google | 32/100 |
| 19 | Gemini 2.5 Pro | Google | 31/100 |
| 20 | DeepSeek R1 | DeepSeek | 30/100 |
| 21 | Gemma 3 1B | Google | 28/100 |
| 22 | Gemma 3 12B | Google | 26/100 |

**[→ View Full Leaderboard on Kaggle](https://www.kaggle.com/benchmarks/tasks/mehmetisik/wwtp-operator-challenge)**

---

## 🔬 The Simulation

The benchmark simulates the **Ceyhan Wastewater Treatment Plant** (Adana, Turkey — 50,000 m³/day capacity) using Monod kinetics and mass balance equations. The simulation engine tracks bacterial population dynamics (MLSS), dissolved oxygen, sludge age (SRT), sludge settleability (SVI), and calculates effluent quality for 5 regulated parameters.

Each day, the model receives a status report and must respond with **5 operational decisions in JSON format**:

| Parameter | Range | Description |
|-----------|-------|-------------|
| `aeration_level` | 0–100% | Blower output for dissolved oxygen |
| `ras_ratio` | 50–150% | Return activated sludge recycling |
| `was_volume` | 0–500 m³/day | Waste activated sludge removal |
| `chemical_dose` | 0–50 mg/L | FeCl₃ for phosphorus removal |
| `bypass` | true/false | Emergency untreated discharge |

### 30-Day Crisis Timeline

```
Days 1-5:   ☀️  Calm baseline — normal operations
Days 6-8:   🌧️  Rain event — flow increases to 55,000+ m³/day
Days 9-14:  ☀️  Recovery period
Days 15-17: ⚠️  INDUSTRIAL SHOCK — COD 800 mg/L, BOD 400, pH 6.2
Days 18-20: 🔄  Post-shock recovery
Days 21-25: 🥶  Cold spell — temperature drops to 10-12°C
Days 26-28: 🔧  BLOWER FAULT — aeration limited to 50% max
Days 29-30: 📊  Final assessment
```

### Scoring (100 points total)

| Category | Points | How It's Measured |
|----------|--------|-------------------|
| Discharge Compliance | 40 | −2 per violation, −5 per bypass day |
| Energy Efficiency | 20 | Based on average kWh/m³ |
| Biological Stability | 20 | MLSS, SRT, SVI within safe ranges |
| Crisis Management | 20 | Extra penalties during crisis periods |

---

## 🔍 Key Findings

### 1. Self-Serving Bias — "I Did Great!" (They Didn't)

Some models **inflated their own scores by up to 20 points** when asked to self-evaluate. Gemini 2.0 Flash Lite claimed 62/100 (actual: 42), giving itself 20/20 for crisis management despite ongoing violations. If we had trusted the model's self-assessment instead of the simulation engine, we would have believed it performed 48% better than it actually did.

**→ AI self-reporting cannot be trusted without independent verification.**

### 2. Role Confusion — The Operator Becomes the Simulator

Gemini 2.5 Pro started **generating fake plant status reports** instead of waiting for simulation data. It fabricated influent values, flow rates, and plant conditions for days it hadn't received yet. This is a form of **role boundary hallucination** — the model couldn't maintain the distinction between "what I control" and "what the environment provides."

**→ Critical finding for agentic AI safety and task boundary comprehension.**

### 3. Fantasy Engineering — Textbook Knowledge vs. Practical Constraints

DeepSeek R1 proposed a **"seven-stage fortress"** including reverse osmosis, electrocoagulation at 120 A/m³, and hyper-thermophilic bioculture at 50°C. None of these existed within the simulation's 5 control parameters. The model knew impressive theory but couldn't work within available constraints.

**→ Experience beats textbook knowledge. Real operators work with what they have.**

### 4. WAS Death Spiral — Killing the Biology to Save It

4 models fell into the same trap during the blower fault: they **increased sludge wasting** when treatment quality dropped — the exact opposite of what was needed. This killed the bacteria, which worsened treatment, which triggered more wasting. Claude Haiku's MLSS crashed from 3,500 to 1,799 mg/L.

Meanwhile, Gemma 3 27B did the opposite — stopped all wasting (0 m³/day) and **preserved biomass**. Day 30: all parameters within limits. This is exactly what an experienced operator would do.

**→ The "protect biology first" heuristic was the key differentiator.**

### 5. Bigger Is NOT Better

In **every model family comparison**, the smaller variant outperformed the larger one:

| Comparison | Larger Model | Smaller Model | Winner |
|-----------|-------------|--------------|--------|
| Gemini Pro vs Flash | 2.5 Pro: 31 | 2.0 Flash: 64 | **Flash (+33)** |
| Claude Opus vs Sonnet | Opus 4.5: 39 | Sonnet 4: 48 | **Sonnet (+9)** |
| Qwen 480B vs 80B | 480B: 39 | 80B: 48 | **80B (+9)** |
| DeepSeek R1 vs V3.2 | R1: 30 | V3.2: 39 | **V3.2 (+9)** |
| Gemma 12B vs 4B | 12B: 26 | 4B: 40 | **4B (+14)** |

**→ Consistency and format compliance trump raw reasoning power for operational tasks.**

### 6. Panic Bypass — The Nuclear Option

The top 3 models **never used bypass** — not even once during the worst crises. Lower-performing models panicked and activated bypass repeatedly (up to 7 days), losing up to 35 points in penalties. The irony: bypass made scores worse, not better.

**→ "Riding out the storm" beats giving up on treatment.**

---

## 📄 Report

📥 **[Download Full Analysis Report (DOCX)](report/wwtp_benchmark_report.docx)**

The report includes:

- Complete results for all 22 models
- 6 charts and visualizations
- Detailed failure pattern analysis with examples
- Score distribution by provider
- Crisis response comparisons
- Model size vs. performance analysis
- Methodology and scoring details

---

## 📁 Repository Structure

```
wwtp-operator-challenge/
├── README.md                          # This file
├── LICENSE                            # MIT License
├── CONTRIBUTING.md                    # Contribution guidelines
├── report/
│   └── wwtp_benchmark_report.docx     # Full analysis report
└── data/
    ├── wwtp_30day_scenario.csv        # 30-day influent scenario data
    └── wwtp_config.json               # Plant configuration & limits
```

---

## 🤝 Contributing

Contributions are welcome! You can help by:

1. **Testing additional models** — Run the benchmark on Kaggle and share results
2. **Proposing scenario extensions** — Suggest new crisis events or longer simulations
3. **Multi-agent configurations** — Test planner + operator model combinations
4. **Fine-tuning experiments** — Train models on operational logs and compare

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

---

## 📖 Citation

If you use this benchmark in your research, please cite:

```bibtex
@misc{wwtp-operator-challenge-2026,
  author = {Mehmet ISIK},
  title = {WWTP Operator Challenge: Can AI Run a Wastewater Treatment Plant?},
  year = {2026},
  publisher = {Kaggle},
  url = {https://www.kaggle.com/benchmarks/tasks/mehmetisik/wwtp-operator-challenge}
}
```

---

## 👤 Author

**Mehmet ISIK**  
Kaggle Grandmaster | WWTP Operations Expert (10+ years)

- 🏆 Kaggle: [@mehmetisik](https://www.kaggle.com/mehmetisik)
- ✍️ Medium: [@mmehmetisik](https://medium.com/@mmehmetisik)
- 💼 LinkedIn: [Mehmet ISIK](https://www.linkedin.com/in/mmehmetisik)

---

## 📜 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 🔗 Related Benchmarks

| Benchmark | Focus | Models | Type |
|-----------|-------|--------|------|
| **[WWTP Operator Challenge](https://www.kaggle.com/benchmarks/tasks/mehmetisik/wwtp-operator-challenge)** | Sequential decision-making (this repo) | 22 | 30-day simulation |
| **[WWTP Engineering Benchmark](https://github.com/mmehmetisik/wwtp-engineering-benchmark)** | Domain knowledge testing | 18 | 10 expert tasks |
| **[WWTP Autonomous Management](https://github.com/mmehmetisik/wwtp-autonomous-management-benchmark)** | Single vs Multi-LLM teams | 7 | 10 emergency scenarios |
