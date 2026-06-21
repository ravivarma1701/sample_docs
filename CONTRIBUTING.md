# Contributing to Sample Docs with LangChain Docling

We appreciate your interest in improving this project! Follow the steps below to get started.

## Code of Conduct

This repository adheres to the [Contributor Covenant Code of Conduct](https://www.contributor-covenant.org/version/2/1/code_of_conduct/). By participating, you are expected to uphold this code.

## How to Contribute

1. **Fork the repository**
   ```bash
   git fork https://github.com/your-username/sample_docs.git
   ```

2. **Create a new branch** for your feature or bug‑fix:
   ```bash
   git checkout -b my-feature-branch
   ```

3. **Make your changes** – add documentation, fix bugs, improve examples, etc.

4. **Run any existing notebooks** to ensure they still work. If you add new dependencies, update `requirements.txt`.

5. **Commit your changes** with a clear commit message:
   ```bash
   git add .
   git commit -m "Add detailed usage example for hierarchical chunking"
   ```

6. **Push to your fork** and open a Pull Request against the `main` branch:
   ```bash
   git push origin my-feature-branch
   ```
   Then, on GitHub, click *New Pull Request*.

## Pull Request Checklist

- [ ] The PR description explains the purpose of the change.
- [ ] New documentation is added or existing docs are updated accordingly.
- [ ] Code style follows the existing conventions (PEP 8 for Python).
- [ ] All notebooks run without errors from start to finish.
- [ ] If new dependencies are introduced, they are added to `requirements.txt`.

## Development Environment

We recommend using a virtual environment:
```bash
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```
If `requirements.txt` does not exist yet, you can generate one from the current environment:
```bash
pip freeze > requirements.txt
```

## Reporting Issues

If you encounter a bug or have a feature request, please open an issue on GitHub with:
- A clear title.
- A description of the problem or desired feature.
- Steps to reproduce (for bugs).
- Any relevant logs or screenshots.

Thank you for contributing!
