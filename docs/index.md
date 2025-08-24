# Vocabulary-Based Adversarial Fuzzing (VB-AF)

**VB-AF** is a gray-box fuzzing framework designed to probe for and identify commonly uncovered and unseen vulnerabilities in Large Language Models (LLMs). 
It serves as a tool for AI safety researchers, red-teamers, and developers to test the alignment and robustness of their models. 

This project is the **official** implementation of the method detailed in this [Kaggle Writeup](https://www.kaggle.com/competitions/openai-gpt-oss-20b-red-teaming/writeups/red-teaming-gpt-oss-20b-probing-for-easily-reprodu), originally developed for probing previously unseen vulnerabilities in OpenAI's `gpt-oss:20b` model as part of the hackathon **'Red‑Teaming Challenge - OpenAI gpt-oss-20b'** hosted on Kaggle. It proved to be an effective tool, helping me uncover an almost invisible vulnerability in the model's reasoning CoT.

Following the vision for which it was developed, I then decided to turn VB-AF into a powerful fuzzing framework - a tool that could help AI red-teamers detect and observe how LLMs responded to unexpected, adversarial inputs. 

---

## What is VB-AF?

At its core, VB-AF is not a simple jailbreak, but a systematic method for observing how LLMs process and respond to unexpected inputs. It works by generating complex, high-entropy prompts that exploit known architectural weaknesses in transformer models. 

Its effectiveness was demonstrated through extensive experimentation, where VB-AF demonstrated its potential to induce cognitive-dissonance like states in reasoning models, leading to undesired behaviour. In its unoptimized, base version (as presented in the `VBAF` class), VB-AF achieved an overall statistically significant **36.44% ASR** against `gpt-oss:20b`. Due to the obvious scope of optimization it presented due to its design, it was decided to be shared with the community for further improvements and exploration of use-cases.

Its fuzzy payload generation algorithm (`generate_fuzzy_payload`) involves the following steps:

1. **Extracting the model's token vocabulary:** this came from the belief that doing so could produce high-entropy but semantically grounded noise for the model. While the base implementation uses the model’s tokens, one could instead design a large, diverse, and more targeted token vocabulary for the same purpose. This flexibility highlights VB-AF’s **gray-box** nature. 
2.	**Generating `n_size = 100` token sequences, each consisting of `7 <= rand_bounds <= 21` tokens joined using ZWSP (`\u200B`) separators.** The ZWSP is a well documented character for adversarial obfuscation, with some very direct applications discussed in **Boucher et al.**, ([IEEE](https://www.cl.cam.ac.uk/~is410/Papers/badchars_draft.pdf) 2021). Its primary role and goal is to disrupt the model's tokenization process, potentially increasing evasion from filters and allowing the payload to be parsed in a non-standard way.
3.	**Inserting a request at a random position `argK` within `[n_size // 2, 3 * n_size // 5]` somewhere in the middle:** the request (or `payload`) was injected specifically somewhere in the **50 - 60%** portion of the prompt context, exploiting the 'lost in the middle' phenomenon studied by **Liu et al.** ([TACL](https://aclanthology.org/2024.tacl-1.9/) 2024) by ensuring the top and bottom of the context was filled with noise, and only the middle contained a legible token sequence - the payload itself. 
4. **Concatenating all token sequences and the injected payload** into a single adversarial prompt that would be sent to the model via a harness for inference.

---

## Ethical Disclaimer

**Warning:** This is a research tool intended for security professionals, AI safety researchers, and developers for authorized security assessments and educational purposes.

By using this software, you agree that **you are solely responsible** for your actions.

The `vbaf` framework is a powerful tool designed to probe for and identify potentially significant vulnerabilities in Large Language Models (LLMs). Misuse of this software to generate harmful content or attack systems without explicit, authorized permission is **strictly prohibited**. 

The author(s) is(are) **not responsible** for any damage caused by the misuse of this tool. Please use responsibly and ethically.

---


## Getting Started

Before you use this tool, **you absolutely must acknowledge the previous disclaimer**. Following that, to begin using VB-AF, start with the following links:

* **[Usage Guide](./usage.md):** A step-by-step guide to installing `vbaf` and using it in your own projects.
* **[API Reference](./api.md):** Detailed documentation for the fuzzers (e.g. base `VBAF`) included and their methods.