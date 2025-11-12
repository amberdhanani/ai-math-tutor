# Revert Workflow Changes - AI Agent Instructions

**Purpose:** This file contains complete instructions to revert all rebase workflow and code ownership changes made on 2025-10-17.

**When to use:** If the new workflow proves too restrictive or burdensome for the team.

---

## 🤖 Instructions for AI Agent

If the user asks you to revert the workflow changes, follow these steps exactly:

## Step 1: Delete Newly Created Files

Delete these files that were created as part of the workflow implementation:

```bash
# Delete CODEOWNERS file
rm /Users/amberdhanani/Software/ai-math-tutor/.github/CODEOWNERS

# Delete GitHub setup guide
rm /Users/amberdhanani/Software/ai-math-tutor/GITHUB_SETUP.md

# Delete this revert guide (after execution)
rm /Users/amberdhanani/Software/ai-math-tutor/REVERT_WORKFLOW_CHANGES.md
```

**Files to delete:**
- `.github/CODEOWNERS`
- `GITHUB_SETUP.md`
- `REVERT_WORKFLOW_CHANGES.md` (this file)

## Step 2: Revert CONTRIBUTING.md to Original State

The CONTRIBUTING.md file was modified to add rebase rules and critical files sections. Restore it to its original state.

**Original content starts below the line:**

---

