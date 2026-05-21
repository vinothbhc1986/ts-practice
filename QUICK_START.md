# 🚀 Quick Start Guide - Get Running in 30 Minutes

## Welcome to the Complete Playwright + AI Test Automation Course!

This guide will get you up and running with your first test in under 30 minutes.

---

## ⏱️ 30-Minute Setup

### Step 1: Prerequisites Check (5 minutes)

```bash
# Check Node.js (need v18+)
node --version

# Check npm
npm --version

# Check Git
git --version
```

**Don't have Node.js?** Download from [nodejs.org](https://nodejs.org/)

### Step 2: Clone & Setup (5 minutes)

```bash
# Clone the repository
git clone https://github.com/PramodDutta/LearningPlaywrightTS.git
cd LearningPlaywrightTS

# Install dependencies
npm init -y
npm install -D @playwright/test typescript
npx playwright install
```

### Step 3: Run Your First Test (5 minutes)

Create a file `my-first-test.spec.ts`:

```typescript
import { test, expect } from '@playwright/test';

test('my first Playwright test', async ({ page }) => {
  // Go to Playwright website
  await page.goto('https://playwright.dev');
  
  // Check the title
  await expect(page).toHaveTitle(/Playwright/);
  
  // Click on Get Started
  await page.getByRole('link', { name: 'Get started' }).click();
  
  // Verify navigation
  await expect(page).toHaveURL(/.*intro/);
  
  console.log('🎉 Congratulations! Your first test passed!');
});
```

Run it:
```bash
npx playwright test my-first-test.spec.ts --headed
```

### Step 4: Explore the Course (15 minutes)

```
📁 Start Here:
├── 01_JavaScript/chapter_01_variables_datatypes/
│   └── lab001_declaring_variables.js  ← Start here if new to JS
│
├── 03_Playwright_Fundamentals/chapter_01_introduction_setup/
│   └── lab251_first_test.spec.ts  ← Start here if you know JS
│
└── 10_AI_Testing/chapter_01_ai_fundamentals/
    └── lab908_ai_testing_intro.ts  ← Start here if experienced
```

---

## 🎯 Choose Your Learning Path

### 🟢 Beginner (No coding experience)
```
Week 1-3: Section 01 - JavaScript Fundamentals
Week 4-5: Section 02 - TypeScript Basics
Week 6-8: Section 03 - Playwright Fundamentals
```
**Time:** ~8 weeks | **Labs:** 350

### 🟡 Intermediate (Know JavaScript)
```
Week 1-2: Section 03 - Playwright Fundamentals
Week 3-4: Section 04 - Playwright Advanced
Week 5-6: Section 05 - Page Object Model
```
**Time:** ~6 weeks | **Labs:** 296

### 🔴 Advanced (Know Playwright)
```
Week 1-2: Section 10 - AI Testing
Week 3-4: Section 11 - AI Projects
Week 5-6: Section 14 - AI Agents
```
**Time:** ~6 weeks | **Labs:** 270

---

## 📚 How to Use Each Lab

Every lab file follows this structure:

```typescript
/**
 * CONCEPT:     ← Read this first (theory)
 * BULLET POINTS: ← Key takeaways
 * EXAMPLES:    ← Real-world usage
 */

// CODE EXAMPLES ← Study and run these

/**
 * EXERCISE:    ← Do these yourself
 * CODING QUESTIONS: ← Practice problems
 * LEARNING:    ← Summary
 * ONE LINER:   ← Remember this!
 */
```

**Recommended Flow:**
1. 📖 Read the CONCEPT section
2. 💻 Run the code examples
3. ✍️ Complete the EXERCISE
4. 🧪 Try the CODING QUESTIONS
5. 📝 Review chapter notes

---

## 🛠️ Essential Commands

```bash
# Run a specific test
npx playwright test lab001 --headed

# Run tests in debug mode
npx playwright test --debug

# Generate tests with codegen
npx playwright codegen https://example.com

# View test report
npx playwright show-report

# Run tests in UI mode
npx playwright test --ui
```

---

## 📊 Track Your Progress

Use the checklist in `CURRICULUM.md` to track completion:

```
[x] Section 01: JavaScript (150 labs)
[ ] Section 02: TypeScript (100 labs)
[ ] Section 03: Playwright Fundamentals (100 labs)
...
```

---

## 🆘 Getting Help

1. **Check Chapter Notes** - Each chapter has a `chapter_XX_notes.md`
2. **Use Cheat Sheets** - Quick reference in `/cheatsheets/`
3. **Take Quizzes** - Self-assess in `/quizzes/`
4. **Open Issues** - GitHub Issues for questions

---

## ⚡ Quick Tips

| Tip | Why |
|-----|-----|
| Use `--headed` flag | See the browser in action |
| Use `--debug` flag | Step through tests |
| Use `codegen` | Record tests automatically |
| Read notes first | Understand before coding |
| Do exercises | Practice makes perfect |

---

**Ready? Start with Lab 001 or Lab 251!** 🎉

*Happy Testing!*

