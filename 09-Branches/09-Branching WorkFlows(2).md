# 🐙 GitHub Flow

## 📖 Overview

**GitHub Flow** is a lightweight branching workflow created by GitHub for teams that deploy software frequently.

Unlike more complex workflows, GitHub Flow has only one long-lived branch:

```text
main
```

Every new feature, bug fix, or improvement is developed in its own short-lived branch.

After the work is reviewed and approved, it is merged into `main`.

The `main` branch should always remain stable and deployable.

---

# 🎯 Core Principles

GitHub Flow is built around a few simple rules:

- The `main` branch is always production-ready.
    
- Every change is made in a separate branch.
    
- Every change is reviewed through a Pull Request.
    
- After approval, changes are merged into `main`.
    
- Deployments happen frequently.
    

Because of its simplicity, GitHub Flow has become one of the most popular Git workflows.

---

# 🌳 Workflow Diagram

```text
                 main
                  │
                  ▼
        Create Feature Branch
                  │
                  ▼
          Make Commits
                  │
                  ▼
             Push Branch
                  │
                  ▼
          Open Pull Request
                  │
                  ▼
            Code Review
                  │
                  ▼
              Merge
                  │
                  ▼
              Deploy
```

---

# 🚀 Typical Workflow

### Step 1

Create a branch.

```bash
git switch -c feature/profile
```

---

### Step 2

Develop the feature.

Commit regularly.

---

### Step 3

Push the branch.

```bash
git push -u origin feature/profile
```

---

### Step 4

Open a Pull Request.

The team reviews:

- Code quality
    
- Bugs
    
- Style
    
- Performance
    
- Security
    

---

### Step 5

Update the branch if necessary.

Continue committing until the Pull Request is approved.

---

### Step 6

Merge into `main`.

---

### Step 7

Deploy.

Many companies automatically deploy every successful merge to production.

---

# 👍 Advantages

- Extremely simple.
    
- Easy for beginners.
    
- Encourages Pull Requests.
    
- Supports Continuous Deployment.
    
- Easy to maintain.
    

---

# 👎 Disadvantages

- Less suitable for projects with multiple supported versions.
    
- No built-in release branch.
    
- Requires confidence that `main` is always deployable.
    

---

# 🏢 Best For

GitHub Flow works especially well for:

- SaaS products
    
- Web applications
    
- APIs
    
- Mobile backends
    
- Continuous Deployment environments
    

Many modern startups use GitHub Flow because of its simplicity.

---

# 🌳 Git Flow

## 📖 Overview

Git Flow is a more structured branching strategy introduced by Vincent Driessen.

Unlike GitHub Flow, Git Flow introduces multiple long-lived branches to organize development and releases.

It is designed for projects with scheduled releases and larger development teams.

---

# 🌳 Main Branch Structure

```text
main

develop

feature/*

release/*

hotfix/*
```

Each branch has a specific purpose.

---

# 🌱 main

The `main` branch contains production-ready code.

Only thoroughly tested code should reach this branch.

Every commit on `main` should represent a stable release.

---

# 🌿 develop

The `develop` branch acts as the integration branch.

Developers merge completed features into `develop`.

When enough features are finished, a release branch is created.

---

# 🌱 feature/*

Every feature starts from `develop`.

Example:

```text
develop

│

└── feature/login
```

When complete:

```text
feature/login

↓

Merge

↓

develop
```

---

# 🚀 release/*

When preparing a release:

```text
develop

↓

release/v2.0
```

Only:

- Bug fixes
    
- Documentation
    
- Version changes
    

should happen here.

No new features are added.

Once ready:

```text
release

↓

main

↓

develop
```

The release is merged into both branches.

---

# 🚨 hotfix/*

Suppose production contains a critical bug.

Creating a normal feature branch would take too long.

Instead:

```text
main

↓

hotfix/security
```

Fix the issue.

Then merge it into:

- main
    
- develop
    

This ensures future releases also contain the fix.

---

# 📊 Git Flow Diagram

```text
                 main
                  ▲
                  │
              release/*
                  ▲
                  │
develop ──────────┼───────────────►

│        │        │

│        │        │

▼        ▼        ▼

feature feature feature

                  ▲

                  │

             hotfix/*
```

---

# 👍 Advantages

- Excellent release management.
    
- Clear separation between development and production.
    
- Easy to support multiple software versions.
    
- Well suited for enterprise environments.
    

---

# 👎 Disadvantages

- More complex.
    
- Many branches to maintain.
    
- Slower release cycle.
    
- Can feel excessive for small projects.
    

---

# 🏢 Best For

Git Flow is commonly used for:

- Enterprise software
    
- Banking systems
    
- Government software
    
- Desktop applications
    
- Software with scheduled releases
    

---

# 🚀 Trunk-Based Development

## 📖 Overview

Trunk-Based Development takes a completely different approach.

Instead of maintaining long-lived branches, developers work very close to a single shared branch called the **trunk**.

The trunk is usually the `main` branch.

Branches are:

- Small
    
- Short-lived
    
- Frequently merged
    

Many branches live only a few hours.

---

# 🌳 Workflow Diagram

```text
              main

      ▲ ▲ ▲ ▲ ▲

      │ │ │ │ │

 Small Small Small

 Branches
```

Every developer continuously integrates their work.

---

# 🚀 Typical Workflow

Create a branch.

Develop a small change.

Commit.

Push.

Open Pull Request.

Merge immediately.

Repeat.

The goal is continuous integration.

---

# 💡 Why It Works

Small changes are easier to:

- Review
    
- Test
    
- Merge
    
- Debug
    

Instead of one huge merge every month,

teams perform dozens of tiny merges every day.

---

# 👍 Advantages

- Minimal merge conflicts.
    
- Excellent for CI/CD.
    
- Faster feedback.
    
- Easier debugging.
    
- Cleaner integration.
    

---

# 👎 Disadvantages

- Requires automated testing.
    
- Requires disciplined developers.
    
- Large unfinished features require feature flags.
    

---

# 🏢 Best For

Trunk-Based Development is common in organizations practicing Continuous Integration and Continuous Delivery.

Examples include:

- Google
    
- Meta
    
- Netflix
    
- Amazon
    
- Microsoft
    

Large engineering organizations often favor this workflow because it encourages rapid integration and reduces long-lived branches.

---

# 📚 Key Takeaways (Part 2)

- **GitHub Flow** is simple, lightweight, and ideal for continuous deployment.
    
- **Git Flow** introduces dedicated branches for development, releases, and hotfixes, making it suitable for projects with planned release cycles.
    
- **Trunk-Based Development** emphasizes frequent integration through short-lived branches and works best with strong automation and CI/CD practices.
    
- No single workflow is universally best—the right choice depends on your project's size, release strategy, and team practices.