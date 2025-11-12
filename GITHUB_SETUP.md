# GitHub Repository Setup Guide

This guide walks you through the GitHub settings you need to configure to enforce the team's rebase workflow and code ownership policies.

## Prerequisites

- You must be a repository administrator
- Repository must be hosted on GitHub

## Step 1: Enable Code Owners

The `CODEOWNERS` file is already in place at `.github/CODEOWNERS`. To make it work:

1. Go to your repository on GitHub
2. Click **Settings** (top menu)
3. Click **Branches** (left sidebar)
4. Find the **Branch protection rules** section
5. Click **Add rule** (or edit existing rule for `main`)

### Configure the Branch Protection Rule

**Branch name pattern:** `main`

Check these boxes:

- ✅ **Require a pull request before merging**
  - ✅ **Require approvals** (set to at least 1)
  - ✅ **Require review from Code Owners** ← **CRITICAL**

- ✅ **Require status checks to pass before merging**
  - This ensures CI checks pass (if you have any)

- ✅ **Require linear history** ← **CRITICAL FOR REBASE WORKFLOW**
  - This prevents merge commits
  - Forces contributors to rebase instead of merge

- ✅ **Do not allow bypassing the above settings**
  - Ensures even admins follow the rules

Click **Create** or **Save changes**

## Step 2: Verify CODEOWNERS is Working

To test that CODEOWNERS is working:

1. Create a test branch and modify a critical file (e.g., `src/App.tsx`)
2. Push the branch and create a pull request
3. Check the PR sidebar - you should see:
   - **Reviewers** section shows `@amberdhanani` as automatically requested
4. If this works, CODEOWNERS is configured correctly!

## Step 3: Configure Merge Settings

Go to **Settings → General → Pull Requests** section:

**Uncheck these options:**
- ❌ **Allow merge commits** (we only want rebase/squash)
- ❌ **Allow squash merging** (optional - only if you want pure rebasing)

**Check this option:**
- ✅ **Allow rebase merging** ← **REQUIRED**

**Also check:**
- ✅ **Automatically delete head branches** (cleans up after merge)

Click **Save**

## Step 4: Enable Required Reviews

Still in **Settings → Branches → Branch protection rule for `main`**:

Under **Require a pull request before merging**:

- Set **Required number of approvals before merging**: `1`
- ✅ **Dismiss stale pull request approvals when new commits are pushed**
  - Forces re-review if code changes after approval
- ✅ **Require review from Code Owners** (already checked in Step 1)

## Step 5: Optional - Add Status Checks

If you set up CI/CD (GitHub Actions, etc.):

In **Branch protection rule → Require status checks to pass**:

- ✅ **Require branches to be up to date before merging**
  - Ensures branch is rebased on latest main
  - Will block merges if branch is behind

Add your CI check names (e.g., `build`, `lint`, `test`)

## Step 6: Configure Notifications

To ensure you get notified when you're requested as a code owner:

1. Click your profile picture → **Settings**
2. Click **Notifications** (left sidebar)
3. Under **Participating, @mentions and custom**:
   - Set **Pull Request reviews** to: `Email` or `Web + Mobile`
4. Under **Watching**:
   - Set **Pull request reviews** to: `Email` or `Web + Mobile`

## Verification Checklist

Test that everything works:

- [ ] Create a PR that modifies `src/App.tsx` → @amberdhanani should auto-appear as reviewer
- [ ] Try to merge a PR without approval → should be blocked
- [ ] Try to merge a PR that's behind main → should be blocked (if you enabled status checks)
- [ ] Try to create a merge commit → should be blocked (only rebase allowed)

## Summary of What You've Configured

| Setting | Purpose |
|---------|---------|
| **CODEOWNERS file** | Auto-assigns @amberdhanani to review critical files |
| **Require review from Code Owners** | Blocks merge until code owner approves |
| **Require linear history** | Enforces rebase workflow, prevents merge commits |
| **Allow rebase merging only** | Only rebasing is permitted (no merge/squash) |
| **Require branches to be up to date** | Forces rebase before merge |
| **Auto-delete branches** | Keeps repo clean after merge |

## Troubleshooting

### CODEOWNERS Not Working

- Verify the file is at `.github/CODEOWNERS` (exact path and capitalization)
- Check that "Require review from Code Owners" is enabled
- Ensure `@amberdhanani` is a valid GitHub username with access to the repo

### Linear History Requirement Not Enforced

- Check that branch protection is enabled on `main`
- Verify "Require linear history" is checked
- Make sure the rule applies to administrators too

### Contributors Can Still Merge Without Rebasing

- Disable "Allow merge commits" in Settings → General → Pull Requests
- Enable "Require linear history" in branch protection
- Enable "Require branches to be up to date before merging"

## Next Steps

Now that GitHub is configured:

1. **Communicate the changes** to your team
2. Point them to [CONTRIBUTING.md](./CONTRIBUTING.md) for the workflow
3. Consider pinning the CONTRIBUTING.md as a repository discussion
4. Monitor the first few PRs to ensure everyone follows the process

---

**Need help?** Check GitHub's official documentation:
- [About CODEOWNERS](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners)
- [Branch protection rules](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches)