```markdown
# Contributing to AI Math Tutor

Thank you for your interest in contributing to the AI Math Tutor project! This document provides guidelines and instructions for contributing.

## Getting Started

1. **Read the Documentation**
   - Review [README.md](./README.md) for setup instructions
   - Check [claude.md](./claude.md) for project context
   - Read through [docs/ai/](./docs/ai/) for architecture details

2. **Set Up Your Environment**
   ```bash
   git clone <repository-url>
   cd ai-math-tutor
   pnpm install
   cp .env.example .env.local
   # Add your API keys to .env.local
   pnpm run dev
   ```

3. **Check Node.js Version**
   - This project requires Node.js 18+
   - Use the version specified in `.nvmrc`: `nvm use`

## Development Workflow

### Branch Strategy

- **`main`**: Stable, production-ready code
- **Feature branches**: `feature/your-feature-name`
- **Bug fixes**: `fix/issue-description`
- **Documentation**: `docs/what-you-are-documenting`

### Making Changes

1. **Create a Branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make Your Changes**
   - Write clean, readable code
   - Follow existing code style and patterns
   - Add comments for complex logic
   - Update documentation if needed

3. **Test Your Changes**
   ```bash
   # Build check
   pnpm run build

   # Lint check
   pnpm run lint

   # Manual testing
   pnpm run dev
   ```

4. **Commit Your Changes**
   - Use clear, descriptive commit messages
   - Follow conventional commits format (recommended):
     ```
     feat: add new lesson for fractions
     fix: resolve VAD sensitivity issue
     docs: update README with deployment steps
     refactor: simplify stage progression logic
     ```

5. **Push and Create PR**
   ```bash
   git push origin feature/your-feature-name
   ```
   Then create a Pull Request on GitHub

## Code Standards

### TypeScript

- Use TypeScript for all new code
- Define proper types (avoid `any` when possible)
- Export types from `src/types/index.ts`

### React Components

- Use functional components with hooks
- Keep components focused and single-purpose
- Extract reusable logic into custom hooks
- Use meaningful prop names

### File Organization

```
src/
├── components/      # React UI components
├── data/           # Static data (lessons, etc.)
├── types/          # TypeScript type definitions
├── utils/          # Utility functions
└── App.tsx         # Main application logic
```

### Naming Conventions

- **Components**: PascalCase (e.g., `VoiceInterface.tsx`)
- **Functions**: camelCase (e.g., `handleStageComplete`)
- **Constants**: UPPER_SNAKE_CASE (e.g., `API_ENDPOINT`)
- **Types/Interfaces**: PascalCase (e.g., `SessionState`)

## Testing Guidelines

While automated tests are not yet implemented, please manually verify:

1. **Voice Session**
   - Connection establishes successfully
   - AI tutor speaks without interrupting itself
   - User speech is detected correctly
   - Stage transitions work

2. **Whiteboard**
   - Drawing works smoothly
   - Clear button functions
   - AI can see drawings (check console logs)

3. **API Endpoints**
   - `/api/session` returns valid SDP
   - `/api/render` generates drawing commands

4. **Build & Deploy**
   - `pnpm run build` succeeds without errors
   - No TypeScript errors
   - No ESLint warnings

## Adding New Lessons

1. Edit `src/data/lessons.ts`
2. Follow the existing lesson structure:
   ```typescript
   {
     lesson_id: 'unique-id',
     title: 'Lesson Title',
     learning_goal: 'What students learn',
     stages: [
       {
         stage_id: 1,
         problem: 'Problem description',
         learning_objective: 'Stage objective',
         mastery_criteria: {
           description: 'How to assess mastery',
           indicators: ['Signal 1', 'Signal 2']
         },
         context_for_agent: 'AI tutor instructions'
       }
     ]
   }
   ```
3. Test thoroughly with voice interaction
4. Document any special behaviors

## Common Tasks

### Adjusting VAD Settings

Edit `src/App.tsx` around line 92:
```typescript
turn_detection: {
  type: 'server_vad',
  threshold: 0.6,           // 0.0-1.0 (higher = less sensitive)
  prefix_padding_ms: 300,   // Capture before speech
  silence_duration_ms: 1000 // Wait before turn ends
}
```

### Modifying AI Tutor Behavior

- **Global behavior**: Edit system instructions in `src/App.tsx:88`
- **Stage-specific**: Edit `context_for_agent` in lesson definition

### Adding New Function Tools

1. Define function in `sendSessionUpdate()` in `src/App.tsx`
2. Add handler in `handleFunctionCall()`
3. Test via console logs to verify AI calls it correctly

## Pull Request Guidelines

### PR Title Format

- `feat: description` - New feature
- `fix: description` - Bug fix
- `docs: description` - Documentation only
- `refactor: description` - Code refactoring
- `chore: description` - Build/tooling changes

### PR Description Should Include

- **What**: What changes were made
- **Why**: Why these changes are needed
- **Testing**: How you tested the changes
- **Screenshots**: If UI changes are involved
- **Breaking Changes**: If any (and migration steps)

### PR Checklist

- [ ] Code builds without errors (`pnpm run build`)
- [ ] No ESLint warnings
- [ ] Manually tested all affected features
- [ ] Documentation updated (if needed)
- [ ] No secrets or API keys committed
- [ ] `.env.local` not included in commits

## Reporting Issues

When reporting bugs, please include:

1. **Environment**
   - Node.js version
   - Browser and version
   - Operating system

2. **Steps to Reproduce**
   - Exact steps to trigger the issue
   - Expected behavior
   - Actual behavior

3. **Logs**
   - Browser console errors
   - Network tab screenshots (redact API keys!)
   - Relevant code snippets

4. **Additional Context**
   - Screenshots or screen recordings
   - Any workarounds you found

## Code of Conduct

- Be respectful and professional
- Provide constructive feedback
- Help others learn and grow
- Focus on the code, not the person

## Questions?

- Check existing issues and discussions
- Review project documentation
- Ask in PR comments for specific questions
- Reach out to maintainers for broader questions

## License

By contributing, you agree that your contributions will be licensed under the MIT License (see [LICENSE](./LICENSE)).

---

**Thank you for contributing to AI Math Tutor!** 🎉
```

---

**To revert:** Replace the entire contents of `CONTRIBUTING.md` with the content above.

## Step 3: Revert Pull Request Template

The `.github/pull_request_template.md` file was modified to add Critical Files Check and rebase checklist items.

**Original content starts below the line:**

---

