# 🐛 Snake Animation Troubleshooting Guide

## Error: "Cannot find module 'canvas'"

This is a known issue with the Platane/snk action. Here are **3 solutions**:

---

## ✅ Solution 1: Use v2 (Recommended - Most Stable)

Replace your `.github/workflows/snake.yml` with this content:

```yaml
name: Generate Snake Animation

on:
  schedule:
    - cron: "0 */12 * * *"
  workflow_dispatch:
  push:
    branches:
      - main

jobs:
  generate:
    permissions:
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 10

    steps:
      - name: Generate github-contribution-grid-snake.svg
        uses: Platane/snk@v2
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-snake.svg
            dist/github-snake-dark.svg?palette=github-dark
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

      - name: Push to output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

**Then update your README.md snake section to:**

```markdown
### 🐍 Contribution Snake

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/BhabaniS1525/BhabaniS1525/output/github-snake-dark.svg" />
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/BhabaniS1525/BhabaniS1525/output/github-snake.svg" />
  <img alt="github-snake" src="https://raw.githubusercontent.com/BhabaniS1525/BhabaniS1525/output/github-snake.svg" />
</picture>
```

---

## ✅ Solution 2: Use svg-only version of v3

Replace with this workflow:

```yaml
name: Generate Snake Animation

on:
  schedule:
    - cron: "0 0 * * *"
  workflow_dispatch:
  push:
    branches:
      - main

jobs:
  generate:
    permissions:
      contents: write
    runs-on: ubuntu-latest

    steps:
      - name: Generate snake
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark

      - name: Push to output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

**Then update README.md to:**

```markdown
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/BhabaniS1525/BhabaniS1525/output/github-contribution-grid-snake-dark.svg" />
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/BhabaniS1525/BhabaniS1525/output/github-contribution-grid-snake.svg" />
  <img alt="github-snake" src="https://raw.githubusercontent.com/BhabaniS1525/BhabaniS1525/output/github-contribution-grid-snake.svg" />
</picture>
```

---

## ✅ Solution 3: Remove Snake, Use Other Awesome Widgets

If snake continues to fail, you can remove it and use these alternatives:

### Option A: Isometric Contribution Calendar

```markdown
![3D Contributions](https://github.com/BhabaniS1525/BhabaniS1525/blob/main/profile-3d-contrib/profile-night-rainbow.svg)
```

Setup: https://github.com/yoshi389111/github-profile-3d-contrib

### Option B: Activity Graph Only (Always Works)

```markdown
[![Activity Graph](https://github-readme-activity-graph.vercel.app/graph?username=BhabaniS1525&theme=tokyo-night&hide_border=true)](https://github.com/ashutosh00710/github-readme-activity-graph)
```

### Option C: Wakatime Stats (Coding Activity)

```markdown
[![Wakatime Stats](https://github-readme-stats.vercel.app/api/wakatime?username=BhabaniS1525&theme=tokyonight)](https://github.com/anuraghazra/github-readme-stats)
```

---

## 🔧 Additional Troubleshooting Steps

### Step 1: Check Permissions

Go to: **Your Repo → Settings → Actions → General**

Ensure these are enabled:

- ✅ Read and write permissions
- ✅ Allow GitHub Actions to create and approve pull requests

### Step 2: Manually Trigger Workflow

1. Go to **Actions** tab
2. Click **Generate Snake Animation**
3. Click **Run workflow** dropdown
4. Click **Run workflow** button
5. Wait for completion

### Step 3: Check Output Branch

After successful run:

1. Switch to **output** branch
2. Verify files exist:
   - `github-snake.svg` or
   - `github-contribution-grid-snake.svg`

### Step 4: Update README URLs

Make sure your README.md URLs match the actual file names in the output branch.

---

## 🎯 Quick Verification Checklist

- [ ] Workflow file is in `.github/workflows/snake.yml`
- [ ] Permissions are set correctly
- [ ] Workflow runs successfully (green checkmark)
- [ ] Output branch exists
- [ ] SVG files exist in output branch
- [ ] README.md URLs match actual file names
- [ ] Wait a few minutes for GitHub to serve the files

---

## 🆘 If Nothing Works

**Simplify your profile without snake:**

Remove the snake section and keep these awesome features that ALWAYS work:

```markdown
### 📊 GitHub Analytics

<div align="center">
  <img height="180em" src="https://github-readme-stats.vercel.app/api?username=BhabaniS1525&show_icons=true&theme=tokyonight"/>
  <img height="180em" src="https://github-readme-stats.vercel.app/api/top-langs/?username=BhabaniS1525&theme=tokyonight"/>
</div>

### 🔥 Streak Stats

![GitHub Streak](https://github-readme-streak-stats.herokuapp.com/?user=BhabaniS1525&theme=tokyonight)

### 📈 Activity Graph

[![Activity Graph](https://github-readme-activity-graph.vercel.app/graph?username=BhabaniS1525&theme=tokyo-night)](https://github.com/ashutosh00710/github-readme-activity-graph)

### 🏆 Trophies

![](https://github-profile-trophy.vercel.app/?username=BhabaniS1525&theme=tokyonight)
```

---

## 💡 Pro Tip

The snake is cool but not essential. Your profile already looks amazing with:

- ✅ Typing animation
- ✅ Stats cards
- ✅ Activity graph
- ✅ Trophies
- ✅ Skill icons

Focus on **content quality** over widgets!

---

**Need more help?** Check the original repo: https://github.com/Platane/snk/issues
