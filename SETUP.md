# Setup Instructions — Premium GitHub Profile

This repo is your **GitHub profile README** — the special repo GitHub shows on your
profile page when a repo is named **exactly the same as your username** and is public.

---

## 1. Folder structure (what you're getting)

```
<YOUR_GITHUB_USERNAME>/                 ← repo name MUST equal your GitHub username
├── README.md                           ← the profile page itself
├── SETUP.md                            ← this file (you can delete it after setup)
└── .github/
    └── workflows/
        ├── snake.yml                   ← generates the contribution snake animation
        ├── profile-3d.yml              ← generates the 3D contribution calendar
        └── waka-readme.yml             ← updates the WakaTime coding-time section
```

---

## 2. Create the special repository

1. Go to GitHub → **New repository**.
2. Name it **exactly** your GitHub username (e.g. if your username is `johndoe`, the
   repo must be named `johndoe`).
3. Make it **Public**.
4. Check **"Add a README file"** (you'll overwrite it), then create the repo.
5. GitHub will show a banner: *"You've discovered a secret repo!"* — that confirms it's linked to your profile.

---

## 3. Replace every placeholder

Find-and-replace these placeholders across `README.md` (and workflow files where noted)
with your real values:

| Placeholder | Replace with | Found in |
|---|---|---|
| `<YOUR_GITHUB_USERNAME>` | your GitHub username, e.g. `rahulsharma23` | README.md, all 3 workflow files |
| `<YOUR_LINKEDIN_URL>` | full LinkedIn profile URL | README.md |
| `<YOUR_LEETCODE_USERNAME>` | your LeetCode username | README.md |
| `<YOUR_WAKATIME_USERNAME>` | your WakaTime username | README.md (informational — actual data comes from the Action) |
| `<YOUR_SHOPORA_LIVE_URL>` / `<YOUR_SHOPORA_REPO_URL>` | Shopora deployment + repo links | README.md |
| `<YOUR_RAPIDKV_REPO_URL>` | RapidKV repo link | README.md |
| `<YOUR_PLAYHUB_LIVE_URL>` / `<YOUR_PLAYHUB_REPO_URL>` | PlayHub deployment + repo links | README.md |
| `<YOUR_GSSOC_PROFILE_URL>` | your GSSoC contributor profile / GSSoC repo link | README.md |

Tip: in VS Code, use **Find & Replace across files** (`Ctrl+Shift+H`) to do this in seconds.

---

## 4. Push the files

```bash
git clone https://github.com/<YOUR_GITHUB_USERNAME>/<YOUR_GITHUB_USERNAME>.git
cd <YOUR_GITHUB_USERNAME>
# copy README.md, SETUP.md, and the .github/ folder from this package into the cloned repo
git add .
git commit -m "feat: premium animated GitHub profile"
git push origin main
```

---

## 5. Enable the GitHub Actions

The workflows need **write permission** to push generated files back to your repo.

1. Go to your repo → **Settings → Actions → General**.
2. Under **Workflow permissions**, select **"Read and write permissions"**.
3. Save.
4. Go to the **Actions** tab → you'll see `Generate Snake Animation`,
   `Generate 3D Contribution Calendar`, and `Update WakaTime Coding Activity`.
5. Click each → **Run workflow** to trigger the first run manually (they'll also
   run automatically on the schedule defined in each YAML file).

The snake workflow pushes its SVG output to a branch called **`output`** — this
branch is created automatically the first time the workflow runs. No manual setup
needed there.

---

## 6. WakaTime setup (optional but required for the coding-time section to populate)

1. Create a free account at https://wakatime.com and install the plugin for your
   editor (VS Code, IntelliJ, etc.) so it starts tracking coding time.
2. Get your API key from https://wakatime.com/settings/api-key.
3. In your GitHub repo → **Settings → Secrets and variables → Actions → New repository secret**:
   - Name: `WAKATIME_API_KEY`
   - Value: (paste your key)
4. Re-run the `Update WakaTime Coding Activity` workflow — it will populate the
   `<!--START_SECTION:waka--> ... <!--END_SECTION:waka-->` block in `README.md`
   automatically on every run.

If you skip WakaTime, just delete that section from `README.md` — everything else
works independently.

---

## 7. Verifying everything works

- **GitHub stats / streak / top languages / activity graph / trophies / LeetCode
  card / visitor counter** — these are all live image URLs (github-readme-stats,
  streak-stats, readme-typing-svg, etc.) and start working the moment you push
  README.md with your real username — no Action needed.
- **Snake animation** — appears after the `snake.yml` workflow's first successful run.
- **3D contribution calendar** — appears after `profile-3d.yml`'s first successful run.
- **WakaTime section** — appears/updates after `waka-readme.yml`'s first successful
  run with a valid API key secret.

---

## 8. Optional cleanup

Once everything is verified working, feel free to delete this `SETUP.md` file from
the repo — it's not meant to be permanent, just a one-time guide.
