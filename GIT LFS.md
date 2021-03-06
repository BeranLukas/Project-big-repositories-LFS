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


# How to clone a Git LFS repository

If the Git LFS is installed, we can use the well-known command `git clone`. The cloning process goes as usual, but in the end, Git automatically checks out the main branch. If any LFS file is required to complete the process, it will be downloaded. For instance, to upload a very large file, we could use commands as follows:

        git clone git@gitlab.example.com:group/repository.git
        git lfs install                       # the Git LFS repository is initialized

There is also the command `git lfs clone`. It delivers much better performance for a large number of LFS files. In this case, Git waits until the whole process is over. Followingly, all required files are download altogether at one point in time. This approach significantly reduces the number of HTTP requests.


# How to pull up and check out

The same way as we used the cloning, we can also use the pull from Git LFS repository, using the `git pull` command (there is no need to use any explicit command to retrieve Git LFS files). It will download all of the needed Git LFS files as a part of the automatic checkout process when the pull completes. In case of the failure of the checkout, missing Git LFS content can be downloaded by `git lfs pull`.

# Tracking files with Git LFS

If you want to start tracking a specific binary file (or you want to add another), you need to use the `git lfs track` command with the specification of the type of the files that you want to track. For example, `git lfs track "*.jpg"` will associate all of the jpg files. Be sure to include the `" "` in your code, as without the quotation marks it will create individual entry for each of the *.jpg* file in your directory. The information about associated files will be added to a `.gitattributes` file and its behaviour is the same as is for `.gitignore`, with the exepction of negative patterns, which Git LFS does not support. All of the patterns currently tracked can be displayed by the `git lfs track` command without any arguments.

If you want to associate just some of the specific files in the directory, for example, only *.jpg* files in the *project* directory, you can use the following command: `git lfs track "project/*.jpg"`

To stop tracking a specific pattern with Git LFS, use the `git lfs untrack` command. For example, to stop tracking the *.jpg* files, use `git lfs untrack "*.jpg"`.

# Committing and pushing

As usual, all of the changes have to be commited. Commiting Git LFS files follows the same procedure as normal. If there are commited changes to the files tracked by Git LFS, there is some additional output from *git push* as the files are uploaded to the server. As Git, Git LFS is content addressable, in other words, it is stored against a SHA-256 hash. It is, therefore, safe to re-attempt transferring Git LFS files to the server in case it, for some reason, fails.

# Moving a Git LFS repository between hosts

Migrating Git LFS repositories from one host to another, it is possible to use the `gift lfs fetch` and `git lfs push` commands with the specification of the *--all* option .

Example of changing the provider for Git LFS repositories from *GitLab* to *GitHub*:
 - `git lfs fetch --all gitlab`
 - `git push -- mirror github`
 - `git lfs push --all github`

# Fetching extra Git LFS history

Command `git lfs fetch --recent` downloads extra content, other than the files needed for commits that you already checkout locally, for other modified branches. This is especially helpful if you are going to be out of the internet connection. Without any configuration, branch or tag containing a commit that is newer than seven days is cosidered as recent. Change of the recent days can be done by setting the property `lfs.fetchrecentrefsdays`. For example, if you want the history of the last 14 days, command `git config lfs.fetchrecentrefdays 14` will do exactly that.

Also content for the commit at the tip of a recent branch or a tag will be downloaded, unless you specify the `lfs.fetchrecentcommitsdays` property. Use `git config lfs.fetchrecentcommitsdays 2` to fetch the commits newer than two days. It can be very useful but be cautious with using it as it can result in a massive amount of data being downloaded.

# Deleting local Git LFS files

To locally delete LFS files, we can use a command `git lfs prune`. Thanks to this command, any local files that do not meet at least one of the following conditions will be deleted:
- the currently checked out commit
- a commit that has not yet been pushed from the local Git LFS cache 
- a recent commit (= created in the last ten days)

We can modify the command to retain the content for an extended period (e.g., 14 days).

        git config lfs.pruneoffsetdays 14

Old files are not deleted automatically. Therefore, it is recommended to regularly prune GIT LFS content in order to reduce the size of the local repository.

We can further modify the command to check whether a copy of your Git LFS objects is remotely saved before they are deleted. This option makes the whole process significantly slower, but if the deleted Git LFS objects are on the remote server, they are recoverable whenever we want.

        git lfs prune --verify-remote

# Deleting remote Git LFS files from the server

We cannot delete LFS files from the server using the command `git lfs prune`. There is no general way how to do it. We have to follow the instructions of our hosting provider.

# Finding paths or commits that reference a Git LFS object

If you have a Git LFS SHA-256 identifier, you can find which commits reference it by the `git log --all -p - S` command. It will show you the exact commit and the path to the Git LFS object, together with the information of who added it and the time of the commit. 

If you think that the Git LFS object is on any particular branch, you can use the `git grep` command to find the file path that reference it.

# Including/excluding Git LFS files

Sometimes you may want to download just a subset of the available Git LFS content for a particular commit. To exclude a pattern or subdirectory, the `git lfs fetch -X` can be used. On the other hand, if you want to include just a particular content or subdirectory, the `git lfs fetch -I` can be used. These commands can be combined to include and at the same time exlude particular patterns.

# Locking Git LFS files

To be able to lock Git LFS files, you need to include `--lockable` flag in the tracking command and specify which Git LFS file you want to lock. For example, to be able to lock the *jpg* files, command `git lfs track "*.jpg" --lockable` will do such a thing. After you commimt and push it, it will be added to *.gitattributes* and registered as lockable. The advantage of the opportunity to lock the file is the possibility to stop other users to edit the file while you are working on it.

When you are ready to make changes to Git LFS file, you can use the `git lfs lock` command to lock it. After you make changes, `git lfs unlock` command will make the file as unlocked. `git lfs locks` command allows you to see all locked files.

# Practical example

As a practical example, we will upload a logo of the Faculty of Social Sciences as a .jpg file and treat it like a git LFS file. To try some manipulation, we will lock the file. We assume that the Git LFS extension is already downloaded.

Firstly, we run:

        git lfs install

Secondly, we start tracking .jpg files as Git LFS files.

        git lfs track "*.jpg"

Thirdly, we will add, commit and push the file on GitHub.

        git add .
        git commit -m "tracking jpg files as Git LFS"
        git push

In another step, we will lock the file with the following command:

        git lfs track "*.jpg" --lockable

Add, commit and push to the GitHub

        git add .
        git commit -m "Locking Git LFS file Logo_IES"
        git push

We have illustrated easy way how to treat big files as Git LFS files and also an example of one of the features mentioned above, namely locking Git LFS files.
