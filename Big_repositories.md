# Handling repositories with a very long history
## Git shallow clone
Git shallow clone lets you pull down just the latest commits, not the entire repo history. So if your project has years of history, or history from thousands of commits, you can select a particular depth to pull. The command `git clone --depth=<N>` is used to reduce the commit history. 
Usually, the parameter `--depth=1` is used and means that we are only interested in the most recent commits.

You can also use git shallow clone to access a single branch:

`git clone [remote-url] --branch [name] --single-branch [folder]`

If you are working with long and diverging branches, this option will only allow you to load data for the commit you plan to use immediately.
## Git filter branch
A second solution when managing repositories with large histories containing a lot of binary garbage might be the git filter branch.
 With the help of specially configured filters, this command allows you to reduce history.

The parameter `--tree-filter <command> ` is the filter for rewriting the tree and its contents. It checks out each commit into a temporary directory, runs your filter command, and builds a new commit from whatever is now in the temporary directory.

For example, if you want to remove a file (containing confidential information or copyright infringement) from all commits, then the syntax would be as follows:

`git filter-branch --tree-filter 'rm filename' HEAD`

However, the main disadvantage of this method is that when the history is overwritten, all commit ids change.
This requires every developer to re-clone the updated repository.


# Handling repositories with huge binary assets

## Git sparse-checkout

## Submodules