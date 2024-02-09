# How to use [hype](https://github.com/gopherguides/hype) as an action to auto generate your repo's README.

This repo shows how to use a github action and hype to auto generate your README.md

## Requirements

For this action to work

- You need to give permission to your GitHub Actions to create a pull request in your GitHub repo settings *(Settings -> Actions -> General)*.   
    - Under `Workflow Permissions` check `Allow GitHub Actions to create and approve pull requests`.

OR


- Instead of useing `{{ `${{secrets.GITHUB_TOKEN}}` }}` in GitHub Actions use a GitHub [Personnal Acces Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token#creating-a-fine-grained-personal-access-token) like: `${{ `{{secrets.PAT}}` }}`.

## The Action

The current action is set to only generate the readme on a pull request.  You can modify this to your own needs.

<code src="hype.yml"></code>
