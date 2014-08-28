HOW TO DELETE FILES FROM GIT HISTORY
------------------------------------

* Run the following commands on local repository. This will entirely remove the development releases from history, index and working directory.
````bash
  $ git filter-branch --force --index-filter 'git rm --cached\
  > --ignore-unmatch releases/cpputest-3.7dev.zip'\
  > --prune-empty --tag-name-filter cat -- --all
  $ git filter-branch --force --index-filter 'git rm --cached\
  > --ignore-unmatch releases/cpputest-3.7dev.tar.gz'\
  > --prune-empty --tag-name-filter cat -- --all
````
* Push the changes to the upstream repository:
````bash
  $ git push -uf origin master
````
* Let Travis Github Deployer do its job. There should now be the current development release, and no development releases in history.

When anyone pulls changes, they should rebase. They should not merge, because this would re-introduce old commits when pushing, including (some of) the deleted files.

##### Note
Possibly the above commands could be part of a script run from Travis? If not, it would be okay to run them occasionally.
