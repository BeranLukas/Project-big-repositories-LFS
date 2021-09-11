# What is GIT LFS?

Initially, it is important to remind what GIT is. It is a fully distributed version control system. Thus, we transfer the complete history of the repository to our local storage during the cloning process. If we work on a project with frequently modified files of enormous size, this process may take considerable time as we download all versions of the files saved in the repository.

As a result, a git extension, GIT LFS (Large File Storage), was created by Atlassian and GIT developers and other open-source collaborators to reduce the amount of downloaded data. Thanks to this extension, large files are saved in a separate location from our repository. In our repository, these files are replaced with pointer files that lead to their location. They are located either in the local GIT LFS cache or some remote Git LFS store. The pointer files are managed automatically by GIT LFS, so we can not see them.

In order to work with GIT LFS, proper hosting (e.g., Bitbucket Cloud, etc.) is required. If we use the repository, we will need GIT LFS command-line client or some GUI client (e.g., Sourcetree).


# Instalation


#
