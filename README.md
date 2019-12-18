# Overview
Useful Resources that I have found for development.

# Development Environments

## CLI
Taking the time to setup and customize the terminal can save a lot of time and make working in the terminal a lot more enjoyable. 

I highly recommend moving to `zsh` instead of `bash`. The completions are much better and it is can be easily customized. This is a great getting started article: [You’re Missing Out on a Better Mac Terminal Experience](https://medium.com/@caulfieldOwen/youre-missing-out-on-a-better-mac-terminal-experience-d73647abf6d7)

Setting up a dotfiles repository also makes moving between computers a lot more seemless. 
 - [Your unofficial guide to dotfiles on GitHub](https://dotfiles.github.io/)
 - [Getting Started with Dotfiles](https://medium.com/@webprolific/getting-started-with-dotfiles-43c3602fd789)
 - [The best way to store your dotfiles: A bare Git repository](https://www.atlassian.com/git/tutorials/dotfiles)
 
 # Processes
 
 ## Versioning
 
[Semantic Versioning](https://semver.org/) is the best way to manage versions. It is widely used, understood, and makes version numbers meaningful by having them reflect real work done in the codebase. 

It is also possible to automatically generate them if a codebase standardizes on how commit messages are written via something like [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/). This allows both version numbers and a changelog to be automatically generated. See:
- [Mozilla: Auto-generating a changelog from git history](https://blog.mozilla.org/webdev/2016/07/15/auto-generating-a-changelog-from-git-history/)
- [How to generate Changelog using Conventional Commits](https://medium.com/jobtome-engineering/how-to-generate-changelog-using-conventional-commits-10be40f5826c)

Using Conventional Commits can also be enforced via a commit linter, such as [commitlint
](https://github.com/conventional-changelog/commitlint). This can run on both the build server and on [developers local machines via git hooks through Husky](https://commitlint.js.org/#/guides-local-setup). The changelog can then be generated with each new build via [conventional-changelog](https://github.com/conventional-changelog/conventional-changelog).
