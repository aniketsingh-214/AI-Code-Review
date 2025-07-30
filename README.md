# AI Code Review

A lightweight, customizable AI-powered tool for automating code review in GitHub Pull Requests or local changes, powered by OpenAI (or other LLM backends).

## 🚀 Features

- Reviews pull requests and diffs automatically using an AI model  
- Flags issues like bugs, security, style deviations, and complexity  
- Supports human-friendly line-by-line comments with explanations  
- Integrates via GitHub Actions or local CLI workflows  
- Fully configurable: models, prompts, ignore/include patterns

## 📦 Installation

### 1. GitHub Action Setup

- Add `OPENAI_API_KEY` to your repository’s Secrets
- Create `.github/workflows/ci-review.yml` with content similar to:

  ```yaml
  name: AI Code Review
  on:
    pull_request:
      types: [opened, synchronize, reopened]
  jobs:
    review:
      runs-on: ubuntu-latest
      steps:
        - uses: actions/checkout@v3
        - name: Run AI code review
          uses: your‑username/AI‑Code‑Review@main
          with:
            OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
            MODEL: gpt‑4
            EXCLUDE: "**/*.md,**/test/**"
            # other configs as needed
````

* Push to your repo—on new pull requests, the tool will analyze diffs and post comments.

### 2. Local CLI Use

* Install dependencies:

  ```bash
  pip install -r requirements.txt   # if Python-based
  # or npm install, yarn install, etc.
  ```

* Run review:

  ```bash
  ai-review --path . --branch feature-branch
  ```

  and optionally:

  ```bash
  ai-review --diff main..feature-branch --output report.md
  ```

## ⚙️ Configuration

Place a config file like `review.config.yml` or use environment variables:

```yaml
api_key: YOUR_OPENAI_KEY
model: gpt-3.5-turbo
prompt: "You are a senior software engineer reviewing code diffs. Provide inline feedback concisely."
ignore:
  - node_modules/**
  - docs/**
include:
  - src/**/*.js
  - src/**/*.py
```

## 🧪 Example Usage

After opening a pull request:

* The bot scans changed files
* Detects issues like unused variables, missing tests, potential security concerns
* Posts comments back to the PR with suggestions and explanations

## 🧾 Output Formats

* Inline GitHub PR comments
* Markdown summary files (e.g. `code-review-report.md`)
* JSON output for machine processing

## 🤝 Contributing

1. Fork the repo
2. Create a branch (`feature/…` or `fix/…`)
3. Make your changes and update the README/docs
4. Submit a pull request
5. Ensure CI tests pass

Please follow the coding style in `CONTRIBUTING.md`.

## Why Use This Tool?

AI‑driven review tools like **Gito** or **CodeRabbit** — provide rapid automated feedback, and help enforce consistency, security, and best practices across your team’s codebase ([github.com][1], [github.com][2], [github.com][3], [dev.to][4], [github.com][5]).
Similar GitHub Actions like **AI Code Reviewer** by villesau use GPT‑4 to comment inline on PR diffs and are trusted by many teams for fast integration and good defaults ([github.com][1]).

## 📚 More Context on AI Code Review

* AI code reviews rely on ML & NLP to analyze code diffs, detect patterns, flag vulnerabilities, and generate improvement suggestions automatically, speeding up development and offloading repetitive tasks ([github.com][2]).
* These tools boost developer productivity, reduce manual review effort, and support consistent coding standards—though final merge decisions should remain human authenticated ([github.blog][6]).

---

Feel free to modify section headings as needed, fill placeholders with your actual file names and commands, and include screenshots or workflow samples specific to your project.

[1]: https://github.com/marketplace/actions/ai-code-review-action?utm_source=chatgpt.com "AI Code Review Action - GitHub Marketplace"
[2]: https://github.com/resources/articles/ai/ai-code-reviews?utm_source=chatgpt.com "AI Code Reviews"
[3]: https://github.com/coderabbitai/ai-pr-reviewer?utm_source=chatgpt.com "coderabbitai/ai-pr-reviewer: AI-based Pull Request ..."
[4]: https://dev.to/daveturissini/build-your-own-ai-code-review-agent-in-5-minutes-with-github-actions-2kcg?utm_source=chatgpt.com "Build Your Own AI Code Review Workflow in 5 Minutes ..."
[5]: https://github.com/topics/ai-code-review?utm_source=chatgpt.com "ai-code-review"
[6]: https://github.blog/ai-and-ml/generative-ai/code-review-in-the-age-of-ai-why-developers-will-always-own-the-merge-button/?utm_source=chatgpt.com "Code review in the age of AI: Why developers will always ..."
