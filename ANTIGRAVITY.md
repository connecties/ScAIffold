# Antigravity Instructions - AI-Scaffolding

This file provides instructions for Google's Antigravity AI assistant. It combines project context, coding standards, and workflow guidelines for optimal AI-assisted development.

## Project Context

This repository contains configurations and workflows for optimizing AI-assisted coding with various AI tools (Claude Code, Cursor, Antigravity). Use this as a reference for setting up similar workflows in other projects.

## Coding Standards

### Python Development
- **Version**: Python 3.10+
- **Formatter**: Ruff (replaces black, isort, flake8)
  - Format: `ruff format .`
  - Lint: `ruff check .`
  - Fix: `ruff check --fix .`
- **Testing**: pytest with 80%+ coverage
  - Run tests: `pytest`
  - With coverage: `pytest --cov`
- **Type hints**: Required for all function parameters and return types
- **Docstrings**: Google-style, required for all public functions, classes, and modules
- **Line length**: 120 characters max
- **Indentation**: 4 spaces

### Type Hints
- Use `Optional[T]` or `T | None` for nullable types
- Use `list[T]`, `dict[K, V]` (lowercase) for Python 3.10+
- Include type hints for all function parameters and return values

### Docstring Example
```python
def calculate_total(items: list[Item], discount: float = 0.0) -> float:
    """Calculate the total price of items with optional discount.

    Args:
        items: List of items to calculate total for.
        discount: Discount percentage to apply (0.0 to 1.0).

    Returns:
        The total price after discount.

    Raises:
        ValueError: If discount is not between 0 and 1.
    """
```

### Naming Conventions
- Functions and variables: `snake_case`
- Classes: `PascalCase`
- Constants: `UPPER_SNAKE_CASE`
- Private members: `_leading_underscore`
- Module files: `snake_case.py`

### Imports
- Sort with Ruff (replaces isort)
- Group: stdlib, third-party, local
- Use absolute imports for clarity
- Avoid wildcard imports (`from x import *`)

### Error Handling
- Use try-except with proper logging
- Provide clear error messages
- Don't silently ignore exceptions
- Use structured logging with `structlog` when available

## Git Workflow

### Branch Strategy
- Use GitHub Flow
- Main branch is always deployable
- Create feature branches from main
- Use descriptive branch names: `feature/add-auth`, `fix/login-bug`

### Conventional Commits
Use the following prefixes:

| Prefix | Description |
|--------|-------------|
| `feat:` | New feature |
| `fix:` | Bug fix |
| `docs:` | Documentation only |
| `style:` | Formatting, no code change |
| `refactor:` | Code change without feature/fix |
| `test:` | Adding or updating tests |
| `chore:` | Maintenance, dependencies |

Examples:
```
feat: add user authentication endpoint
fix: resolve login timeout issue
docs: update API documentation
refactor: extract validation logic to utility
test: add unit tests for auth service
chore: update dependencies
```

### Commit Best Practices
- Write clear, concise commit messages
- Focus on "why" not "what"
- Keep commits atomic (one logical change)
- Always run tests before committing
- Never commit secrets or credentials

### Pre-Commit Checklist
1. Run tests: `pytest`
2. Format code: `ruff format .`
3. Lint code: `ruff check .`
4. Review changes: `git diff`

## Workflow Guidelines

### Planning Mode
- Start complex tasks in PLANNING mode
- Create `implementation_plan.md` for significant changes
- Get the plan right before implementing
- Break large tasks into smaller, focused steps
- Use `task.md` to track progress with checkboxes

### Execution Mode
- Write code following the standards above
- Make changes incrementally
- Run linter after making changes
- Return to PLANNING if unexpected complexity arises

### Verification Mode
- Always verify work with tests when available
- Run linter to check for issues
- Test UI changes in browser when applicable
- Create `walkthrough.md` after completing verification
- Document what was tested and validation results

### Error Handling in Development
- Catch and log errors appropriately
- Implement graceful degradation
- Set appropriate timeouts
- Handle rate limiting for API calls

## Testing Standards

### Framework
- Use pytest for all tests
- Target 80%+ code coverage
- Tests in `tests/` directory mirroring `src/` structure
- Test files: `test_<module>.py`
- Test functions: `test_<description>`

### Fixtures
- Use fixtures for reusable test data
- Prefer `scope="function"` unless shared state is needed
- Use `conftest.py` for shared fixtures

### Parametrization
```python
@pytest.mark.parametrize("input_val,expected", [
    (1, 2),
    (2, 4),
    (0, 0),
])
def test_double(input_val, expected):
    assert double(input_val) == expected
```

### Mocking
- Use `pytest-mock` or `unittest.mock`
- Mock external dependencies (APIs, databases)
- Avoid mocking the code under test

### Test Commands
- Run tests: `pytest`
- With coverage: `pytest --cov`
- Verbose: `pytest -v`
- Single file: `pytest tests/test_specific.py`
- Single test: `pytest tests/test_specific.py::test_name`

## LLM & ML Development

### Frameworks
- **LLM**: LangChain, transformers
- **Data**: pandas, numpy
- **API**: FastAPI with Pydantic

### LangChain Best Practices
- Use LCEL (LangChain Expression Language) for chains
- Implement proper error handling for LLM calls
- Add retry logic for API failures
- Cache expensive operations

### Prompt Engineering
- Store prompts as separate files or constants
- Version control prompt templates
- Test prompts with diverse inputs
- Document expected outputs

### Performance
- Use async for I/O-bound LLM calls
- Implement caching for repeated queries
- Batch requests when possible
- Monitor token usage and costs

## Key Files

| File | Purpose |
|------|---------|
| `ANTIGRAVITY.md` | This file - Antigravity instructions |
| `CLAUDE.md` | Claude Code memory (project-specific) |
| `AGENTS.md` | Cursor agent instructions |
| `skills/` | Modular skills for specific domains |
| `threads.md` | Boris Cherny's tips source material |

## Available Skills

When working on specific tasks, consult these skills:
- **code-style**: Python formatting and naming conventions
- **git-workflow**: Git branching and commit conventions
- **llm-development**: LangChain and ML best practices
- **testing**: pytest conventions and fixtures

## Preferences

- **Concise responses**: Provide focused, actionable responses
- **Show examples**: Include code examples when helpful
- **Explain rationale**: Explain the "why" behind changes
- **Edit over create**: Prefer editing existing files over creating new ones
- **Documentation**: Only create documentation when explicitly requested
- **Proactive**: Take obvious follow-up actions (verify builds, run tests)
- **Ask for clarity**: Always ask for clarification rather than making assumptions

## Files to Never Commit

- `.env` files with secrets
- `credentials.json`
- API keys or tokens
- Large binary files
- IDE-specific files (unless shared team config)

## Known Pitfalls

<!-- Add corrections here as you encounter issues -->
<!-- Example: "When creating pytest fixtures, always use scope='function' unless shared state is explicitly needed" -->

## Quick Reference Commands

| Task | Command |
|------|---------|
| Format code | `ruff format .` |
| Lint code | `ruff check .` |
| Fix lint issues | `ruff check --fix .` |
| Run tests | `pytest` |
| Run with coverage | `pytest --cov` |

---
*Update this file whenever Antigravity makes a mistake or when project standards evolve*
