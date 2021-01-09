# reviewdog_fail_on_error_bug

This is a small repository i created as a code example with <https://github.com/reviewdog/reviewdog/issues/848>.

## Error explaination

Supplying the `-fail-on-error` flag with the `nofilter` or `file` filter modes throws a `reviewdog: input data has violations warning`.

## How to reproduce

1. Install reviewdog [stable](https://github.com/reviewdog/reviewdog#installation)/[nightly](https://github.com/reviewdog/nightly#install-nightly-reviewdog).
. Go into the testdata folder and choice your linter of choise.
2. Run any linter with reviewdog (e.g. `eslint ./testdata/javascript | reviewdog -filter-mode="nofilter"`).
3. See that everything works.
4. Now add the `-fail-on-error` flag (e.g. `eslint ./testdata/javascript | reviewdog -filter-mode="nofilter" -fail-on-error="true"`).
5. See the warning appear and see the wrong exit code when your on the warning branch (see section below).

## Other linter commands

### Flake8

```
flake8 ./testdata/python/ | reviewdog -f=flake8 -filter-mode=nofilter -fail-on-error
```

## Warning and error branch

I also created a separate warnings branch on which all the linting errors for the `javascript` and `python` data have been removed. The only thing that is left are warnings.
## What goes wrong

### The warning message

I did not expect to get this warning message.

### The exit codes

I expected the following exit codes:

| type              | exit code |
|-------------------|-----------|
| errors + warnings | 1         |
| errors            | 1         |
| warnings          | 0         |

Instead I got

| type              | exit code |
|-------------------|-----------|
| errors + warnings | 1         |
| errors            | 1         |
| warnings          | 1         |
