# Quiz CLI

An interactive command-line quiz game for learning JavaScript. Quiz CLI presents categorized programming questions in a terminal, accepts numbered answers, provides immediate feedback and explanations, calculates a final score, reviews incorrect answers, and supports replaying the quiz.

## Features

- Interactive terminal-based quiz experience
- Categories:
  - JavaScript Basics
  - Node.js Fundamentals
  - General Programming
- Question-count selection:
  - All available questions
  - Three questions
  - Five questions when supported
- Randomized question order for each session
- Numbered answer selection with input validation
- Immediate correctness feedback
- Explanations for answered questions
- Score and percentage calculation
- Performance messages based on the final result
- Incorrect-answer review
- Replay support
- Terminal styling using ANSI escape sequences
- No external runtime dependencies

## Technologies

- JavaScript
- Node.js 18 or later
- ECMAScript modules
- Node.js built-in modules:
  - `node:fs/promises`
  - `node:url`
  - `node:path`
  - `node:readline`
- Node.js test runner command via `node --test`

## Prerequisites

- Node.js `>=18.0.0`
- A terminal capable of running interactive command-line programs

No external services, environment variables, database, bundler, or build tool are required.

## Setup and Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/SoumikMukherjeeEpam/test-app.git
   ```

2. Change into the project directory:

   ```bash
   cd test-app
   ```

3. No dependency installation is required. The project uses only Node.js built-in modules and does not declare runtime or development dependencies.

## How to Run

Start the quiz using the package script:

```bash
npm start
```

This runs:

```bash
node index.js
```

If the entry file has executable permission, it can also be started directly:

```bash
./index.js
```

## Usage

After starting the application, follow the interactive terminal prompts:

1. View the welcome banner.
2. Select a quiz category.
3. Select the number of questions.
4. Press Enter to begin.
5. Choose answers using their numbered options.
6. Review correctness feedback and explanations after each answer.
7. View the final score and percentage.
8. Review incorrect answers.
9. Choose whether to replay the quiz.

Questions are shuffled each session.

## Question Data

Questions are stored in [`data/questions.json`](data/questions.json). The file contains categories, with each category containing question objects using this structure:

```json
{
  "question": "Question text",
  "options": [
    "First option",
    "Second option",
    "Third option"
  ],
  "answer": 0,
  "explanation": "Explanation of the correct answer"
}
```

The `answer` field is a zero-based index into the `options` array. Categories can be extended by following the same structure.

The repository currently includes these categories:

- `JavaScript Basics`
- `Node.js Fundamentals`
- `General Programming`

## Project Structure

```text
test-app/
├── data/
│   └── questions.json     # Quiz categories and question data
├── src/
│   ├── colors.js          # ANSI terminal color and styling helpers
│   ├── input.js           # Readline prompts and input validation
│   └── quiz.js            # Quiz state, scoring, shuffling, and feedback
├── index.js               # CLI entry point and application flow
└── package.json           # Project metadata and npm scripts
```

## Available Scripts

| Command | Description |
|---|---|
| `npm start` | Starts the quiz with `node index.js` |
| `npm test` | Runs `node --test` |

## Testing

The declared test script is:

```bash
npm test
```

It invokes the Node.js built-in test runner:

```bash
node --test
```

No test files or test directories are currently present in the repository, so there are no visible automated tests at this time.

## Architecture and Implementation

The application is organized into a CLI entry point and focused source modules:

- `index.js`
  - Loads `data/questions.json` using `node:fs/promises`.
  - Resolves the data path using `import.meta.url` and path utilities.
  - Coordinates category selection, question-count selection, quiz execution, results, review, replay, and error handling.
  - Ensures readline resources are cleaned up when the application exits.

- `src/input.js`
  - Creates a `readline` interface.
  - Provides Promise-based terminal prompts.
  - Handles numbered selections, validation, yes/no confirmation, and “press Enter” interactions.

- `src/quiz.js`
  - Implements the `Quiz` class.
  - Maintains the current category, question index, score, and submitted answers.
  - Shuffles questions using the Fisher–Yates algorithm.
  - Provides question state, answer validation, progress information, feedback, explanations, final scoring, and incorrect-answer review.

- `src/colors.js`
  - Provides terminal styling through raw ANSI escape sequences.
  - Includes generic colorization and convenience or combined styles without an external color package.

The project uses ECMAScript modules, enabled by `"type": "module"` in `package.json`.

## Configuration

There are no environment variables or separate configuration files.

Quiz content and categories are configured in:

```text
data/questions.json
```

Application behavior is implemented in the JavaScript source files under `src/` and in `index.js`.

## Limitations

- The quiz is terminal-based and does not provide a graphical or web interface.
- Questions are maintained directly in `data/questions.json`.
- No automated test files are currently included.
- No separate `LICENSE` file was found, although `package.json` declares MIT license metadata.
- Terminal styling depends on ANSI escape sequence support in the terminal.
