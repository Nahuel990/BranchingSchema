# Git Branching Strategies & Tagging

This document provides an overview of commonly used Git branching strategies, when to use them, and how tagging fits into the release process. It is intended for professional software and data teams managing code in collaborative environments.

---

## Branching Strategies

### 1. Git Flow
**Use when:** Working in large teams, with formal release cycles and multiple parallel developments.

- Main branches: `main`, `develop`
- Supporting branches: `feature/*`, `release/*`, `hotfix/*`

**Workflow:**
- New features are developed in `feature/*` branches off `develop`
- Releases are prepared in `release/*` branches
- Hotfixes are applied directly to `main` via `hotfix/*`

**Pros:**
- Clear structure for releases
- Good for complex projects

**Cons:**
- Overhead for small or fast-moving teams

---

### 2. GitHub Flow
**Use when:** Deploying continuously or working in small, agile teams.

- Main branch: `main`
- Feature branches: short-lived `feature/*` off `main`

**Workflow:**
- Create feature branch → open Pull Request → code review + CI → merge to `main`

**Pros:**
- Simple and effective
- Encourages frequent integration

**Cons:**
- Less control over environments

---

### 3. GitLab Flow
**Use when:** Using environments and issue-based workflows.

- Combines GitHub Flow with deployment environments (e.g., `dev`, `staging`, `prod`)
- Feature branches are linked to issue tracking

**Workflow:**
- Feature branches → merged to `dev` → promotion to `staging` → finally to `prod`

**Pros:**
- Integrates CI/CD and issue tracking
- Supports environment-specific branches

**Cons:**
- Slightly more complex to set up

---

### 4. Trunk-Based Development
**Use when:** Practicing Continuous Integration and Continuous Deployment (CI/CD).

- Main branch: `main` (single integration point)
- All changes are merged frequently (daily or multiple times per day)
- Feature flags are used to hide incomplete work

**Pros:**
- Minimal merge conflicts
- Rapid delivery

**Cons:**
- Requires strong CI, code quality checks, and feature flag discipline

---

### 5. Release Branching
**Use when:** Supporting multiple live versions or customers with different release cadences.

- Branches: `release/1.0`, `release/2.0`, etc.

**Workflow:**
- Develop on `main`
- When ready to release, create `release/x.y` branch
- Apply hotfixes to both `main` and relevant release branches as needed

**Pros:**
- Enables long-term support
- Clean version control

**Cons:**
- Requires strict process for maintenance

---

### 6. Environment Branching
**Use when:** Managing code that is deployed and tested separately in environments like `dev`, `qa`, `prod`.

- Branches: `dev`, `staging`, `main` (or `prod`)

**Workflow:**
- Merge features to `dev`
- Promote to `staging` after successful testing
- Final merge to `main` for production

**Pros:**
- Aligns with traditional deployment environments

**Cons:**
- Can lead to drift between branches if not well-maintained

---

#### 7. Experiment/Data Branching (This is a new suggested branching schema for ML/Data suggested by Google https://developers.google.com/machine-learning/guides/rules-of-ml#rule_40_keep_ensembles_simple)
**Use when:** Working on data pipelines, machine learning models, or exploratory development.

- Branches by experiment, dataset, or pipeline stage (e.g., `exp/new-ml-model`, `feat/data-cleaning-2023`)

**Workflow:**
- Independent branches for isolated experiments
- Merge or archive after evaluation

**Pros:**
- Great for experimentation
- Clean separation of work

**Cons:**
- Requires process to avoid unmaintained branches

---

## Tagging Strategies

### Why use tags?
Tags mark specific points in Git history for versioning and deployment.

- **Lightweight tags:** Quick pointers to a commit (e.g., `v1.2.0`)
- **Annotated tags:** Include metadata such as tagger name, date, and message

### When to tag:
- On every release (`v1.0.0`, `v1.1.0`, `v1.2.1`)
- After critical hotfixes
- Before/after major refactoring
- At integration milestones

**Best practices:**
- Use semantic versioning: `MAJOR.MINOR.PATCH` (e.g., `2.3.0`)
- Keep a changelog referencing each tag
- Tag from the commit on the `main` or `release/*` branch

---

## Summary Table

| Strategy                  | Team Size | Release Frequency | Multi-Environment | Best For                        |
|---------------------------|-----------|-------------------|-------------------|----------------------------------|
| Git Flow                 | Large     | Low               | Yes               | Traditional software projects    |
| GitHub Flow              | Small     | High              | No                | Startups and fast iterations     |
| GitLab Flow              | Medium    | Medium-High       | Yes               | CI/CD with issue tracking        |
| Trunk-Based Development  | Medium+   | High              | No                | High-performance engineering     |
| Release Branching        | Medium+   | Medium            | Optional          | LTS, client versioning           |
| Environment Branching    | Medium    | Medium            | Yes               | Data teams, infra teams          |
| Experiment/Data Branching| Any       | Low               | Optional          | ML, data pipelines, R&D          |

---

*End of document.*