```markdown
## Description

<!-- Provide a clear and concise description of what this PR does -->

## Type of Change

<!-- Check all that apply -->

- [ ] 🐛 Bug fix (non-breaking change which fixes an issue)
- [ ] ✨ New feature (non-breaking change which adds functionality)
- [ ] 💥 Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] 📝 Documentation update
- [ ] 🔧 Configuration change
- [ ] ♻️ Code refactoring (no functional changes)

## Motivation and Context

<!-- Why is this change required? What problem does it solve? -->
<!-- If it fixes an open issue, please link to the issue here. -->

Closes #(issue)

## How Has This Been Tested?

<!-- Describe the tests you ran to verify your changes -->

- [ ] Manually tested locally with `pnpm run dev`
- [ ] Tested voice session connection
- [ ] Tested whiteboard functionality
- [ ] Tested stage progression (if applicable)
- [ ] Build completes successfully (`pnpm run build`)
- [ ] No ESLint warnings (`pnpm run lint`)

### Test Configuration

- **Node version**: <!-- e.g., 20.19.3 -->
- **Browser**: <!-- e.g., Chrome 118 -->
- **OS**: <!-- e.g., macOS 14.0 -->

## Screenshots (if appropriate)

<!-- Add screenshots or recordings to help explain your changes -->

## Checklist

<!-- Check all that apply -->

- [ ] My code follows the code style of this project
- [ ] I have updated the documentation accordingly
- [ ] I have read the [CONTRIBUTING.md](../CONTRIBUTING.md) document
- [ ] My changes generate no new warnings or errors
- [ ] I have added comments to my code, particularly in hard-to-understand areas
- [ ] No secrets or API keys are included in this PR
- [ ] `.env.local` is not included in the commit

## Additional Notes

<!-- Any additional information that reviewers should know -->

## Deployment Notes

<!-- Any special deployment considerations? -->
<!-- Does this require environment variable changes? -->
<!-- Does this require database migrations? -->
```

---

**To revert:** Replace the entire contents of `.github/pull_request_template.md` with the content above.

## Step 4: Revert GitHub Repository Settings

Go to your GitHub repository and undo these settings:

### Branch Protection (Settings → Branches)

If you created or modified a branch protection rule for `main`:

**Option A - Remove the rule entirely:**
1. Go to Settings → Branches
2. Find the rule for `main`
3. Click "Delete" button

**Option B - Disable specific settings:**
1. Go to Settings → Branches → Edit rule for `main`
2. Uncheck these boxes:
   - ❌ Require review from Code Owners
   - ❌ Require linear history
   - (Keep other settings if you had them before)
3. Click "Save changes"

### Merge Settings (Settings → General → Pull Requests)

Restore original merge settings:

1. Go to Settings → General
2. Scroll to "Pull Requests" section
3. Re-enable whichever merge methods you want:
   - ✅ Allow merge commits (if you want)
   - ✅ Allow squash merging (if you want)
   - ✅ Allow rebase merging (keep this, it's harmless)

## Step 5: Verify Revert Completed

After reverting, check:

- [ ] `.github/CODEOWNERS` file is deleted
- [ ] `GITHUB_SETUP.md` is deleted
- [ ] `REVERT_WORKFLOW_CHANGES.md` is deleted
- [ ] `CONTRIBUTING.md` reverted to original (no rebase/critical files sections)
- [ ] `.github/pull_request_template.md` reverted to original (no Critical Files Check)
- [ ] GitHub branch protection updated or removed
- [ ] GitHub merge settings restored

## Step 6: Communicate to Team

After reverting, notify your team:

> "Update: We're reverting the rebase workflow experiment. Previous contribution guidelines are back in effect. Check the updated CONTRIBUTING.md for current practices."

---

## Quick Command Summary for AI Agent

```bash
# Delete new files
rm .github/CODEOWNERS
rm GITHUB_SETUP.md
rm REVERT_WORKFLOW_CHANGES.md

# Revert modified files (use Edit tool with original content above)
# - Revert CONTRIBUTING.md
# - Revert .github/pull_request_template.md

# Then remind user to revert GitHub settings manually
```

---

## Backup Information

**Changes made on:** 2025-10-17

**Files created:**
1. `.github/CODEOWNERS`
2. `GITHUB_SETUP.md`
3. `REVERT_WORKFLOW_CHANGES.md`

**Files modified:**
1. `CONTRIBUTING.md` - Added sections: "CRITICAL: Rebase Frequently" and "Critical Files: Coordination Required"
2. `.github/pull_request_template.md` - Added "Critical Files Check" section and updated checklist

**GitHub settings modified:**
1. Branch protection for `main` (potentially)
2. Merge method settings (potentially)

---

**Note to future AI agent:** This file contains all the information needed to completely revert the workflow changes. Execute steps 1-6 in order.
