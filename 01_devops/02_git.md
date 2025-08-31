# GIT

## Table of contents
1. [What is GIT](#question1)
2. [Benefits of using version control](#question2)
3. [Branching strategies](#question3)
4. [Git workflow](#question4)
5. [What is a commit](#question5)
6. [Resolving merge conflicts](#question6)
7. [Difference between git merge and git rebase](#question7)
8. [CMDS](#question8)
9. [Git LFS](#question9)
10. [Cherypick](#question10)

## 1. What is GIT <a name="question1"></a>

    Git is a free and open-source distributed version control system (VCS) designed to handle everything from small to very large projects with speed and efficiency. It was originally created by Linus Torvalds in 2005

    - Distributed:
        Unlike older centralized VCSs, every developer has a complete local copy of the entire repository history. This allows for offline work and faster local operations like commits, branching, and merging.
    - Version Control:
        Git tracks changes made to files over time, enabling developers to revert to previous versions, compare changes, and understand the history of a project.
    - Branching and Merging:
        Git excels at allowing developers to create independent lines of development (branches), work on features in isolation, and then seamlessly merge those changes back into the main project.
    - Performance:
        Git is known for its speed in handling common operations like committing, branching, and merging.
    - Collaboration:
        Git facilitates collaborative software development by providing tools and workflows for teams to share code, review changes (e.g., through pull requests), and resolve conflicts.

## 2. Benefits of using version control <a name="question2"></a>

    - Collaboration:
        Git facilitates seamless collaboration among multiple developers working on the same project. It allows team members to work on separate features or bug fixes simultaneously without overwriting each other's work, and provides robust mechanisms for merging changes.
    - Change Tracking and History:
        Git meticulously records every change made to the codebase, including who made the change, when it was made, and a descriptive commit message explaining the purpose of the change. This comprehensive history is invaluable for understanding project evolution, debugging issues, and auditing changes.
    - Branching and Merging:
        Git's powerful branching model enables developers to create isolated environments for experimenting with new features or fixes without affecting the main codebase. Once changes are stable, they can be easily merged back into the main branch.
    - Error Recovery and Rollbacks:
        The complete history maintained by Git acts as a safety net. If a bug is introduced or a change causes issues, it is easy to identify the problematic commit and revert to a previous, stable version of the code.
    - Backup and Disaster Recovery:
        Git repositories serve as a distributed backup of the project's history. Even if a local copy is lost, the project can be restored from a remote repository.
    - Improved Code Quality and Review:
        The ability to track changes and compare different versions facilitates code reviews, allowing team members to scrutinize changes, identify potential issues, and ensure code quality before integration.
    - Faster Development and Experimentation:
        The ease of creating branches and merging changes encourages experimentation and rapid iteration, leading to a more efficient development workflow.

## 3. Branching strategies <a name="question3"></a>

Branching in Git is a way to create separate lines of development within a project. A branch is like a pointer to a specific commit in the Git history.
By default, Git starts with a main branch (commonly called main or master). When you create a new branch, you’re making a copy of the project’s history at that point. This allows you to work on new features, bug fixes, or experiments without affecting the main codebase. 
- Each branch is independent, so changes don’t interfere with others until merged.
- Branches make parallel development possible (e.g., multiple developers working on different features).
- You can easily merge branches to combine work or delete branches after completion.

**Strategies:**
- **Release branching:**
    We can clone the develop branch to create a Release branch once it has enough functionality for a release. This branch kicks off the next release cycle; thus, no new features can be contributed beyond this point. The things that can be contributed are documentation generation, bug fixing, and other release-related tasks. The release is merged into the master and given a version number once it is ready to ship. It should also be merged into the development branch, which may have evolved since the initial release.
- **Feature branching:**
    This branching model maintains all modifications for a specific feature contained within a branch. The branch gets merged into master once the feature has been completely tested and approved by using tests that are automated.
- **Task branching:**
    In this branching model, every task is implemented in its respective branch. The task key is mentioned in the branch name. We need to simply look at the task key in the branch name to discover which code implements which task.

## 4. Git workflow <a name="question4"></a>

working directory, staging area/index, local repository, remote repository

## 5. What is a commit <a name="question5"></a>

The `git commit` command is a fundamental operation in Git, used to record changes to the local repository. It captures a snapshot of the project's currently staged changes and saves them to the repository's history

- Snapshot Creation:
    A commit creates a unique snapshot of the project's state at a specific point in time. This snapshot includes the content of all files that were staged for the commit.
- Commit Message:
    Each commit requires a descriptive message that explains the purpose and nature of the changes included in the commit. This message is crucial for understanding the project's history and for collaboration.
- Metadata:
    In addition to the commit message and file contents, a commit also stores metadata such as the author, timestamp, and a unique identifier (SHA-1 hash).
- Staging Area:
    Before a git commit can be executed, changes must first be added to the staging area using the git add command. This allows for selective inclusion of changes in a commit, ensuring only desired modifications are recorded.
- Local Repository:
    `git commit` saves the new commit object only to the local Git repository. To share these changes with others, they must be explicitly pushed to a remote repository using git push

## 6. Resolving merge conflicts <a name="question6"></a>

Resolving merge conflicts in Git involves a series of steps to integrate divergent changes from different branches into a single, coherent version.
1. Identify Conflicted Files:
    Use `git status `to see a list of files that require manual resolution. 
2. Locate and Understand Conflicts: 
    Git inserts special markers to delineate conflicting sections:
        <<<<<<< HEAD: Indicates the beginning of changes from the current branch (HEAD).
        =======: Separates the changes from the current branch and the incoming branch.
        >>>>>>> [branch-name]: Indicates the end of changes from the incoming branch. 
3. Resolve the Conflicts Manually:
    Crucially, remove all the conflict markers: (<<<<<<<, =======, >>>>>>>) after resolving each conflict. 
4. Mark as Resolved:
    After resolving the conflicts in a file and removing the markers, stage the resolved file using `git add <filename>`.
5. Commit the Resolution:
    `git commit -m "Resolved merge conflicts"`
6. Verify and Push (if applicable):
    `git push origin <branch_name>`

## 7. Difference between git merge and git rebase <a name="question7"></a>
1. `git merge`:
    git merge integrates changes by creating a new "merge commit" that combines the histories of both branches.
    - History:
        It preserves the entire, original history of both branches, including the point where they diverged. This results in a non-linear history with merge commits indicating where integrations occurred.
    - Destructive Nature:
        Non-destructive, as it does not alter existing commits.
    - Use Cases:
        Suitable for public branches or when maintaining a precise, auditable history is crucial, as it clearly shows when and where branches were integrated.
2. `git rebase`:
    git rebase integrates changes by rewriting the commit history. It moves the commits from one branch to the tip of another, effectively replaying them on top of the target branch.
    - History:
        It creates a linear history, making it appear as if the commits from the rebased branch were created directly on top of the target branch. This eliminates merge commits.
    - Destructive Nature:
        Destructive, as it rewrites commit history and generates new commit IDs for the replayed commits.
    - Use Cases:
        Primarily used on local, private branches to clean up commit history before merging into a shared branch, making the history more readable and concise. Caution: Never rebase public or shared branches, as it can cause significant issues for collaborators due to the rewritten history.

## 8. CMDS <a name="question8"></a>

```bash
git init
git clone <name>
git submodules --init
git submodules --update
git add *
git commit -m
git push origin <b_name>
git fetch
git reset HEAD~1
git rebase -i HEAD~3
```

## 9. Git LFS <a name="question9"></a>

Git Large File Storage (LFS) is an open-source Git extension designed to manage large binary files efficiently within Git repositories. Standard Git is optimized for text-based files, where it can track changes (diffs) effectively. However, with large binary files like images, videos, or datasets, any modification necessitates a complete replacement of the file in the repository, leading to repository bloat and slower Git operations (e.g., clone, fetch, pull). 
Git LFS addresses this by replacing large files in the Git repository with small, text-based pointer files. The actual content of these large files is stored separately on a remote LFS server (e.g., GitHub, GitLab, Bitbucket). When a user clones or checks out a repository, Git LFS automatically fetches the relevant large file content as needed, rather than downloading the entire history of the large file.

- Efficient handling of large files:
    Prevents repository bloat and improves performance for operations involving large binaries.
- Lazy downloading:
    Downloads large file content only when required during checkout, reducing initial clone times.
- Version control for binaries:
    Allows versioning of large files without storing their full history directly within the Git repository.
- Integration with existing Git workflows:
    Works seamlessly with standard Git commands once configured.

```bash
git lfs install
git lfs track
```

## 10. Cherypick <a name="question10"></a>

Git cherry-pick is a command used to apply the changes introduced by one or more specific commits from one branch onto another. Unlike merge or rebase, which typically integrate all commits from a source branch, cherry-pick allows for granular control, enabling the selection of individual commits.  
  
When you cherry-pick a commit, Git takes the changes introduced in that commit and creates a new commit with the same changes on your current working branch. This new commit will have a different SHA-1 hash than the original commit, even though its content is identical.  
  
```bash
git cherry-pick <commit-hash>
```
  
**Considerations:**  
While useful in specific scenarios, cherry-pick can lead to duplicate commits and a less linear history if overused. In many cases, traditional merge or rebase operations are preferred for integrating changes between branches. Cherry-pick should be reserved for situations where only specific, isolated changes need to be applied.
