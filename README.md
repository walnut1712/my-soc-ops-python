# 🎯 Soc Ops

> **An interactive social bingo game designed to break the ice at in-person events and mixers.**

Find people who match the questions on your card and get 5 in a row to win! Built with FastAPI, Jinja2, and HTMX for a smooth, interactive experience.

[![Python 3.13+](https://img.shields.io/badge/python-3.13%2B-blue)](https://www.python.org/downloads/)
[![FastAPI](https://img.shields.io/badge/built%20with-FastAPI-009485)]()
[![Tests Passing](https://img.shields.io/badge/tests-25%20passing-brightgreen)]()
[![MIT License](https://img.shields.io/badge/license-MIT-success)](LICENSE)

---

## ✨ Features

- 🎮 **Interactive Bingo Board** - Dynamically generated 5×5 bingo cards with question prompts
- 🎯 **Real-time Game Logic** - Instant feedback on marked squares and automatic win detection
- 🚀 **Fast & Responsive** - Built with FastAPI for low-latency operations and HTMX for smooth interactions
- 🎨 **Modern UI** - Clean, engaging interface optimized for mobile and desktop
- 🧪 **Fully Tested** - 25 comprehensive tests ensuring game logic reliability
- 📱 **Session-Based** - Maintains game state across player sessions

---

## 🚀 Quick Start

### Prerequisites

- [Python 3.13](https://www.python.org/downloads/) or higher
- [uv](https://docs.astral.sh/uv/) package manager

### Setup & Run

```bash
# Install dependencies
uv sync

# Start the server
uv run uvicorn app.main:app --reload
```

Open [http://localhost:8000](http://localhost:8000) in your browser and start playing!

---

## 📚 Learning Resources

This project is accompanied by a comprehensive **lab guide** that walks through building an AI-powered social game using GitHub Copilot agents.

| Part                                 | Topic                       |
| ------------------------------------ | --------------------------- |
| [**00**](workshop/00-overview.md)    | Overview & Checklist        |
| [**01**](workshop/01-setup.md)       | Setup & Context Engineering |
| [**02**](workshop/02-design.md)      | Design-First Frontend       |
| [**03**](workshop/03-quiz-master.md) | Custom Quiz Master Agent    |
| [**04**](workshop/04-multi-agent.md) | Multi-Agent Development     |
| [**05**](workshop/05-complete.md)    | Completion & Next Steps     |

👉 **[View Full Lab Guide](workshop/GUIDE.md)** for the complete learning experience.

---

## 🛠️ Development

### Run Tests

```bash
uv run pytest
```

### Lint & Format

```bash
uv run ruff check .    # Check code quality
uv run ruff format .   # Format code
```

### Project Structure

```
app/
  ├── main.py              # FastAPI application & routes
  ├── game_logic.py        # Core bingo game algorithm
  ├── game_service.py      # Game service layer
  ├── models.py            # Data models
  ├── data.py              # Question database
  └── templates/           # HTML templates (Jinja2)
tests/
  ├── test_api.py          # API endpoint tests
  └── test_game_logic.py   # Game logic tests
```

---

## 🤝 Contributing

Contributions are welcome! Whether you want to add new questions, improve the UI, or extend the game logic, we'd love your help.

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## 📝 License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

## 🔒 Security

Please report security vulnerabilities responsibly. See [SECURITY.md](SECURITY.md) for more information.

---

**Built with ❤️ for mixers, networking events, and breaking the ice.**
