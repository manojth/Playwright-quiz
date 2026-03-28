# Product Requirements Document (PRD): Playwright Automation Quiz

## 1. Overview
The **Playwright Automation Quiz** is a high-end, static single-page web application (SPA) designed to help developers test and improve their knowledge of the Playwright testing framework. The app features a professional dark-mode aesthetic, local progress tracking (no backend required), and detailed educational feedback. It is optimized for hosting on static platforms like GitHub Pages.

## 2. Technical Stack
*   **Frontend**: HTML5, CSS3 (Vanilla), JavaScript (Vanilla).
*   **Storage**: Browser `localStorage` for persisting quiz results and history.
*   **Hosting Compatibility**: Fully static (GitHub Pages, Vercel, Netlify).
*   **Fonts**: 
    *   `Syne`: Primary headings and UI buttons.
    *   `JetBrains Mono`: Technical labels, code blocks, and statistics.
*   **Icons**: Emoji-based icons (👤, 🟢, 🟡, 🔴, 📊, 🏆).

## 3. Core Features

### 3.1. User Identity (Pseudo-Auth)
*   **Goal**: Provide a personalized experience without a backend.
*   **Implementation**: Users can enter a "Display Name" or "Username" which is stored in `localStorage`.
*   **Persistence**: Identity and scores persist in the browser until the cache is cleared.

### 3.2. Levels & Difficulty
The quiz is divided into three distinct levels, each with 10 questions:
*   **Basic (🟢 Fundamentals)**: Installation, selectors (Locators), basic assertions, and `page.goto()`.
*   **Intermediate (🟡 Proficiency)**: Auto-waiting, handling frames/popups, Trace Viewer, and API testing.
*   **Advanced (🔴 Expert)**: Parallel execution configuration, CI/CD integration (GitHub Actions), custom fixtures, and visual regression testing.

### 3.3. Quiz Engine
*   **Step-by-Step Navigation**: One question at a time.
*   **Progress Tracking**: Visual progress bar (0% to 100%) and "Question X of 10" indicator.
*   **Code Support**: Responsive code blocks with syntax styling for Playwright snippets (TypeScript/JavaScript).
*   **Immediate Feedback**: 
    *   Correct/Incorrect highlighting on options.
    *   Rich-text explanations shown immediately after answering.
*   **Results Logic**: Scores are calculated and saved to `localStorage` upon completion.

### 3.4. Results Dashboard (History)
*   **Score Summary**: "Best Score", "Average percentage", and "Total attempts" tracked per difficulty level.
*   **Recent Activity**: List of the last 8 attempts with level, score, percentage, and date.
*   **Toggle Interface**: Collapsible dashboard using local data.

## 4. Design Specifications

### 4.1. Color Palette (CSS Variables)
```css
--bg: #0a0e1a;          /* Deep dark background */
--surface: #111827;     /* Main card background */
--surface2: #1a2235;    /* Input/Button background */
--border: #1e2d45;      /* Subtle dividers */
--accent: #00d4ff;      /* Cyan highlight */
--accent2: #7c3aed;     /* Violet highlight */
--green: #10b981;       /* Success/Basic level */
--yellow: #f59e0b;      /* Warning/Intermediate level */
--red: #ef4444;         /* Error/Advanced level */
--text: #e2e8f0;        /* High-contrast text */
--muted: #64748b;       /* De-emphasized text */
```

### 4.2. UI Elements
*   **Gradients**: Linear gradients (135deg) between `--accent` and `--accent2`.
*   **Minimalist Setup**: No external scripts like Supabase; all logic contained in the local script.

## 5. Data Schema (LocalStorage)

### Key: `playwright_quiz_results`
Value: An Array of Objects:
```json
[
  {
    "id": "unique-timestamp-id",
    "username": "User",
    "level": "basic",
    "score": 8,
    "total": 10,
    "percentage": 80,
    "completed_at": "ISO-8601-String"
  }
]
```

## 6. Functional Workflow

1.  **Entry**: User enters a display name (stored locally).
2.  **Selection**: User selects a level from the dashboard.
3.  **Execution**: System pulls 10 Playwright-specific questions.
4.  **Interaction**: User selects an answer; system provides immediate feedback/explanation.
5.  **Completion**: 
    *   System calculates final score.
    *   Result is appended to the `playwright_quiz_results` array in `localStorage`.
    *   Local dashboard re-renders based on the updated array.

## 7. Content Structure (Example)
```javascript
{
  q: "Which locator strategy is recommended as the most resilient to DOM changes?",
  code: "await page.locator(???).click();",
  options: ["CSS Selector", "XPath", "User-facing attributes (e.g., getByRole)", "ID Attribute"],
  answer: 2,
  explanation: "Playwright recommends using **user-facing attributes** like <code>getByRole</code> or <code>getByText</code> as they mirror how users interact with the page and are more resilient than structural selectors like CSS or XPath."
}
```
