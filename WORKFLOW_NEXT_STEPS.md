# Workflow Setup - Next Steps

**Status:** Files are ready, GitHub settings need to be configured

**Last updated:** 2025-10-17 (paused for dinner)

---

## ✅ What's Already Done

These files have been created/updated and are ready to go:

1. ✅ `CONTRIBUTING.md` - Updated with rebase rules and critical files list
2. ✅ `.github/CODEOWNERS` - Auto-assigns @amberdhanani to review critical files
3. ✅ `.github/pull_request_template.md` - Updated with coordination checklist
4. ✅ `GITHUB_SETUP.md` - Complete setup guide for GitHub settings
5. ✅ `REVERT_WORKFLOW_CHANGES.md` - Rollback instructions if experiment fails

**Nothing has been committed yet** - these are just local changes.

---

## 🎯 What You Need to Do Tomorrow

### Step 1: Configure GitHub Repository Settings (5 minutes)

Go to your GitHub repository and configure these settings:

#### A. Branch Protection for `main`

**Path:** Settings → Branches → Add rule (or edit existing rule)

**Branch name pattern:** `main`

**Required settings:**
- ✅ **Require a pull request before merging**
  - ✅ Require approvals: `1`
  - ✅ **Require review from Code Owners** ← This makes CODEOWNERS work

- ✅ **Require linear history** ← This enforces rebase workflow (prevents merge commits)

- ✅ **Do not allow bypassing the above settings**

Click **Create** or **Save changes**

#### B. Merge Method Settings

**Path:** Settings → General → Pull Requests section

**Configure these:**
- ❌ **Uncheck "Allow merge commits"** ← Forces rebase/squash only
- ✅ **Check "Allow rebase merging"** ← Required
- ❌ **Uncheck "Allow squash merging"** (optional - your choice)
- ✅ **Check "Automatically delete head branches"** ← Keeps repo clean

Click **Save**

---

### Step 2: Test That It Works (2 minutes)

Create a quick test to verify CODEOWNERS is working:

1. Create a test branch: `git checkout -b test-codeowners`
2. Make a trivial change to `src/App.tsx` (add a comment)
3. Push and create a PR
4. **Expected result:** You should see @amberdhanani auto-assigned as reviewer

If you see yourself auto-assigned, it's working! Close/delete the test PR.

---

### Step 3: Commit and Push Changes (1 minute)

Once GitHub is configured and tested:

```bash
# Review what's changed
git status

# Add all the new workflow files
git add CONTRIBUTING.md .github/CODEOWNERS .github/pull_request_template.md GITHUB_SETUP.md REVERT_WORKFLOW_CHANGES.md WORKFLOW_NEXT_STEPS.md

# Commit
git commit -m "Add rebase workflow and code ownership policies

- Update CONTRIBUTING.md with rebase rules and critical files list
- Add CODEOWNERS to auto-assign reviews for critical files
- Update PR template with coordination checklist
- Add GITHUB_SETUP.md for repository configuration
- Add REVERT_WORKFLOW_CHANGES.md for easy rollback"

# Push to main
git push origin main
```

---

### Step 4: Notify Your Team (2 minutes)

Send a message to contractors/team members:

> **New workflow starting [DATE]:**
>
> We're implementing a rebase-first workflow to keep our git history clean. Please read the updated CONTRIBUTING.md before your next PR.
>
> **Key changes:**
> 1. **Rebase when main updates** - No merge commits allowed
> 2. **Coordinate on critical files** - Notify @amberdhanani before modifying files in api/, src/data/, src/types/, App.tsx, or config files
> 3. **GitHub will auto-assign reviews** - For critical files, I'll be automatically added as a reviewer
>
> **Read:** CONTRIBUTING.md for full workflow details
>
> This is an experiment - we'll evaluate after 2 weeks.

---

## 📋 Quick Checklist for Tomorrow

- [ ] Configure GitHub branch protection (Settings → Branches)
- [ ] Configure merge settings (Settings → General → Pull Requests)
- [ ] Test CODEOWNERS with a test PR
- [ ] Commit and push all workflow files
- [ ] Notify team about new workflow
- [ ] (Optional) Delete this file after completing steps

---

## 🆘 If You Need Help Tomorrow

- **Full setup guide:** See `GITHUB_SETUP.md`
- **To revert everything:** Follow `REVERT_WORKFLOW_CHANGES.md`
- **GitHub docs:** [About CODEOWNERS](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners)

---

## Time Estimate

- GitHub configuration: **5 minutes**
- Testing: **2 minutes**
- Committing changes: **1 minute**
- Team notification: **2 minutes**
- **Total: ~10 minutes**

---

**Note:** You can also ask an AI agent tomorrow: "Follow the steps in WORKFLOW_NEXT_STEPS.md" and they'll know exactly what to do.

**Current state:** All files ready locally, GitHub settings not configured yet, changes not committed.
