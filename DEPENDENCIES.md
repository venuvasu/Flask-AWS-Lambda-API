# Dependency Management

This document describes the dependency management approach used in the Flask-AWS-Lambda-API project.

## Overview

The project uses a multi-level dependency management strategy to balance flexibility and reproducibility:

1. **Original Requirements Files**: Simple lists of dependencies without version constraints.
   - `hello_world/requirements.txt`
   - `tests/requirements.txt`

2. **Pinned Requirements Files**: Direct dependencies with exact versions.
   - `hello_world/requirements_pinned.txt`
   - `tests/requirements_pinned.txt`

3. **Locked Requirements Files**: Complete dependency trees with all direct and transitive dependencies.
   - `hello_world/requirements_lock.txt`
   - `tests/requirements_lock.txt`
   - `requirements_lock.txt` (consolidated)

## File Purposes

### Original Requirements Files
- Lightweight lists of dependencies for quick installation
- Flexible for development environments
- Not recommended for production due to version unpredictability

### Pinned Requirements Files
- Pin direct dependencies to specific versions
- Balance between flexibility and reproducibility
- Suitable for most development and CI environments

### Locked Requirements Files
- Complete dependency trees with exact versions of all packages
- Guarantee reproducible environments
- Recommended for production deployments and critical CI pipelines

## Consolidated Lock File
The `requirements_lock.txt` file at the root of the project combines all dependencies from both application and test environments. Use this file for the most comprehensive and reproducible environment setup.

## Security Considerations
- Regular security scanning is recommended using tools like `pip-audit`
- Lock files were verified to be free of known vulnerabilities at the time of creation

## How to Use

### For Development
```bash
# Install minimal dependencies (flexible versions)
pip install -r hello_world/requirements.txt

# For tests
pip install -r tests/requirements.txt
```

### For Stable Development/Testing
```bash
# Install direct dependencies with pinned versions
pip install -r hello_world/requirements_pinned.txt

# For tests
pip install -r tests/requirements_pinned.txt
```

### For Production/Deployment
```bash
# Install all dependencies with exact versions
pip install -r requirements_lock.txt
```

## Updating Dependencies

When updating dependencies:

1. Modify the original `requirements.txt` files
2. Generate new pinned versions: `pip freeze > requirements_pinned.txt`
3. Use a tool like `pip-compile` or manually create new lock files
4. Verify with security scanning: `pip-audit -r requirements_lock.txt`

## Dependency Tree

Key dependency relationships in the project:

- **Flask** (2.3.3)
  - blinker (1.9.0)
  - click (8.1.8)
  - itsdangerous (2.2.0)
  - Jinja2 (3.1.6)
    - MarkupSafe (3.0.2)
  - Werkzeug (3.1.3)
    - MarkupSafe (3.0.2)

- **awsgi** (0.0.5)
  - httptools (0.6.4)
  - uvloop (0.21.0)
  - websockets (15.0.1)
  - Werkzeug (3.1.3)

- **requests** (2.31.0)
  - certifi (2024.2.2)
  - charset-normalizer (3.4.2)
  - idna (3.6)
  - urllib3 (2.0.7)

- **pytest** (7.4.0)
  - iniconfig (2.0.0)
  - packaging (25.0)
  - pluggy (1.4.0)

- **boto3** (1.28.0)
  - botocore (1.31.85)
    - jmespath (1.0.1)
    - python-dateutil (2.8.1)
    - urllib3 (2.0.7)
  - jmespath (1.0.1)
  - s3transfer (0.6.2)