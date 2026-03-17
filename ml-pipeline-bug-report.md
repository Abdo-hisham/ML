# ML Pipeline YAML Bug Report

## Repository Link

- Public GitHub repository: **ADD_YOUR_PUBLIC_REPO_LINK_HERE**

## Actions Screenshot Evidence

- Add a screenshot of a successful green run from the **Actions** tab here.
- Suggested filename: `actions-success.png`

## Original YAML Bugs Identified and Fixes Applied

1. `on:` block indentation and structure were invalid.
- Bug: `push`, `branches`, and `main` were not indented under `on`.
- Fix: Rebuilt valid YAML structure under `on` and updated trigger logic.

2. Trigger behavior did not match assignment requirement.
- Bug: Original workflow targeted `main` and included `pull_request`.
- Fix: Changed trigger to run on every `push` except `main` using:
  - `on.push.branches-ignore: [main]`

3. `jobs` structure indentation was invalid.
- Bug: `validate-and-test`, `runs-on`, and `steps` were not nested properly.
- Fix: Corrected indentation so GitHub Actions can parse the workflow.

4. `Linter Check` step was incomplete.
- Bug: Step had no `run` or `uses` directive.
- Fix: Added linter command using Ruff:
  - `pip install ruff`
  - `ruff check .`

5. Missing checkout step.
- Bug: Repository files are unavailable in runner without checkout.
- Fix: Added `actions/checkout@v4` as the first step.

6. Artifact upload step was missing.
- Bug: No step to upload `README.md` as required.
- Fix: Added final step using `actions/upload-artifact@v4` with:
  - Artifact name: `project-doc`
  - Path: `README.md`

7. `requirements.txt` dependency source was assumed but absent.
- Bug: `pip install -r requirements.txt` would fail if file missing.
- Fix: Added `requirements.txt` with `torch` to support the dry test.

## Final Workflow File

- `.github/workflows/ml-pipeline.yml`

## How to Export This Report to PDF

1. Open this file in VS Code: `ml-pipeline-bug-report.md`.
2. Use any Markdown-to-PDF extension or print to PDF from preview.
3. Save as `ml-pipeline-bug-report.pdf`.

## Submission Checklist

- [ ] Public repository link updated in this report.
- [ ] Green Actions run screenshot captured and attached.
- [ ] PDF version generated and submitted.
