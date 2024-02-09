
# How to use [hype](https://github.com/gopherguides/hype) as an action to auto generate your repo's README.

This repo shows how to use a github action and hype to auto generate your README.md

## Requirements

For this action to work


* You need to give permission to your GitHub Actions to create a pull request in your GitHub repo settings _(Settings -> Actions -> General)_.





* Under `Workflow Permissions` check `Allow GitHub Actions to create and approve pull requests`.



OR


* Instead of useing `${{secrets.GITHUB_TOKEN}}` in GitHub Actions use a GitHub [Personnal Acces Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token#creating-a-fine-grained-personal-access-token) like: `${{secrets.PAT}}`.


## The Action

The current action is set to only generate the readme on a pull request.  You can modify this to your own needs.

```yml
name: Generate README with Hype
on: [pull_request]

jobs:

  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - name: Set up Go
      uses: actions/setup-go@v4
      with:
        go-version: "1.22.x"

    - name: Install hype
      run: go install github.com/gopherguides/hype/cmd/hype@latest

    - name: Run hype
      run: pushd .hype;hype export -format=markdown -f module.md > ../README.md;popd

    - name: Commit README back to the repo
      run: |-
        git config --global user.email "hype@gopherguides.com"
        git config --global user.name "hype"
        git diff --quiet || (git add README.md && git commit -m "Updated README")
        git push

```

