# Big repositories & LFS

## Authors
- Ekaterina Tolstoguzova
- Lukáš Beran
- Martin Konvičný

## Table of Contents

1. [Big repositories](Big_repositories.md)
- [Handling repositories with a very long history](Big_repositories.md#handling-repositories-with-a-very-long-history)
     * [Git shallow clone](Big_repositories.md#git-shallow-clone)
     * [Git filter branch](Big_repositories.md#git-filter-branch)
- [Handling repositories with huge binary assets](Big_repositories.md#handling-repositories-with-huge-binary-assets)
     * [Git sparse-checkout](Big_repositories.md#git-sparse-checkout)
     * [Submodules](Big_repositories.md#submodules)

2. [LFS](https://github.com/BeranLukas/Project-big-repositories-LFS/blob/main/GIT%20LFS.md)
- [What is GIT LFS](https://github.com/BeranLukas/Project-big-repositories-LFS/blob/main/GIT%20LFS.md#what-is-git-lfs)
- [Installation](https://github.com/BeranLukas/Project-big-repositories-LFS/blob/main/GIT%20LFS.md#instalation)
- [How to create a new Git LFS repository](https://github.com/BeranLukas/Project-big-repositories-LFS/blob/main/GIT%20LFS.md#how-to-create-a-new-git-lfs-repository)
- [How to clone a Git LFS repository](https://github.com/BeranLukas/Project-big-repositories-LFS/blob/main/GIT%20LFS.md#how-to-clone-a-git-lfs-repository)
- [How to pull up and check out](https://github.com/BeranLukas/Project-big-repositories-LFS/blob/main/GIT%20LFS.md#how-to-pull-up-and-check-oout)
- [Tracking files with Git LFS](https://github.com/BeranLukas/Project-big-repositories-LFS/blob/main/GIT%20LFS.md#tracking-files-with-git-lfs)
- [Committing and pushing](https://github.com/BeranLukas/Project-big-repositories-LFS/blob/main/GIT%20LFS.md#committing-and-pushing)
- [Moving a Git LFS repository between hosts](https://github.com/BeranLukas/Project-big-repositories-LFS/blob/main/GIT%20LFS.md#moving-a-git-lfs-repository-between-hosts)
- [Fetching extra Git LFS history](https://github.com/BeranLukas/Project-big-repositories-LFS/blob/main/GIT%20LFS.md#fetching-extra-git-lfs-history)
- [Deleting local Git LFS files](https://github.com/BeranLukas/Project-big-repositories-LFS/blob/main/GIT%20LFS.md#deleting-local-git-lfs-files)
- [Deleting remote Git LFS files from the server](https://github.com/BeranLukas/Project-big-repositories-LFS/blob/main/GIT%20LFS.md#deleting-remote-git-lfs-files-from-the-server)
- [Finding paths or commits that reference a Git LFS object](https://github.com/BeranLukas/Project-big-repositories-LFS/blob/main/GIT%20LFS.md#finding-paths-or-commits-that-reference-a-git-lfs-object)
- [Including/excluding Git LFS files](https://github.com/BeranLukas/Project-big-repositories-LFS/blob/main/GIT%20LFS.md#includingexcluding-git-lfs-files)
- [Locking Git LFS files](https://github.com/BeranLukas/Project-big-repositories-LFS/blob/main/GIT%20LFS.md#locking-git-lfs-files)
- [Practical example](https://github.com/BeranLukas/Project-big-repositories-LFS/blob/main/GIT%20LFS.md#practical-example)

## Sources

 [Mestering Git, Chapter 9](https://www.packtpub.com/product/mastering-git/9781783553754)

 [GitHub, Git-LFS](https://github.com/git-lfs/git-lfs/wiki)

 [Atlassian, Big repositories](https://www.atlassian.com/git/tutorials/big-repositories)

 [Atlassian, Git-LFS](https://www.atlassian.com/git/tutorials/git-lfs)

 [Bitbucket Support, Working with Git LFS files](https://confluence.atlassian.com/bitbucketserver/working-with-git-lfs-files-970595880.html)

 [Atlassian, Git submodules](https://www.atlassian.com/git/tutorials/git-submodule)
 
 [GitHub, Get up to speed with partial clone and shallow clone](https://github.blog/2020-12-21-get-up-to-speed-with-partial-clone-and-shallow-clone/)
 
 