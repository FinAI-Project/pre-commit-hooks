# Pre-commit hooks

## Quick start

1.  Install pre-commit

    ```sh
    pip install pre-commit
    ```

    In a python project, add the following to your requirements.txt (or requirements-dev.txt):

    ```sh
    pre-commit
    ```

2.  Add a pre-commit configuration

    Create a file named `.pre-commit-config.yaml` in the root directory of your project with following contents.

    ```yaml
    repos:
    - repo: https://github.com/FinAI-Project/pre-commit-hooks
      rev: 1.0.0
      hooks:
      - id: unittest
        args: ["discover", "-s", "tests"] # Suppose all test files are in the tests directory
    ```

    You can use either `pytest` or `unittest` as needed.

    Then add `.pre-commit-config.yaml` to git repo.

    ```sh
    git add .pre-commit-config.yaml
    ```

3.  Install the git hook scripts

    ```sh
    pre-commit install
    ```

4.  Pre-commit hook will be triggered when committing, e.g.

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
