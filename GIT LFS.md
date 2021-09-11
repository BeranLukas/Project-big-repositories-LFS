# What is Git LFS?

Initially, it is important to remind what Git is. It is a fully distributed version control system. Thus, we transfer the complete history of the repository to our local storage during the cloning process. If we work on a project with frequently modified files of enormous size, this process may take considerable time as we download all versions of the files saved in the repository.

For instance, we would like to make a few changes to a binary image. The image takes up 50 MB of space. We make nine changes. Each version of the file is tracked. Therefore, 500 MB of the repository is used (the original file occupies 50 MB of the storage + 9 version takes up 450 MB). All versions of the image are also pushed to the remote. The large size of one file significantly decreases the speed at which we can operate with our repository.

As a result, a git extension, Git LFS (Large File Storage), was created by Atlassian and Git developers and other open-source collaborators to reduce the amount of downloaded data. Thanks to this extension, large files are saved in a separate location from our repository. In our repository, these files are replaced with pointer files that lead to their location. They are located either in the local Git LFS cache or some remote Git LFS store. The pointer files are managed automatically by GIT LFS, so we can not see them.

In order to work with Git LFS, proper hosting (e.g., Bitbucket Cloud, etc.) is required. If we use the repository, we will need Git LFS command-line client or some GUI client (e.g., Sourcetree).


# Installation

Firstly, we download the git extension. There are three ways how to do it.
1. Download it via a package manager (`brew install git-lfs` or `port install git-lfs`)
2. Download it from [the project website](https://git-lfs.github.com/).
3. Download a free Git GUI client that includes Git LFS, such as [Sourcetree](https://www.sourcetreeapp.com/).

Then, install the Git command line extension: `git lfs install`


# How to create a new Git LFS repository

In progress ...

# How to clone a Git LFS repository

If the Git LFS is installed, we can use the well-known command `git clone`. If the Git LFS is installed, we can use the well-known command. The cloning process goes as usual, but in the end, Git automatically checks out the main branch. If any Git LFS file is required to complete the process, it will be downloaded.

EXAMPLE!

There is also the command `git lfs clone`.