# Summary: Best Practices in Python Development

## 1. One Virtual Environment Per Project

### Why
- **Isolation**: Keep project dependencies separate
- **Version management**: Different projects can use different dependency versions
- **System protection**: Avoid corrupting the system Python installation

### Tooling

**Poetry** (Recommended)
- Combines `pip`, `virtualenv`, and packaging under a single CLI
- Uses `pyproject.toml` (replaces `requirements.txt` and `requirements-dev.txt`)
- Generates `poetry.lock` for deterministic builds
- [Documentation](https://python-poetry.org/docs/)

**virtualenvwrapper**
- Wrapper around `virtualenv` for easier workflow
- Simplifies creating, deleting, and (de)activating virtual environments
- Windows users: use `virtualenvwrapper-win`
- [Documentation](https://virtualenvwrapper.readthedocs.io/en/latest/)

**pyenv**
- Manage multiple Python versions
- Switch between global/per-project Python versions
- Supports different runtimes (e.g., PyPy)
- [Documentation](https://github.com/pyenv/pyenv)

**venv**
- Built-in Python module
- Good for simple projects with few dependencies
- [Documentation](https://docs.python.org/3/library/venv.html)

---

## 2. Test Your Code

### Why
- Prevent surprises in production
- Ensure everything works as expected
- Prevent regressions when adding new features
- Build confidence during refactoring
- Tests document implementation and use cases

### Tooling

**pytest** (Recommended over unittest)
- Fixtures for reusable testing code
- Markers for grouping/skipping tests
- Automatic test discovery
- Highly configurable
- Rich plugin ecosystem:
  - `pytest-cov`: Coverage reporting
  - `pytest-xdist`: Parallel test execution
- Easy to write custom plugins
- [Documentation](https://docs.pytest.org/en/latest/)

**tox**
- Test code against multiple Python versions and runtimes
- Essential for libraries supporting multiple Python versions
- Can wrap linting and other operations
- Simplifies development workflow with single command
- [Documentation](https://tox.readthedocs.io/en/latest/)

---

## 3. Write High Quality Code

### Why
- Easy to read and understand
- Better maintainability
- Fewer bugs

### Code Formatters

**black** (The Standard)
- The go-to formatter for the Python community
- Opinionated, deterministic formatting
- Follows PEP8 style guidelines
- [Documentation](https://black.readthedocs.io/en/stable/)

*Note: Follow [PEP8](https://www.python.org/dev/peps/pep-0008/) style guidelines ([human-readable version](https://pep8.org/))*

### Linters

**ruff** (Most Comprehensive)
- Comprehensive static analysis
- Extremely fast
- Detects potential code issues and pitfalls
- [Documentation](https://beta.ruff.rs/docs/)

### pre-commit

**pre-commit Hooks**
- Automatically run checks before commits/pushes
- Ensures all contributors follow best practices
- Configuration via `.pre-commit-config.yaml`
- Can run formatters, linters, and tests
- Reduces failed CI builds
- Supports multiple languages (Python, Ruby, Go, Rust, etc.)
- [Documentation](https://pre-commit.com/)

**Benefits:**
- Format code automatically before commit
- Fail commits with linting errors
- Exercise test suite before pushing to remote
- Use existing hooks or create custom ones

---

## 4. Structure Your Code and Projects

### Why
- Clear package/module structure provides project overview
- Modular design improves reusability
- Better maintainability and approachability for newcomers

### Guidelines
- Don't overload single modules
- Split projects into logical packages
- Be consistent with naming conventions
- Separate non-core logic into independent packages
- Consider extracting shared utilities into separate libraries

**Example Use Case:** Create a separate client library for third-party API interactions used by multiple applications. This centralizes changes when APIs evolve.

### Tooling

**cookiecutter**
- Create projects from predefined templates
- Ensures consistent project structure across team
- Rapid setup without copy-pasting
- Use existing templates or create your own
- Works for Python and non-Python projects
- [Documentation](https://cookiecutter.readthedocs.io/en/latest/)

---

## 5. Use Continuous Integration and Deployment

### Why
- Automatically verify tests pass
- Run time-consuming tests that developers skip locally
- Catch linting errors
- Test against all target versions and platforms
- Last resort for automated quality assurance
- Automate deployments (faster, less error-prone)
- Minimize code review time by automating checks
- Human time is expensive - automate what you can

### Tooling Options
- **GitHub Actions**
- **GitLab CI/CD** (integrated)
- **BitBucket Pipelines**

*Choice depends on your git repository manager and requirements*

---

## 6. Utilize IDE Capabilities

### Why
- More efficient and fluent development
- Many tools available to make programming easier

### PyCharm (Recommended)
- Excellent `pytest` integration
- Built-in Git integration
- Automatic code formatting support (e.g., `black`)
- Intuitive search capabilities
- Refactoring features
- Integrated debugger
- Jupyter Notebook support
- Free Community Edition available
- [Documentation](https://www.jetbrains.com/help/pycharm/quick-start-guide.html)

---

## 7. Use Existing Solutions

### Why
- Extensive Python Standard Library (stable and reliable)
- Over 150,000 packages on [PyPI](https://pypi.org/)
- Someone has likely solved your problem already
- Save time and effort

**Best Practice:** Spend 5 minutes researching (Google, [StackOverflow](https://stackoverflow.com/)) before implementing a new solution.

---

## 8. Learn to Debug Efficiently

### Why
- No code is completely bug-free
- Proper tools help identify issues quickly
- Better debugging = faster problem resolution

### Debuggers

**pdb** (Built-in)
- Part of Python Standard Library
- Sufficient for most use cases
- [Documentation](https://docs.python.org/3/library/pdb.html)

**ipdb**
- Feature-rich alternative to `pdb`
- Similar API with enhancements
- [Documentation](https://pypi.org/project/ipdb/)

**pdb++**
- Drop-in replacement for `pdb`
- Additional features and improvements
- [Documentation](https://pypi.org/project/pdbpp/)

### Profilers

**memray** (Memory Profiling)
- Comprehensive memory profiler
- [Documentation](https://bloomberg.github.io/memray/)

**py-spy** (Runtime Profiling)
- Profile running Python programs
- No source code modification required
- No need to restart target process
- Useful for production web applications
- [Documentation](https://github.com/benfred/py-spy)

### Runtime Error Tracking

**Sentry** (Production Error Monitoring)
- Complete stack traces with variable values
- Browser and OS information
- Notifications for runtime exceptions
- Support for multiple languages
- [Documentation](https://docs.sentry.io/?platform=python)

### Use Logging Instead of Print Statements

**logging module** (Standard Library)
- Redirect output to files
- First place to look when users report issues
- Specify runtime levels (debug, info, warning, error)
- No need to remove debug statements
- [Documentation](https://docs.python.org/3/library/logging.html)

---

## General Guidelines

1. **For applications**: Use the latest Python version
2. **For libraries**: Support older Python versions
3. **Always develop in branches**: Even for solo projects, branching allows easy context switching
4. **Practice code reviews**: Great learning opportunity for all parties
5. **Document your code**: Help others (and future you) understand your work

---

## Quick Reference: Recommended Tools

| Category | Tool | Purpose |
|----------|------|---------|
| Dependency Management | poetry | Virtual environments + package management |
| Testing | pytest | Test runner and framework |
| Formatting | black | Code formatter |
| Linting | ruff | Static code analysis |
| Pre-commit | pre-commit | Git hooks for quality checks |
| Project Templates | cookiecutter | Generate consistent project structures |
| IDE | PyCharm | Full-featured Python IDE |
| Debugging | pdb/ipdb/pdb++ | Interactive debugger |
| Profiling | memray, py-spy | Memory and runtime profiling |
| Error Tracking | Sentry | Production error monitoring |
| Logging | logging | Standard library logging |

