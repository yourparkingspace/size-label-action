# size-label-action

GitHub action to assign labels based on pull request change sizes.

Labels are taken from https://github.com/kubernetes/kubernetes/labels?q=size

## Usage

Create a `.github/workflows/size-label.yml` file:

```yaml
name: Size Label
on: pull_request
jobs:
  size-label:
    runs-on: [self-hosted, ubuntu-latest, x64, linux]
    steps:
      - name: size-label
        uses: yourparkingspace/size-label-action@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Configuration

The following environment variables are supported:

- `IGNORED`: A list of [glob expressions](http://man7.org/linux/man-pages/man7/glob.7.html)
  separated by newlines. Files matching these expressions will not count when
  calculating the change size of the pull request. Lines starting with `#` are
  ignored and files matching lines starting with `!` are always included.

You can configure the environment variables in the workflow file like this:

```yaml
        env:
          GITHUB_TOKEN: "${{ secrets.GITHUB_TOKEN }}"
          IGNORED: ".*\n!.gitignore\nyarn.lock\ngenerated/**"
```

## License

MIT
