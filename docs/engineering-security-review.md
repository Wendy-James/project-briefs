# Engineering Quality And Security Review

Date: 2026-05-19

Scope: public repositories under `Wendy-James`, including profile README, portfolio site, project brief repository, frontend/backend practice repositories, workflow automation repository, reading notes, and the LaTeX course-design template.

## Summary

The public GitHub portfolio now has a clearer professional entry point and safer project presentation. A local scan found no committed `.env` file, private key, database connection string, large binary artifact, or obvious live cloud/API token pattern in the checked public repository working trees.

The most important cleanup completed in this pass:

| Repository | Completed change |
|---|---|
| `Wendy-James` | Updated the profile README for AI engineering, backend, LLM application and document intelligence positioning. |
| `project-briefs` | Added public, evidence-bounded project briefs for major AI/backend/research experience. |
| `Wendy-James.github.io` | Updated the portfolio page to match the GitHub profile positioning. |
| `ai-zhishi-zhushou` | Clarified prototype scope and engineering structure in README/project files. |
| `mas-chuangzuozhe-houtai` | Moved AMap Web JS key usage to `VUE_APP_AMAP_KEY`; added `.env.example`; documented architecture and API assumptions. |
| `pingguofeng-dianshang-lianxi-zhan` | Moved WeChat/OpenAI demo credentials to environment variables; added `.env.example`. |
| `waimao-quanpinlei-huoke-zhushou` | Added safe `.env.example`, `.env` ignore rules, and header-only schema CSV templates for public structure without real business data. |

## Security Findings

| Severity | Repository | Path / area | Finding | Status / recommendation |
|---|---|---|---|---|
| High | `mas-chuangzuozhe-houtai` | `src/main.js` | AMap Web JS key was hardcoded in frontend source. | Fixed. Rotate the previously exposed key in the AMap console if it was ever pushed publicly. |
| Medium | `pingguofeng-dianshang-lianxi-zhan` | `ai_kefu.py` | Demo WeChat/OpenAI credential variables were represented directly in source. Values appeared to be placeholders, but the pattern was unsafe. | Fixed with environment variable reads and `.env.example`. |
| Medium | `waimao-quanpinlei-huoke-zhushou` | CSV data areas | Header-only CSV schemas are now public. Real customer/supplier rows would be sensitive if added later. | Keep only schema/templates in Git. Keep real rows ignored and local. |
| Medium | `waimao-quanpinlei-huoke-zhushou` | QQ mail / search integrations | Runtime credential variable names appear in code and docs. No live values were found by pattern scan. | Keep real values in local environment only. Add automated secret scanning before future pushes. |
| Medium | `waimao-quanpinlei-huoke-zhushou` | local workflow config/docs | Some workflow files may contain local paths or machine-specific examples. | Replace visible local paths with `${PROJECT_ROOT}` or relative examples during the next cleanup pass. |
| Low | `mas-chuangzuozhe-houtai` | Vue forms | Password fields exist as normal UI/business fields. No hardcoded password value was found. | Keep as application form data only; avoid logging or committing sample user records. |
| Low | `hefei-gongda-kechengsheji-muban` | LaTeX template | No secret patterns or large generated artifacts were found. | Optional: add `.gitignore` for LaTeX build outputs. |

## Engineering Structure Matrix

Legend: `Y` = present, `Partial` = present but should be expanded, `-` = missing or not applicable.

| Repository | README | `.gitignore` | `.env.example` | Dependency manifest | Tests | Docs | License |
|---|---:|---:|---:|---:|---:|---:|---:|
| `Wendy-James` | Y | - | - | - | - | Partial | - |
| `Wendy-James.github.io` | Y | - | - | - | - | - | - |
| `project-briefs` | Y | Y | Partial | - | - | Y | - |
| `ai-zhishi-zhushou` | Y | Y | - | - | - | Partial | - |
| `mas-chuangzuozhe-houtai` | Y | Y | Y | `package.json` | - | Partial | - |
| `pingguofeng-dianshang-lianxi-zhan` | Y | Y | Y | - | - | - | - |
| `waimao-quanpinlei-huoke-zhushou` | Y | Y | Y | - | Y | Partial | - |
| `open-source-reading-notes` | Y | - | - | - | - | Partial | - |
| `hefei-gongda-kechengsheji-muban` | Y | - | - | - | - | Partial | Y |

## Recommended Next Cleanup

1. Add `LICENSE` or a clear portfolio-only usage notice to repositories that are not meant for reuse.
2. Add `requirements.txt` or `pyproject.toml` to Python repositories with runnable scripts.
3. Add `docs/api.md` and `docs/architecture.md` to the main runnable projects.
4. Add a lightweight secret-scan script or GitHub Action before future pushes.
5. Keep generated outputs, local reports, customer data, supplier lists and real email records out of Git.

## Conventional Commit Templates

Use these commit messages over the next two weeks:

```text
docs: update GitHub profile for AI backend positioning
docs: add engineering security review report
chore: add env examples for public repositories
fix: load AMap key from environment variable
fix: read demo credentials from environment variables
docs: add API contract for document QA prototype
fix: render chat messages without innerHTML
docs: document Vue admin dashboard architecture
docs: add backend API contract for admin dashboard
chore: add Python dependency manifest
docs: replace local absolute paths with setup variables
refactor: move local workflow config to example file
test: add secret scan check for public repos
test: add smoke test for document QA frontend
test: add safety tests for CSV schema templates
docs: add public disclosure policy for project briefs
docs: add security notes for workflow automation project
chore: add license and repository usage notices
ci: add basic lint and secret scanning workflow
```
