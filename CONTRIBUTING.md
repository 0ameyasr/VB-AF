# Contributing to VB-AF

If you're reading this, thank you for considering to contribute to VB-AF. All contributions, from bug reports to new features, are welcome.

This document provides a set of guidelines for contributing to the project.

## How Can You Contribute?
There are two primary ways:

### Reporting Bugs
If you find a bug, please ensure it has not already been reported by searchng the existing [issues](https://github.com/0ameyasr/vb-af/issues).

If you're opening a new issue, please include:
1. A clear and descriptive title
2. A detailed description of the bug, including steps to reproduce it
3. A code snippet that demonstrates your reported issue
4. The version of Python you are using

### Suggesting New Features or Enhancements
If you have an idea for a new feature (e.g. a new fuzzer) or an enhancement to an existing one, please open an [issue](https://github.com/0ameyasr/vb-af/issues) with:
1. A clear and descriptive title
2. A step-by-step description of the proposed enhancement and its benefits
    - Why is this feature needed? What problem does it aim to solve or improve?
    - What exactly is the feature (e.g. a new fuzzer, optimization, etc.)? Describe it in detail.
    - Explain the benefits it would bring to the codebase and the community. How would it enhance functionality or existing performance?
    - Where would this feature fit in the existing codebase? How would it interact with existing components?
    - Any other relevant points or suggestions to help clarify the proposal.
3. Include any relevant code snippets or provide examples of how the feature would be used in practice.

### Submitting Pull Requests
Here's how to set up your environment and submit a pull request:

1. Fork the repository
2. Clone your fork: 
    ```bash
    git clone https://github.com/YOUR_USERNAME/vb-af.git
    cd vbaf
    ```
3. Use a virtual environment.
    ```bash
    python -m venv venv
    source venv/bin/activate # On Windows, use `venv\Scripts\activate`

    # Install the project in editable mode
    pip install -e
    ```
4. Install the dependencies listed in `requirements.txt` (root).
5. Create a new branch for your changes. Use a descriptive name.
    ```bash
    git checkout -b feature/new-feature
    ```
6. Write your code. Please ensure your code follows existing style conventions. You are required to format all code using `black`.
7. Write tests. Please add new tests in the tests/ directory to ensure it works as expected and prevent future regressions.
8. Update documentation. If your changes affect the public API, please update the docstrings and any relevant files in the `docs/` directory.
9. Submit the pull request - push your branch to your fork on GitHub and open a pull request to the `main` branch of the original repository. Provide a clear description of the changes you have made.
