# Keep Hugging Face Spaces Awake

This repository contains a GitHub Actions workflow that periodically pings multiple Hugging Face Spaces to help prevent them from going inactive due to inactivity timeouts.

## 🚀 Features

- Automatically pings Hugging Face Spaces every 15 minutes
- Helps reduce cold starts and loading delays
- Uses GitHub Actions (completely free)
- Supports manual workflow execution
- Lightweight and easy to customize

---

## 📂 Workflow Location

Place the workflow file here:

```bash
.github/workflows/keep-spaces-awake.yml
```

---

## 🛠 Current Hugging Face Spaces

The workflow currently pings the following Spaces:

- https://kalpkanungo-multimodal-en-de-translator.hf.space
- https://kalpkanungo-geovistar.hf.space
- https://kalpkanungo-eventface.hf.space
- https://huggingface.co/spaces/kalpkanungo/Reflex_rag
- https://kalpkanungo-scenegraphnet.hf.space

---

## 📜 Workflow Configuration

```yaml
name: Keep HuggingFace Spaces Awake

on:
  schedule:
    - cron: "*/15 * * * *"
  workflow_dispatch:

jobs:
  ping-spaces:
    runs-on: ubuntu-latest

    steps:
      - name: Ping HuggingFace Spaces
        run: |
          urls=(
            "https://kalpkanungo-multimodal-en-de-translator.hf.space"
            "https://kalpkanungo-geovistar.hf.space"
            "https://kalpkanungo-eventface.hf.space"
            "https://huggingface.co/spaces/kalpkanungo/Reflex_rag"
            "https://kalpkanungo-scenegraphnet.hf.space"
          )

          for url in "${urls[@]}"; do
            echo "Pinging $url"
            curl -L --max-time 30 -s -o /dev/null $url
          done
```

---

## ⏰ Cron Schedule

```cron
*/15 * * * *
```

This means the workflow runs every **15 minutes**.

You can modify this depending on how frequently you want to keep your Spaces active.

Examples:

| Schedule | Meaning |
|---|---|
| `*/15 * * * *` | Every 15 minutes |
| `*/30 * * * *` | Every 30 minutes |
| `0 * * * *` | Every hour |

---

## ▶️ Manual Trigger

The workflow also supports manual execution using:

```yaml
workflow_dispatch:
```

You can run it anytime from the **GitHub Actions** tab.

---

## 📦 Setup Instructions

### 1. Create a GitHub Repository

Create a new repository on GitHub.

---

### 2. Add the Workflow File

Create the following directory structure:

```bash
.github/workflows/
```

Add your workflow file:

```bash
keep-spaces-awake.yml
```

---

### 3. Push to GitHub

```bash
git init
git add .
git commit -m "Add HF Spaces keep-alive workflow"
git branch -M main
git remote add origin <your-repo-url>
git push -u origin main
```

---

### 4. Enable GitHub Actions

Go to the repository → **Actions** tab → enable workflows if prompted.

---

## ⚠️ Notes

- GitHub Actions schedules may occasionally be delayed by a few minutes.
- Hugging Face infrastructure may still sleep Spaces under heavy load conditions.
- Pinging too frequently is unnecessary and may waste GitHub Action minutes.

---

## 📄 License

MIT License
