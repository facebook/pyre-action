# Pyre Github Action

[Pyre](https://pyre-check.org/) is a performant type checker for Python compliant with [PEP 484](https://www.python.org/dev/peps/pep-0484/). Pyre can analyze codebases with millions of lines of code incrementally – providing instantaneous feedback to developers as they write code.

Pyre GitHub Action enables you to run [Pyre](https://pyre-check.org/docs/getting-started/) in CI and view the results on [GitHub Security code scanning UI](https://docs.github.com/code-security/code-scanning/automatically-scanning-your-code-for-vulnerabilities-and-errors/managing-code-scanning-alerts-for-your-repository#viewing-the-alerts-for-a-repository).


## Usage
```yml
name: Pyre

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  pyre:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Run Pyre Action
        uses: facebook/pyre-action@v0.0.2
        with:
            repo-directory: './'
            requirements-path: 'requirements.txt'

```

## Inputs
### `repo-directory`

**Required**, Path to the Python source code you want to analyze. If you want to analyze the root of your repo, use `'./'`. The default will be to analyze the root of your repository.

Pyre Action will look for a [`.pyre_configuration`](https://pyre-check.org/docs/configuration/#configuration-files) in the root of your `repo-directory`. If one cannot be found, a default Pyre configuration will be used.

### `requirements-path`

**Required**, Path to file containing your Python code's dependencies relative to `repo-directory`. The default will look for [`requirements.txt`](https://pip.pypa.io/en/latest/reference/requirements-file-format/) in the root of the directory you specified in `repo-directory`.

### `version`
Which [version](https://pypi.org/project/pyre-check/#history) of Pyre to use. Defaults to the [latest stable version of Pyre](https://pypi.org/project/pyre-check/) if the `use-nightly` flag below is also not set.

### `use-nightly`

When set to `true`, the action will use the [nightly version of Pyre](https://pypi.org/project/pyre-check-nightly/) to analyze your Python code. The nightly version of Pyre tends to be unstable and is not recommended unless you are adventurous. By default, the action will use the [latest stable version of Pyre](https://pypi.org/project/pyre-check/).


## License

Pyre Action is licensed under the MIT license.
