# Summary: Project Structure

## Overview
This document covers best practices for organizing Python projects, from simple scripts to complex packages.

## Python Script Structure

For small helper tools and utilities, a single-file Python script is appropriate. The recommended structure includes:

```python
# imports
import logging

# constants
LOGGER = logging.getLogger()

# functions
def magical_function():
    LOGGER.warning("We are about to do some magical stuff")

# main entry point
def main():
    # The actual logic of the script
    magical_function()

# script execution guard
if __name__ == "__main__":
    main()
```

**Key Components:**
- Import statements at the top
- Constants defined after imports
- Function definitions
- `main()` function containing script logic
- `if __name__ == "__main__":` guard for script execution

## Python Package Structure

For larger projects, organize code as a package with the following structure:

```
my_project/
├── README.md
├── requirements.txt
├── setup.py
├── src/
│   └── my_project/
│       ├── __init__.py
│       ├── my_module.py
│       ├── other_module.py
│       └── my_pkg1/
│           ├── __init__.py
│           └── my_third_module.py
└── tests/
    ├── conftest.py
    ├── test_module.py
    ├── test_other_module.py
    └── my_pkg1/
        └── test_my_third_module.py
```

### Key Files

**requirements.txt**
- Lists Python package dependencies
- Install with: `pip install -r requirements.txt`
- [Documentation](https://pip.pypa.io/en/latest/user_guide/#requirements-files)

**setup.py**
- Contains project metadata
- Used for packaging and distribution
- Minimal example:

```python
from setuptools import setup, find_packages

setup(
    name='my_project',
    version='0.1',
    packages=find_packages(where="src"),
    package_dir={"": "src"}
)
```

**Installation in editable mode:**
- Run `pip install -e .` in project root
- Changes to source code are immediately reflected without reinstallation

## Best Practices

1. **Single scripts**: Use for simple, focused tasks
2. **Package structure**: Use for complex projects with multiple modules
3. **Separate source and tests**: Keep `src/` and `tests/` directories distinct
4. **Mirror test structure**: Test directory structure should mirror source structure
5. **Use editable installs**: During development, install with `-e` flag for convenience

