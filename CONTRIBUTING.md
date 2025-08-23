# Contributing to VB-AF

If you're reading this, thank you for considering to contribute to VB-AF. All contributions, from bug reports to new features, are welcome.

This document provides a set of guidelines for contributing to the project.

## How Can You Contribute?
There are three primary ways:

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

Pull Requests (PRs) are also welcome. However, to maintain the quality and consistency of the codebase, it is required that code contributions adhere to the following guidelines:

1. Guiding Principles
    - **Minimalism:** The core `vbaf` library should remain light-weight, focused, and free of heavy client-based abstractions or unnecessary dependencies. New features should be implemented with efficiency and simplicity in mind. Pythonic coding is heavily encouraged.
    - **Consistency:** Code should adhere to the existing style and architectural patterns used throughout the project. This ensures the codebase remains readable and easy to maintain. For example, if you want to add a new fuzzer, you can do so by extending the `VBAF` class in `src/vbaf/fuzzers.py`, instead of first proposing to create a new module for the same.

2. Code Formatting
    - All Python code must be formatted with `black` using its default settings. Before submitting your pull request, please format your code:
      
        ```bash
        pip install black
        black .
        ```
       This ensures a consistent code style across the entire project.

3. Documentation
    - All new public classes, methods, and functions must include a comprehensive docstring following the **Google Python Style Guide**. Good documentation is crucial for making the tool accessible and maintainable. The docstrings should clearly explain the purpose of the code. It should document all arguments (Args:), return values (Returns:), and any errors that might be raised (Raises:). Include a concise, copy-pasteable code example if the function is user-facing.

Once you've acknowledged the guidelines above, you can proceed to setup your environment and submit a pull request:

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

