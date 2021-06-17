# Git Submodules {#git-update-submodule .task}

How to update a submodule

Submodules allow you to treat the two projects as separate yet still be able to use one from within the other. When dependencies are managed in submodules \(full, independant, repos in their own right\), occasionally you'll need to update the submodule \(NB: the submodule is pegged to a specific commit - **it does not follow HEAD**\).

**Note:** [Sourcetree](https://www.sourcetreeapp.com/) allows you to update all child submodules of a repo at the same time: **Actions** \> **Options** \> **Git** \> **\[x\]Perform submodule updates recursively**

Once the submodule parent repo has been updated/pushed to the remote, the steps below are for updating the hosted submodule:

1.  In Sourcetree: from the host repo, double click the submodule from the submodule panel on the left

2.  Pull any new updates to the submodule

3.  Return to host repo and commit the submodule update


If you have the submodule parent repo open on the same branch as the submodule you may get an error \(Sourcetree may complain that proceeding will delete local files\). If you changed files and wish to keep these changes, save them elsewhere. Checkout a different branch on the submodule parent repo and pull updates from the host repo again


