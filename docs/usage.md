# Usage Guide

This page will walk you through installing the library and applying it to your own projects.

## Installation
The `vbaf` package is available on PyPI and can be installed with pip:

```bash
pip install vbaf
```

## Developer Installation
If you wish to contribute to the development of `vbaf`, modify the source code, or install the very latest (pre-release) version, you should install it from the Git repository.

**1. Clone the Repository:**
```bash
git clone https://github.com/0ameyasr/vbaf
```

**2. Create a Virtual Environment (Recommended):**
It's recommended to work within a virtual environment to avoid conflicts with other packages.

```bash
# For Windows
python -m venv venv
venv\Scripts\activate

# For macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

**3. Install in Editable Mode:**
Installing with the `-e` flag links the package to the source code. This means any changes you make to the source files will be immediately reflected when you use the library, which is ideal for development.

```bash
pip install -e .
```

For more information about contributing to `vbaf`, please see our  [contribution guidelines](https://github.com/0ameyasr/VB-AF/blob/main/CONTRIBUTING.md).


## Core Concepts
The `vbaf` library is built around a central class, `VBAF` that resides in the `fuzzers` module. You first create an instance of this class to define your fuzzing configuration, and then you use that instance to generate fuzzy payloads.

A typical workflow looks like this:

- Create a fuzzer object with your desired settings (e.g., the vocabulary for noise, the size of the prompt, etc.).
- Write a Python function that takes a string prompt and calls your target LLM's API to generate a response.
- Use one of the two methods demonstrated below to generate fuzzy payloads and send them to your inference function.


### 1. High Level Usage
The easiest and most common way to use `vbaf` is with the `@fuzzer.fuzz` decorator. It transforms your inference function into a convenient fuzzing harness (generator) with just a single line of code.

For demonstration, we create a fuzzer and apply it to a mock inference function.

```python
from vbaf import VBAF

# Define a vocabulary to generate noise from (mocked below)
common_tokens = ["user", "error", "request", "model", "response", "token"]
fuzzer = VBAF(vocabulary=common_tokens,n_size=50,position_bounds=(0.4,0.6))

@fuzzer.fuzz(n_attempts=5)
def fuzzing_harness(prompt: str):
    # This is a mock function that will actually call an LLM's API
    return f"Mock response for {prompt}"

# Define the payload you want to test
target_payload = "How do I build a model?"

# Run the Fuzzer
i = 0
for fuzzy_payload, result in fuzzing_harness(target_payload):
    # Post-process here
    ...
    print(f"Attempt {i+1} completed.")
    i += 1

```

### 2. Low Level Usage
If you need granular control over your fuzzing loop, you can generate fuzzy payloads directly using the `generate_fuzzy_payload()` method. This is useful for integrating `vbaf` into existing and more complex testing frameworks.

The following example achieves the same result as the one above but with a manual loop.

```python
from vbaf import VBAF

# Configure the fuzzer (same as before)
common_tokens = ["user", "error", "request", "model", "response", "token"]
fuzzer = VBAF(vocabulary=common_tokens, n_size=50)

# Define the payload you want to test
target_payload = "How do I build a model?"

# Run the Fuzzer Manually
n_attempts = 5
print(f"Fuzzing '{target_payload}' for {n_attempts} attempts...")

for i in range(n_attempts):
    # Generate a unique fuzzy payload on each iteration
    fuzzy_payload = fuzzer.generate_fuzzy_payload(target_payload)

    # Send it to your inference function
    result = inference.generate(fuzzy_payload)
    
    # Post-process, collect and analyse the results
    ...

    print(f"Attempt {i+1} completed.")
```