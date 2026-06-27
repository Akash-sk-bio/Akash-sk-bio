# Setup Instructions

## 1. Push files to your profile repo

```bash
cd path/to/Akash-sk-bio
git init
git remote add origin https://github.com/Akash-sk-bio/Akash-sk-bio.git
git add .
git commit -m "feat: premium profile v2"
git push -u origin main
```

## 2. Enable GitHub Actions

Go to your repo → Settings → Actions → General → Allow all actions → Save

## 3. Run Snake animation (first time)

Go to Actions tab → "Generate Snake Animation" → Run workflow

## 4. Fix YouTube workflow

Find your YouTube Channel ID:
- Go to your YouTube channel → View Page Source → search for `"channelId"`
- Replace `UCXX_REPLACE_WITH_YOUR_CHANNEL_ID` in `.github/workflows/youtube.yml`
- Then run the "Latest YouTube Videos" workflow

## 5. Optional upgrades

### WakaTime coding stats
1. Sign up at https://wakatime.com (free)
2. Install the VS Code extension
3. Add `WAKATIME_API_KEY` to repo Secrets (Settings → Secrets → Actions)
4. Add this to your README where you want it:

```markdown
[![WakaTime](https://wakatime.com/badge/user/YOUR_USER_ID.svg)](https://wakatime.com/@YOUR_USER_ID)
```

### 3D Contribution Calendar
Add this wherever you want in your README:

```markdown
![3D Contribution Calendar](https://raw.githubusercontent.com/Akash-sk-bio/Akash-sk-bio/main/profile-3d-contrib/profile-night-rainbow.svg)
```

And add this GitHub Action:

```yaml
# .github/workflows/3d-contrib.yml
name: 3D Contribution Calendar
on:
  schedule:
    - cron: "0 18 * * *"
  workflow_dispatch:
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: yoshi389111/github-profile-3d-contrib@0.7.1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          USERNAME: Akash-sk-bio
      - run: |
          git config user.name github-actions
          git config user.email github-actions@github.com
          git add -A
          git commit -m "3D contribution calendar update"
          git push
```
