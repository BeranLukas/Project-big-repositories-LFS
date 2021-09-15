# Handling repositories with a very long history
## Git shallow clone
Git shallow clone lets you pull down just the latest commits, not the entire repo history. So if your project has years of history, or history from thousands of commits, you can select a particular depth to pull. The command `git clone --depth=<N>` is used to reduce the commit history. 
Usually, the parameter `--depth=1` is used and means that we are only interested in the most recent commits.

You can also use git shallow clone to access a single branch:

`git clone [remote-url] --branch [name] --single-branch [folder]`

If you are working with long and diverging branches, this option will only allow you to load data for the commit you plan to use immediately.
## Git filter branch

# Handling repositories with huge binary assets

## Git sparse-checkout

## Submodules