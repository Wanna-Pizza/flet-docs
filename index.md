---
layout: default
title: Home
---

# Complete Guide: Adding User Extensions to Flet

This comprehensive guide will walk you through the process of adding custom user extensions to your Flet applications. Perfect for beginners who want to extend Flet's functionality with community-created widgets and components.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Step 1: Install UV Package Manager](#step-1-install-uv-package-manager)
- [Step 2: Create Virtual Environment](#step-2-create-virtual-environment)
- [Step 3: Install Flet](#step-3-install-flet)
- [Step 4: Create New Project (Optional)](#step-4-create-new-project-optional)
- [Step 5: Project Setup](#step-5-project-setup)
- [Step 6: Adding Extensions](#step-6-adding-extensions)
- [Step 7: Building and Running](#step-7-building-and-running)
- [Examples](#examples)
- [Troubleshooting](#troubleshooting)

## Prerequisites

Before starting, make sure you have:
- Python 3.8 or higher installed
- Terminal/Command Prompt access
- Basic familiarity with command line operations

## Step 1: Install UV Package Manager

UV is a fast Python package manager that we'll use for dependency management.

### Install UV globally:

```bash
pip install uv
```

**What this does:** Installs the UV package manager globally on your system, making it available from any directory.

## Step 2: Create Virtual Environment

A virtual environment keeps your project dependencies isolated from your system Python.

### Create virtual environment:

```bash
uv venv
```

### Activate the virtual environment:

**For macOS/Linux:**
```bash
source .venv/bin/activate
```

**For Windows:**
```cmd
.venv\Scripts\activate
```

**What this does:** 
- Creates a new virtual environment in the `.venv` folder
- Activates it so all Python packages are installed in isolation

**How to know it's active:** You'll see `(.venv)` at the beginning of your terminal prompt.

## Step 3: Install Flet

Install Flet with all optional dependencies:

```bash
uv pip install flet[all]==0.28.3
```

**What this does:** Installs Flet version 0.28.3 with all optional features enabled, giving you access to all Flet widgets and capabilities.

## Step 4: Create New Project (Optional)

If you don't have an existing project, create a new one:

```bash
uv run flet create test_app
```

**Replace `test_app` with your desired project name.**

**What this does:** Creates a new Flet project with the following structure:

```
test_app/
├── pyproject.toml          # Project configuration
├── README.md              # Project documentation
├── src/
│   ├── main.py           # Main application file
│   └── assets/           # Static files (images, etc.)
```

## Step 5: Project Setup

### Navigate to your project directory:

```bash
cd test_app
```

### Sync dependencies:

```bash
uv sync
```

**What this does:** 
- Creates a new `.venv` folder inside your project
- Installs all dependencies listed in `pyproject.toml`
- Locks dependency versions in `uv.lock`

**Important:** Delete any old `.venv` folders outside your project. Keep only the one created inside your project root.

## Step 6: Adding Extensions

Extensions are added by modifying the `pyproject.toml` file in your project root.

### Open `pyproject.toml` and locate the dependencies section:

```toml
dependencies = [
    "flet==0.28.3"
]
```

### Add your extensions to this list

#### Method 1: From GitHub Repository

For extensions hosted on GitHub, use this format:

```toml
dependencies = [
    "flet==0.28.3",
    "flet-animated-border @ git+https://github.com/Wanna-Pizza/flet-animated-border.git@main"
]
```

**Format explanation:**
- `flet-animated-border` - The package name
- `@ git+` - Indicates installation from Git
- `https://github.com/Wanna-Pizza/flet-animated-border.git` - Repository URL
- `@main` - Specifies the branch (use `@main`, `@master`, or specific tag)

#### Method 2: From PyPI

For extensions published on PyPI:

```toml
dependencies = [
    "flet==0.28.3",
    "flet-custom-widget==1.2.3"
]
```

### Install the new dependencies:

```bash
uv sync
```

**What this does:** Downloads and installs the new extensions and their dependencies.

## Step 7: Building and Running

### Build for your platform:

**For macOS:**
```bash
uv run flet build macos -v
```

**For Windows:**
```cmd
uv run flet build windows -v
```

**For Linux:**
```bash
uv run flet build linux -v
```

**What this does:** 
- Compiles your app for the specified platform
- The `-v` flag provides verbose output for debugging
- **Important:** This step is required to see custom widgets during development

### Run your application:

**For macOS/Linux:**
```bash
uv run flet run src/main.py
```

**For Windows:**
```cmd
uv run flet run src\main.py
```

**Alternative (hot reload for development):**

**For macOS/Linux:**
```bash
uv run flet -r src/main.py
```

**For Windows:**
```cmd
uv run flet -r src\main.py
```

**What this does:** 
- Runs your Flet application
- The `-r` flag enables hot reload (automatically restarts when files change)

## Examples

### Example 1: Adding Multiple Extensions

```toml
dependencies = [
    "flet==0.28.3",
    "flet-animated-border @ git+https://github.com/Wanna-Pizza/flet-animated-border.git@main",
    "flet-charts @ git+https://github.com/example/flet-charts.git@v1.0",
    "flet-widgets==2.1.0"
]
```

### Example 2: Using the Extension in Your Code

```python
import flet as ft
from flet_animated_border import AnimatedBorder  # Import your extension
```

### Example 3: Complete Workflow

**For macOS/Linux:**
```bash
# 1. Create project
uv run flet create my_awesome_app
cd my_awesome_app

# 2. Edit pyproject.toml to add extensions
# (add your extensions to the dependencies list)

# 3. Install dependencies
uv sync

# 4. Build for your platform
uv run flet build macos -v

# 5. Run with hot reload
uv run flet -r src/main.py
```

**For Windows:**
```cmd
# 1. Create project
uv run flet create my_awesome_app
cd my_awesome_app

# 2. Edit pyproject.toml to add extensions
# (add your extensions to the dependencies list)

# 3. Install dependencies
uv sync

# 4. Build for your platform
uv run flet build windows -v

# 5. Run with hot reload
uv run flet -r src\main.py
```

## Troubleshooting

### Common Issues and Solutions

#### Issue: "uv: command not found"
**Solution:** UV is not installed. Run `pip install uv` first.

#### Issue: Virtual environment not activating
**Solution:** Make sure you're in the correct directory and using the right command for your OS.

#### Issue: Extension not found after installation
**Solutions:**
1. Run `uv sync` after adding to `pyproject.toml`
2. Make sure you've built the project: `uv run flet build [platform] -v`
3. Check that the extension name is spelled correctly

#### Issue: Import errors when using extensions
**Solutions:**
1. Ensure the extension is properly installed: `uv list` to see installed packages
2. Check the extension's documentation for correct import syntax
3. Make sure you've built the project for your platform

#### Issue: Build fails
**Solutions:**
1. Check that all dependencies are compatible
2. Try building with verbose output: `uv run flet build [platform] -v`
3. Ensure you have the necessary system dependencies installed

### Useful Commands

```bash
# Check installed packages
uv list

# Update all dependencies
uv sync --upgrade

# Remove a dependency
# (Edit pyproject.toml to remove the line, then run)
uv sync

# Check UV version
uv --version
```

## Tips for Success

1. **Always build after adding extensions** - This ensures custom widgets are available during development
2. **Use virtual environments** - Keeps your projects isolated and manageable
3. **Pin versions** - Specify exact versions in `pyproject.toml` for reproducible builds
4. **Test frequently** - Run your app after each extension addition to catch issues early
5. **Read documentation** - Each extension may have specific setup requirements

---

**Congratulations!** You now have a complete understanding of how to add and use user extensions in Flet. Start building amazing applications with the power of community-created widgets!
