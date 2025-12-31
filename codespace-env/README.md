# GitHub Codespaces Developer Environment

This document compiles all the necessary configuration steps required for setting up a development environment using GitHub Codespaces with a custom devcontainer baseline.

<p align="right">(<a href="../README.md">back to beginning</a>)</p>

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#overview">Overview</a></li>
    <li><a href="#devcontainer-baseline">Devcontainer Baseline</a></li>
    <li><a href="#getting-started">Getting Started</a></li>
    <li><a href="#customization">Customization</a></li>
  </ol>
</details>

## Overview

[GitHub Codespaces](https://github.com/features/codespaces) is a cloud-based development environment that allows you to develop entirely in the cloud. It provides a complete, configurable dev environment with a VS Code experience, running in a container.

## Devcontainer Baseline

The baseline configuration is located at [`devcontainer-baseline/baseline/.devcontainer/`](devcontainer-baseline/baseline/.devcontainer/).

This baseline provides a standardized starting point for creating consistent development environments across repositories.

### Base Configuration

The base devcontainer configuration can be found at:
- [`devcontainer.base.json`](devcontainer-baseline/baseline/.devcontainer/devcontainer.base.json)

## Getting Started

1. **Copy the baseline to your repository**
   ```bash
   cp -r devcontainer-baseline/baseline/.devcontainer /path/to/your/repo/