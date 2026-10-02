# 🤝 Contributing to JARVIS 3.0 (Mark LV)

Thank you for your interest in contributing to **JARVIS 3.0 — Next-Generation Autonomous Voice AI**, created and maintained by **Praveen Suthar**!

Repository: [https://github.com/Praveen-Suthar-08/JARVIS-3.0-Assistant.git](https://github.com/Praveen-Suthar-08/JARVIS-3.0-Assistant.git)

---

## 📌 Code of Conduct

By participating in this project, you agree to abide by our [Code of Conduct](CODE_OF_CONDUCT.md).

---

## 🛠️ How to Contribute

### 1. Reporting Bugs
- Search existing GitHub Issues before submitting a bug report.
- Include OS version, Python version, error stack trace, and steps to reproduce.

### 2. Suggesting Features
- Open an Issue titled `[Feature Request]: Your feature title`.
- Describe the motivation, use cases, and proposed design.

### 3. Submitting Pull Requests
1. Fork the repository on GitHub.
2. Create a new topic branch (`git checkout -b feature/awesome-plugin`).
3. Ensure all Python files adhere to PEP 8 standards.
4. Test your changes locally (`python main.py`).
5. Commit with clear, descriptive commit messages.
6. Push to your fork and submit a Pull Request to `main`.

---

## 🧩 Plugin Submission Guidelines

When adding new skills to `plugins/` or `actions/`:
- Keep tools modular and self-contained in a single file.
- Define a clear JSON schema dictionary `TOOL = { ... }`.
- Provide error handling inside the `execute(...)` function so runtime failures return helpful error text to the model rather than crashing the system loop.

---

## 👨‍💻 Maintainer

**Praveen Suthar**  
GitHub: [@Praveen-Suthar-08](https://github.com/Praveen-Suthar-08)
