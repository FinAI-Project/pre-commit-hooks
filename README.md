# Pre-commit hooks

This project provides a set of Git pre-commit hooks that can be used to enforce code quality, style, and other checks before committing changes to your repository. Below, you'll find instructions on how to install and use these hooks in your project.

## Installation

1.  Install `pre-commit`

    Before using the hooks, you need to install the `pre-commit` package. You can do this using `pip`:

    ```sh
    pip install pre-commit
    ```

    In a python project, add the following to your requirements.txt (or requirements-dev.txt):

    ```sh
    pre-commit
    ```

2.  Clone the `pre-commit-hooks` Repository

    There are two ways to set up the `pre-commit-hooks` in your project: as **global hooks** or as a **submodule** in your project.

    #### Option1: Global Hooks

    1.  Clone the `pre-commit-hooks` repository to any directory:

        ```sh
        cd <any-dir>
        git clone https://github.com/FinAI-Project/pre-commit-hooks
        ```

    2.  Set the global Git hooks path to the cloned directory:

        ```sh
        git config --global core.hooksPath <any-dir>/pre-commit-hooks
        ```

    3.  (Optional) Updating the Hooks

        ```sh
        git pull origin main
        ```

    #### Option 2: Submodule in Your Project

    1.  Add the `pre-commit-hooks` repository as a submodule in your project:

        ```sh
        git submodule add https://github.com/FinAI-Project/pre-commit-hooks .githooks
        ```

    2.  Set the Git hooks path to the `.githooks` directory:

        ```sh
        git config core.hooksPath .githooks
        ```

    3.  (Optional) Updating the Hooks

        ```sh
        git submodule update --remote .githooks
        git add .githooks
        git commit -m "Update pre-commit-hooks submodule to latest version"
        ```

    #### Option3: Submodule already exists in Your Project

    1.  Initialize submodules

        ```sh
        git submodule update --init
        ```

    2.  Set the Git hooks path to the `.githooks` directory:

        ```sh
        git config core.hooksPath .githooks
        ```

3.  (Optional) Customize `.pre-commit-config.yaml`

    If you want to customize the pre-commit hooks, you can create a `.pre-commit-config.yaml` file in the root directory of your project. This file will override the default configuration provided by the `pre-commit-hooks` repository.

    Here’s an example of what the `.pre-commit-config.yaml` might look like:

    ```yaml
    repos:
    - repo: https://github.com/FinAI-Project/pre-commit-hooks
      rev: 1.0.0
      hooks:
      - id: unittest
        args: ["discover", "-s", "tests"] # Suppose all test files are in the tests directory
    ```

## Usage

Once the hooks are set up, they will automatically run every time you execute `git commit`. The hooks will check your code according to the configured rules. If any issues are found, the commit will be blocked, and you'll need to fix the issues before committing again.

```sh
$ git commit -m "pre-commit demo"
unittest.................................................................Passed
[main 69a0c69] pre-commit demo
2 files changed, 11 insertions(+), 4 deletions(-)
```

*PS: Unit tests will be skipped if no Python file changed.*

## FAQ

1.  Temporarily disabling hooks

    ```sh
    SKIP=unittest git commit -m "foo"
    ```
