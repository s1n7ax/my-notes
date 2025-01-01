- Head

  - Head is a pointer to the current commit

- Featch

  - When fetching, git creates a new branch called 'remotes/\<remote\>/\<branch\>'
    and gets the changes from the remote branch

- Fast forward merge

  - When there is a clean commit history without any conflicts, it's a fast
    forward merge

- Submodules
  - Sub modules only tracks the remote repository and the head pointer
  - When the head pointer changes, the root repository will show that the
    sub module has been changed
  - Git will never change a sub module for you
