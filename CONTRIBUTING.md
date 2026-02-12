# Contributing to WWTP Operator Challenge

Thank you for your interest in contributing to this benchmark! Here are several ways you can help.

## 🧪 Testing Additional Models

The most valuable contribution is testing new models on the benchmark:

1. Go to the [Kaggle Benchmark Page](https://www.kaggle.com/benchmarks/tasks/mehmetisik/wwtp-operator-challenge)
2. Run the simulation with your chosen model
3. Share results by opening an issue with:
   - Model name and version
   - Final score (total and per-category breakdown)
   - Any interesting failure patterns observed

## 📋 Proposing New Scenarios

We plan to extend the benchmark with additional crisis events. Suggestions welcome:

- **Seasonal transitions** — gradual temperature changes over 90+ days
- **Equipment upgrades** — introducing new treatment capacity mid-simulation
- **Regulatory changes** — tighter discharge limits partway through
- **Multiple shock loads** — overlapping industrial discharge events

Open an issue with the tag `scenario-proposal` and describe:
- The crisis event and its real-world basis
- Suggested duration and severity
- Expected impact on plant operations

## 🤖 Multi-Agent Experiments

We're interested in whether multi-agent configurations can prevent the failure patterns we observed:

- **Planner + Operator**: One model plans strategy, another executes decisions
- **Operator + Validator**: One model decides, another validates before submission
- **Ensemble voting**: Multiple models vote on each decision

## 🔧 Fine-Tuning Experiments

If you fine-tune a model on WWTP operational data, we'd love to see:
- Training data description (anonymized)
- Before/after benchmark scores
- Which failure patterns were addressed

## 📝 Guidelines

- Be respectful and constructive
- Include data and evidence with claims
- Follow the existing code and documentation style
- Test your changes before submitting

## 📬 Contact

For questions, open an issue or reach out on [Kaggle](https://www.kaggle.com/mehmetisik).
