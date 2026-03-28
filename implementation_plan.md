# Implementation Plan: Playwright Automation Quiz (Static Migration)

## 1. Goal
The objective is to refactor the current `index.html` purely as a static website for **Playwright Automation** (using TypeScript/JavaScript examples) and replace **Supabase** with **LocalStorage** for data persistence. This will allow the website to be hosted as a public site on GitHub Pages without any external dependencies.

## 2. User Review Required
> [!IMPORTANT]
> This change involves removing the Supabase backend. All previous user scores stored in Supabase will no longer be accessible through this new version. All future scores will be stored locally in the user's browser (LocalStorage).

> [!NOTE]
> The quiz content will be pivoted to Playwright (Node.js/TypeScript), which is the most common use case for the framework.

## 3. Proposed Changes

### [Component Name]

#### [MODIFY] [index.html](file:///Users/study/Documents/Projects/Assessments/C_#_Selenium_Quiz/index.html)
*   **Remove Supabase**: Delete the Supabase library script tag and initialization code.
*   **Branding & Copy**: Update all headers, titles, and level descriptions from "C# Selenium" to "Playwright".
*   **Auth Logic Replacement**:
    *   Replace the login/signup screen with a simple "Enter Your Name" onboarding screen.
    *   Update `handleLogin`, `handleSignup`, and `handleLogout` to work with `localStorage` (setting a `username` key).
*   **Persistence Logic**:
    *   Rewrite `saveResult` to push to an array in `localStorage` under the key `playwright_quiz_results`.
    *   **Playwright Branding**: Implement a theme based on Playwright's official colors (Green and Blue gradients).
*   **Code Examples**: Provide a pedagogical mix of **TypeScript** and **JavaScript** for the quiz questions.
*   **UI Tweaks**: Update emoji icons and status messages to reflect the Playwright brand/ecosystem.

## 4. Open Questions
- Theme colors will be transitioned to **Playwright Green (#2EAD33)** and **Playwright Blue (#45BAEE)**.
- Code snippets will feature both strict TypeScript types and standard JavaScript syntax.

## 5. Verification Plan

### Automated Tests
- N/A for single-file static HTML.

### Manual Verification
- **Onboarding**: Check if entering a name skips the auth screen and persists it.
- **Quiz Flow**: Take a quiz in each level and verify the scoring works correctly.
- **Persistence**: Refesh the page after a quiz and ensure "My Results History" accurately displays the new scores from `localStorage`.
- **Responsive Review**: Ensure the code blocks and labels still look premium on mobile views.
- **Static Check**: Verify that `supabase` is not called in the browser console.
