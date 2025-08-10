---
name: "VS Code Performance Investigation"
about: "Request investigation into high CPU/memory/lag in VS Code on macOS"
title: "[VSCode Perf] <short summary>"
labels: ["performance", "vscode"]
assignees: ["<your-github-username>"]
---

## Purpose
Briefly describe the problem and the goal of this investigation. Include any notable dates, PRs, or releases.

## Environment
- OS (macOS version): <!-- e.g., 14.5 -->
- VS Code version: <!-- e.g., 1.92.0 -->
- CPU: <!-- e.g., Apple M2 Pro (10 cores) -->
- Memory: <!-- e.g., 32GB -->
- Major extensions: <!-- e.g., GitLens, Copilot, ESLint, Prettier, Pylance, rust-analyzer -->
- Project size: <!-- repo size/file count, presence/size of node_modules, monorepo, etc. -->
- Git usage: <!-- yes/no; submodules/LFS/huge history? -->

## Symptoms (check all that apply)
- [ ] Slow app launch / file or tab switching
- [ ] Input lag while typing
- [ ] High CPU usage (e.g., Code Helper ~100%)
- [ ] High memory usage (e.g., > 4GB)
- [ ] Fans spinning constantly / fast battery drain
- [ ] Other: <!-- describe -->

## Steps to Reproduce
1. <!-- step 1 -->
2. <!-- step 2 -->
3. <!-- step 3 -->

## What To Investigate
Provide guidance the assistant should follow. For example:
1. Diagnostic checklist of likely causes
2. Factor-by-factor attribution (extensions/settings/file watching/Git/language servers)
3. Known macOS + VS Code performance pitfalls (past cases)
4. Concrete mitigation steps (settings/procedures)
5. Maintenance practices to prevent recurrence

## Expected Output
- Categorized list of potential causes
- Verification steps and necessary commands/UI operations for each cause
- Remediation steps if the cause applies
- Recommendations to avoid recurrence

## Reference Data (optional)
Paste outputs or attach logs where possible. Prefer linking a single consolidated log produced by the helper script below.

### Versions and Extensions
```
code --version
code --list-extensions
```

### OS / Hardware
```
sw_vers -productVersion
sysctl -n machdep.cpu.brand_string
sysctl -n hw.memsize
sysctl -n hw.ncpu
```

### Process Load Snapshot
```
top -o cpu -stats pid,command,cpu,mem -l 5 | grep -E 'Code|Electron|PID'
```

### Workspace Size
```
du -sh node_modules .git || true
find . -type f | wc -l
```

### Git Presence
```
git rev-parse --is-inside-work-tree 2>/dev/null || echo no
```

## Logs / Attachments
- Link or attach log file(s): <!-- e.g., _docs/logs/vscode_perf_YYYY-MM-DD_HHMMSS.log -->
- Note any extension or language server logs collected.
- If sensitive paths exist, redact as needed.

## Collection Script (optional)
Run the helper to collect a consolidated snapshot and attach the resulting log file path:
```
bash scripts/vscode-perf-collect.sh > _docs/logs/vscode_perf_$(date +%F_%H%M%S).log
```
For other workspaces:
```
WORKSPACE_DIR=/path/to/work bash scripts/vscode-perf-collect.sh > _docs/logs/vscode_perf_projectA_$(date +%F_%H%M%S).log
```

