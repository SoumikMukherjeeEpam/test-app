# Quiz CLI

Quiz CLI is an interactive terminal quiz game for learning JavaScript, Node.js, and general programming concepts. It loads multiple-choice questions from a JSON file, lets users choose a category and question count, tracks answers and scores, and provides explanations and incorrect-answer reviews.

## Features

- Interactive command-line interface
- Questions grouped into categories:
  - JavaScript Basics
  - Node.js Fundamentals
  - General Programming
- Multiple-choice questions with four options each
- Selection of all questions, three questions, or five questions when available
- Randomized question order using Fisher–Yates shuffling
- Progress display while answering questions
- Immediate correctness feedback and explanations
- Score and percentage calculation
- Performance messages based on the final score
- Incorrect-answer review showing selected and correct answers
- Replay option after completing a quiz
- ANSI terminal colors without external dependencies

## Technologies

- JavaScript
- Node.js 18 or later
- ECMAScript modules
- Node.js built-in modules:
  - `node:fs/promises`
  - `node:url`
  - `node:path`
  - `node:readline`

The project has no external npm dependencies.

## Prerequisites

- Node.js `18.0.0` or later
- A terminal or command-line environment

## Setup

No dependency installation is required because the project does not use external npm packages.

1. Ensure Node.js 18 or later is installed.
2. Open a terminal in the project directory.
3. Start the quiz:

```bash
npm start
```

## How to Run

The application can be started using the npm script:

```bash
npm start
```

Alternatively, run the entry point directly with Node.js:

```bash
node index.js
```

The application then:

1. Loads questions from `data/questions.json`.
2. Displays a welcome message and available categories.
3. Prompts for a category.
4. Prompts for the number of questions.
5. Randomizes and presents the questions.
6. Displays feedback and explanations.
7. Shows final results and incorrect answers.
8. Asks whether to play again.

## Usage

After starting the application, select a category and choose the number of questions. Each question presents four numbered answer options.

The available question categories are:

| Category | Topic | Questions |
| --- | --- | ---: |
| `javascript` | JavaScript Basics | 5 |
| `nodejs` | Node.js Fundamentals | 5 |
| `general` | General Programming | 5 |

There are 15 questions in total. The question-count choices include all questions, three questions, or five questions when the selected category has enough questions.

At the end of a quiz, the application displays:

- Category name
- Number of correct answers
- Score percentage
- Performance message
- Incorrect answers with the selected and correct answers

Performance messages use the following thresholds:

| Score | Message |
| ---: | --- |
| 100% | Perfect score |
| 80–99% | Great job |
| 60–79% | Good effort |
| 40–59% | Room for improvement |
| Below 40% | Keep practicing |

## Configuration

The application does not use environment variables or separate configuration files.

Quiz content is stored in:

```text
data/questions.json
```

The file contains a top-level `categories` object. Each category contains question objects with:

- `question`: The question text
- `options`: An array of four answer choices
- `answer`: A zero-based index identifying the correct option
- `explanation`: An explanation shown after answering

When editing the question data, preserve the category and question structure. Answer indexes must remain zero-based.

## Project Structure

```text
test-app/
├── data/
│   └── questions.json   # Quiz categories and question data
├── src/
│   ├── colors.js        # ANSI styling and terminal color helpers
│   ├── input.js         # Readline prompts, selections, confirmations, and pauses
│   └── quiz.js          # Quiz state, question flow, scoring, and results
├── index.js             # Application entry point and main quiz flow
├── package.json         # Project metadata and npm scripts
└── README.md            # Project documentation
```

## Application Architecture

The application is organized into three main areas:

### Entry Point

`index.js` coordinates the application lifecycle. It loads the question data relative to the ES module location, displays the welcome flow, gathers the user's selections, creates a `Quiz` instance, runs the quiz, displays results, and handles replay and readline cleanup.

### Input Utilities

`src/input.js` provides reusable terminal input functions built on Node.js `readline`:

- Create a readline interface
- Prompt for text input
- Select from numbered options
- Confirm yes/no responses
- Wait for the user to press Enter

Invalid numeric selections are rejected and prompted again. Confirmation responses beginning with `y` are treated as affirmative.

### Quiz Engine

`src/quiz.js` manages:

- Shuffled question order
- Current question state
- Progress tracking
- Answer recording
- Correctness checks
- Score calculation
- Progress-bar rendering
- Final results and incorrect-answer review

Recorded answers include the question text, selected option index, correct option index, and whether the answer was correct.

### Terminal Styling

`src/colors.js` provides ANSI-based styling and helper functions for colored, bold, dimmed, and status-oriented terminal output. It does not require an external color library.

## Available Scripts

| Command | Description |
| --- | --- |
| `npm start` | Starts the application with `node index.js` |
| `npm test` | Runs Node's built-in test command with `node --test` |

## Testing

The project defines a test script:

```bash
npm test
```

This runs:

```bash
node --test
```

No test files, test directories, or testing framework configuration were identified in the repository. Therefore, no repository test suite is currently provided.

## Build and Deployment

The project is intended to run directly with Node.js.

There is no:

- Build step
- Bundler
- Transpiler
- Docker configuration
- GitHub Actions workflow
- Deployment configuration

## License

This project declares the MIT license in `package.json`.

