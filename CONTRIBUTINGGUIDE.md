# 🤝 Contributing to SpinWheeler

Thank you for your interest in contributing to SpinWheeler! This guide will help you get started with contributing to our interactive spin wheel game platform.

---

## 📋 Table of Contents

-   [Code of Conduct](#code-of-conduct)
-   [How Can I Contribute?](#how-can-i-contribute)
-   [Development Setup](#development-setup)
-   [Fork-Branch-PR Workflow](#fork-branch-pr-workflow)
-   [Coding Standards](#coding-standards)
-   [Testing Guidelines](#testing-guidelines)
-   [Commit Message Guidelines](#commit-message-guidelines)
-   [Pull Request Guidelines](#pull-request-guidelines)
-   [Getting Help](#getting-help)

---

## 📜 Code of Conduct

By participating in this project, you agree to abide by our Code of Conduct. Please read it before contributing.

**Be respectful, inclusive, and collaborative.** We welcome contributors from all backgrounds and experience levels.

---

## 🤔 How Can I Contribute?

### 🐛 Report Bugs

-   Use the GitHub issue template for bug reports
-   Include steps to reproduce the issue
-   Provide screenshots or videos if applicable
-   Mention your browser/device information

### 💡 Suggest Features

-   Check existing issues first to avoid duplicates
-   Use the feature request template
-   Explain the use case and expected behavior
-   Consider implementation complexity

### 🔧 Fix Issues

-   Look for issues labeled `good first issue` or `help wanted`
-   Comment on issues you'd like to work on
-   Follow the development workflow below

### 📚 Improve Documentation

-   Fix typos and grammar errors
-   Add missing information
-   Improve code comments
-   Update README sections

---

## 🛠 Development Setup

### Prerequisites

-   Node.js (v18 or higher)
-   npm or yarn
-   Git
-   Firebase account (for backend features)

### Local Setup

1. **Fork the repository** (see workflow below)
2. **Clone your fork:**

    ```bash
    git clone https://github.com/YOUR_USERNAME/spinwheeler.git
    cd spinwheeler
    ```

3. **Install dependencies:**

    ```bash
    npm install
    ```

4. **Set up environment variables:**

    ```bash
    cp .env.example .env
    # Edit .env with your Firebase credentials
    ```

5. **Start development server:**

    ```bash
    npm run dev
    ```

6. **Run tests:**
    ```bash
    npm test
    ```

---

## 🔄 Fork-Branch-PR Workflow

### Step 1: Fork the Repository

1. Go to [https://github.com/yourusername/spinwheeler](https://github.com/yourusername/spinwheeler)
2. Click the "Fork" button in the top-right corner
3. This creates a copy of the repository under your GitHub account

### Step 2: Clone Your Fork

```bash
git clone https://github.com/YOUR_USERNAME/spinwheeler.git
cd spinwheeler
```

### Step 3: Add Upstream Remote

```bash
git remote add upstream https://github.com/yourusername/spinwheeler.git
git fetch upstream
```

### Step 4: Create a Feature Branch

```bash
# Always work from the main branch
git checkout main
git pull upstream main

# Create and switch to a new branch
git checkout -b feature/your-feature-name
# or
git checkout -b fix/your-bug-fix
# or
git checkout -b docs/your-documentation-update
```

**Branch Naming Conventions:**

-   `feature/` - for new features
-   `fix/` - for bug fixes
-   `docs/` - for documentation updates
-   `refactor/` - for code refactoring
-   `test/` - for adding or updating tests

### Step 5: Make Your Changes

1. Write your code following our [coding standards](#coding-standards)
2. Add tests for new functionality
3. Update documentation if needed
4. Test your changes locally

### Step 6: Commit Your Changes

```bash
# Stage your changes
git add .

# Commit with a descriptive message
git commit -m "feat: add custom wheel color picker

- Add color picker component for wheel segments
- Implement color validation
- Add unit tests for color picker
- Update documentation"

# Push to your fork
git push origin feature/your-feature-name
```

### Step 7: Create a Pull Request

1. Go to your fork on GitHub
2. Click "Compare & pull request" for your branch
3. Fill out the PR template with:
    - Description of changes
    - Related issue number
    - Screenshots (if applicable)
    - Testing instructions

### Step 8: Review and Iterate

-   Address any review comments
-   Make requested changes
-   Push updates to your branch
-   The PR will automatically update

---

## 📝 Coding Standards

### JavaScript/React Standards

-   Use **functional components** with hooks
-   Follow **ESLint** and **Prettier** configurations
-   Use **TypeScript** for new components (if applicable)
-   Write **descriptive variable and function names**
-   Add **JSDoc comments** for complex functions

### File Structure

```
src/
├── components/          # Reusable UI components
│   ├── Button/
│   │   ├── Button.jsx
│   │   ├── Button.test.js
│   │   └── index.js
│   └── Wheel/
├── pages/              # Page components
├── hooks/              # Custom React hooks
├── context/            # React Context providers
├── services/           # API and external services
├── utils/              # Utility functions
└── assets/             # Images, icons, etc.
```

### Component Guidelines

```jsx
// ✅ Good example
import React from "react";
import PropTypes from "prop-types";

/**
 * Custom button component with loading state
 * @param {Object} props - Component props
 * @param {string} props.children - Button text
 * @param {boolean} props.loading - Loading state
 * @param {Function} props.onClick - Click handler
 */
const Button = ({ children, loading, onClick, ...props }) => {
    return (
        <button
            className="btn btn-primary"
            disabled={loading}
            onClick={onClick}
            {...props}
        >
            {loading ? "Loading..." : children}
        </button>
    );
};

Button.propTypes = {
    children: PropTypes.node.isRequired,
    loading: PropTypes.bool,
    onClick: PropTypes.func,
};

Button.defaultProps = {
    loading: false,
    onClick: () => {},
};

export default Button;
```

---

## 🧪 Testing Guidelines

### Unit Tests

-   Write tests for all new components and functions
-   Use **React Testing Library** for component tests
-   Aim for **80%+ code coverage**
-   Test both success and error scenarios

### Test Structure

```javascript
// Button.test.js
import { render, screen, fireEvent } from "@testing-library/react";
import Button from "./Button";

describe("Button", () => {
    it("renders with correct text", () => {
        render(<Button>Click me</Button>);
        expect(screen.getByText("Click me")).toBeInTheDocument();
    });

    it("calls onClick when clicked", () => {
        const handleClick = jest.fn();
        render(<Button onClick={handleClick}>Click me</Button>);

        fireEvent.click(screen.getByText("Click me"));
        expect(handleClick).toHaveBeenCalledTimes(1);
    });

    it("shows loading state", () => {
        render(<Button loading>Click me</Button>);
        expect(screen.getByText("Loading...")).toBeInTheDocument();
    });
});
```

### Integration Tests

-   Test complete user workflows
-   Test Firebase interactions
-   Test wheel spinning functionality

---

## 💬 Commit Message Guidelines

We follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Types

-   `feat:` - New feature
-   `fix:` - Bug fix
-   `docs:` - Documentation changes
-   `style:` - Code style changes (formatting, etc.)
-   `refactor:` - Code refactoring
-   `test:` - Adding or updating tests
-   `chore:` - Maintenance tasks

### Examples

```bash
# ✅ Good commit messages
git commit -m "feat: add custom wheel color picker"
git commit -m "fix: resolve wheel spinning animation bug"
git commit -m "docs: update README with new features"
git commit -m "test: add unit tests for Wheel component"

# ❌ Bad commit messages
git commit -m "fixed stuff"
git commit -m "update"
git commit -m "wip"
```

---

## 🔍 Pull Request Guidelines

### Before Submitting

-   [ ] Code follows our coding standards
-   [ ] Tests pass locally
-   [ ] Documentation is updated
-   [ ] No console errors or warnings
-   [ ] Responsive design works on mobile/desktop

### PR Template

```markdown
## Description

Brief description of changes made

## Type of Change

-   [ ] Bug fix
-   [ ] New feature
-   [ ] Documentation update
-   [ ] Code refactoring
-   [ ] Test addition/update

## Related Issue

Closes #123

## Testing

-   [ ] Unit tests pass
-   [ ] Integration tests pass
-   [ ] Manual testing completed
-   [ ] Mobile responsiveness tested

## Screenshots (if applicable)

Add screenshots here

## Checklist

-   [ ] My code follows the style guidelines
-   [ ] I have performed a self-review
-   [ ] I have commented my code where needed
-   [ ] I have made corresponding changes to documentation
-   [ ] My changes generate no new warnings
```

---

## 🆘 Getting Help

### Before Asking for Help

1. Check existing issues and PRs
2. Read the documentation
3. Search the codebase
4. Try to reproduce the issue locally

### Where to Get Help

-   **GitHub Issues** - for bugs and feature requests
-   **GitHub Discussions** - for questions and ideas
-   **Discord/Slack** - for real-time help (if available)

### What to Include When Asking for Help

-   Clear description of the problem
-   Steps to reproduce
-   Expected vs actual behavior
-   Environment details (OS, Node version, etc.)
-   Error messages or logs
-   Screenshots if applicable

---

## 🎉 Recognition

Contributors will be recognized in:

-   GitHub contributors list
-   Project README (for significant contributions)
-   Release notes

---

## 📄 License

By contributing to SpinWheeler, you agree that your contributions will be licensed under the MIT License.

---

**Thank you for contributing to SpinWheeler! 🎡**

If you have any questions about this guide, please open an issue or reach out to the maintainers.
