# Overview
Useful Resources that I have found for development.

| Section                                              | Description                              |
| :--------------------------------------------------- | :--------------------------------------- |
| [Development Machine](#DevelopmentMachine) | Tips for setting-up a better development environment |
| [Processes](#Processes)                              | Resources for better ways of working     |
| [iOS](#iOS)                                          | iOS development specific resources       |

<a name="DevelopmentMachine"></a>
# Development Machine

## CLI
Taking the time to setup and customize the terminal can save a lot of time and make working in the terminal a lot more enjoyable. 

### zsh
I highly recommend moving to `zsh` instead of `bash`. The completions are much better and it is can be easily customized. This is a great getting started article: [You’re Missing Out on a Better Mac Terminal Experience](https://medium.com/@caulfieldOwen/youre-missing-out-on-a-better-mac-terminal-experience-d73647abf6d7)

### dotfiles
Setting up a dotfiles repository also makes moving between computers a lot more seemless. 
 - [Your unofficial guide to dotfiles on GitHub](https://dotfiles.github.io/)
 - [Getting Started with Dotfiles](https://medium.com/@webprolific/getting-started-with-dotfiles-43c3602fd789)
 - [The best way to store your dotfiles: A bare Git repository](https://www.atlassian.com/git/tutorials/dotfiles)
 
 
 ## Quick Look
 Using a mac, the default quick look isn't great. There are plugins that can make this a lot better, as detailed in [this repo](https://github.com/sindresorhus/quick-look-plugins).
 
 **TLDR**: run this command to have a better quick loook experience:
 ```shell
 brew cask install qlcolorcode qlstephen qlmarkdown quicklook-json qlimagesize suspicious-package quicklookase qlvideo
 ```
 
 <a name="Processes"></a>
 # Processes
 
 ## Versioning
 
[Semantic Versioning](https://semver.org/) is the best way to manage versions. It is widely used, understood, and makes version numbers meaningful by having them reflect real work done in the codebase. 

It is also possible to automatically generate them if a codebase standardizes on how commit messages are written via something like [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/). This allows both version numbers and a changelog to be automatically generated. See:
- [Mozilla: Auto-generating a changelog from git history](https://blog.mozilla.org/webdev/2016/07/15/auto-generating-a-changelog-from-git-history/)
- [How to generate Changelog using Conventional Commits](https://medium.com/jobtome-engineering/how-to-generate-changelog-using-conventional-commits-10be40f5826c)

Using Conventional Commits can also be enforced via a commit linter, such as [commitlint
](https://github.com/conventional-changelog/commitlint). This can run on both the build server and on [developers local machines via git hooks through Husky](https://commitlint.js.org/#/guides-local-setup). The changelog can then be generated with each new build via [conventional-changelog](https://github.com/conventional-changelog/conventional-changelog).

<a name="iOS"></a>
# iOS 
## Get Release size of Framework
1. Build framework in app by archiving the app targeting a device (in this case, I was testing [GRDB](https://github.com/groue/GRDB.swift)).
2. Open IPA and locate the framework file, copy it out.
3. Run:
```Shell
$ xcrun bitcode_strip -r GRDB.framework/GRDB -o GRDB.nobitcode
$ lipo -thin arm64 GRDB.nobitcode -o GRDB.arm64
```
Methodology copied from what Realm is doing. See:

https://github.com/realm/realm-cocoa/issues/2581

https://github.com/realm/realm-cocoa/issues/4785#issuecomment-289987511

## CLI
A few useful aliases to add to your `.bash_profile` or `.zshrc` (I find it useful to make a `.aliases` that they both import)

### Clear Derived Data

Xcode builds can occasionally screw up due to old build information laying around in derived data. A shortcut to clearing it is:
```bash
alias ddd="rm -rf ~/Library/Developer/Xcode/DerivedData"
```
### Kill Xcode
When switching between branches where the `.xcodeproj` file has changed a lot, xcode will occassionally throw up a lot of annoying dialogs asking if you want the one on disk or in memory, and you'll need to restart xcode anyways. This is easy command to call before switching between problemmatic branches (also useful to add to Automator).
```bash
alias killxcode="killall Xcode || true"
```
### Reset Pods Integration
Cocoapods can have a pretty complicated setup and occassionally things go wrong. If you think there is a pod state problem, it is often easier to deintegrate and reset up the Cocoapods. This will do everything in one line.
```bash
alias nukepods="killall Xcode || true; rm -rf ~/Library/Caches/CocoaPods; rm -rf Pods; rm -rf ~/Library/Developer/Xcode/DerivedData/*; pod deintegrate; pod setup; pod install;"
```
