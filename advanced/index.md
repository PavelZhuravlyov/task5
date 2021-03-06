---
layout: curriculum
title: GitHub Advanced
byline: Mastering Git and GitHub
---

This curriculum will be your companion to the GitHub Advanced class taught by the GitHub Training Team and other educational groups. In this course, you'll explore strategies for branch and history rewriting, temporary storing and recovery techniques, and Git technology mechanics for faster problem solving.

{% capture slide %}
### Understanding Git
* Based on classic graph and hashing concepts
* SHA1 as the core hashing algorithm
* Linked-list-like data structure
* Built-in data integrity
{% endcapture %}
{% include slide-section %}

{% capture slide %}
#### Data structure
* Directed acyclic graph of commits
* Commit object
* Tree object
* Blob object
* SHA1 hash of commit, tree, blob
{% endcapture %}
{% include slide-section %}

{% capture svg_path %}../assets/diagrams/commit-data-structure.svg{% endcapture %}
{% include svg %}

* Linked list of commits
* First commit has `nil` parent
* Integrity checking with `git gc`

{% capture svg_path %}../assets/diagrams/commit-dag.svg{% endcapture %}
{% include svg %}

#### Treeish & commitish

* Simple ways of describing history points
* Easier-to-describe and understand numerically
* Application of patterns works on [GitHub](https://help.github.com/articles/comparing-commits-across-time)

```
HEAD
HEAD^^
HEAD~2
HEAD@{one.day.ago}
HEAD@{today}
```


{% capture slide %}
### Branching strategies
{% endcapture %}
{% include slide-section %}

#### Summary
* GitHub Flow
* Branch-per-feature
* Compatibility with Pull Requests
* git-flow
* Long-term release support

#### Details
These are called Branching Strategies, but are just as easily called *Team Collaboration Techniques* in an abstract discussion of version control.

* Branch by feature
* git-flow
    *  Made popular on Git by Vincent Driessen and his NVIE site
    * [Git-Flow: A Successful Branching Model](http://nvie.com/posts/a-successful-git-branching-model/)
    * [Git-Flow Source](https://github.com/nvie/gitflow)
    * Too many levels?
    * GH prefers Simplest thing that works.
* GitHub Flow
    * [How GitHub Develops](https://github.com/blog/919-how-github-develops)
    * [GitHub Flow blog post](http://scottchacon.com/2011/08/31/github-flow.html)
    * Works well with Pull Requests when one-layer deep
    * Think of features much smaller than typical
* Git's Model
    * [Git Maintenance Notes](https://sites.google.com/site/maintnotes/)
    * [Git Workflows](https://www.kernel.org/pub/software/scm/git/docs/gitworkflows.html)
    * [Git's Source Code](https://github.com/git/git)
    * Branches
        * master
        * maint
        * next (graduation from pu)
        * pu (can be rebased)
        * html
        * man
    * _"A trivial and safe enhancement goes directly on top of 'master'."_
    * _"The two branches "master" and "maint" are never rewound, and "next" usually will not be either"_
    * _"When a topic that was in 'pu' proves to be in testable shape, it graduates to 'next'."_
* Version numbers
    * `major.minor.fix`
    * [Semantic versioning](http://semver.org)
* Rebase before sharing (sending a Pull Request)
    * [Contributing to Spring Social](https://github.com/spring-projects/spring-social/wiki/Contributing)
    * [How To Merge Without Fear](http://blog.springsource.org/2010/12/21/git-and-social-coding-how-to-merge-without-fear/)
    * [What to do when things get complicated](http://blog.springsource.org/2011/07/18/social-coding-pull-requests-what-to-do-when-things-get-complicated/)


{% capture slide %}
### Applying branching patterns
{% endcapture %}
{% include slide-section %}

#### Summary
* Breaking features down into pieces
* Feedback early on Pull Requests
* @mentioning teams instead of individuals
* Continuous integration

#### Further reading
[Validated Build Promotions with Git, GitHub, and Jenkins](http://www.youtube.com/watch?v=Gd8OfAmKkMQ)

<iframe width="640" height="480" src="//www.youtube-nocookie.com/embed/Gd8OfAmKkMQ?rel=0" frameborder="0" allowfullscreen></iframe>

[Git and GitHub Workflows at the Utah JUG](https://speakerdeck.com/matthewmccullough/git-and-github-workflows-at-the-utah-jug)

<script async class="speakerdeck-embed" data-id="111dc3201094013231b066d414c0f9a8" data-ratio="1.77777777777778" src="//speakerdeck.com/assets/embed.js"></script>

{% capture slide %}
### Git-core GUIs
{% endcapture %}
{% include slide-section %}


#### Summary
* for staging, committing
* for browsing history
* Tcl/Tk based

#### Details
```
$ git gui
$ gitk
$ gitk&
$ gitk --all
```


{% capture slide %}
### Mastering Shortcuts
* Shortcuts to multiple steps
* Useful customized commands
{% endcapture %}
{% include slide-section %}


Add and commit along with the commit message:

```shell
$ git commit -a -m"[message]"
```

Commit, amend, and provide the commit message:

```shell
$ git commit --amend -m "[updated message]"
```

Checkout and create a branch:

```shell
$ git checkout -b [branch] [base]
```

{% capture slide %}
### Isolating Work

* Version patches of large change sets
* Stage interactively on command line
* Revise to-be-committed patch
{% endcapture %}
{% include slide-section %}



```bash
# Stage by patch
$ git add -p [file]

# Unstage by patch
git reset reset HEAD -p [file]
```


{% capture slide %}
### Branch best practices
{% endcapture %}
{% include slide-section %}

* Pros/cons of collapsing commits during merge
* Relation to branching strategies and deliverable expectations
* Checking merge state
* Cleaning up branches

```shell
$ git merge --squash [branch]
```

Querying commit existence:

```shell
$ git branch --contains [commit]
```

List branches with this merged in:

```shell
$ git branch --merged [commit]
```

List branches without this merged in:

```shell
$ git branch --no-merged [commit]
```

{% capture slide %}
### Ignoring content
{% endcapture %}
{% include slide-section %}

#### Repository-specific ignores
* Ignoring files from repo & system level
* Reviewing ignored files with custom command
* Forcing a staging of ignored files

```shell
$ vi .gitignore
```

#### System-wide ignores
```shell
$ git config core.excludesfile [path]
```

#### Listing ignored files
```shell
$ git config alias.show-ignored \
    "ls-files --exclude-standard
    --others --ignored"
```

#### Staging ignored files
```shell
$ git add -f [path]
```

#### Video
<iframe src="//player.vimeo.com/video/99804597" width="100%" height="350" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>


{% capture slide %}
### Navigating History
{% endcapture %}
{% include slide-section %}

```bash
$ git log --author [author-name]

$ git log --since [integer].days.ago

$ git log -S [string-in-patch]

$ git log -G [regex-pattern-in-patch]

$ git log --grep=[regex-in-message]

$ git log --diff-filter=[A|M|D]

$ git log --follow --stat --diff-filter=[A|M|D] -- <filename>

$ git log --oneline --left-right master..other

$ git log --oneline --left-right master...other

$ git name-rev [commit-ref]
```

* Log is like a search engine.
* Search for person, time, change, contents, message.
* Dramatically narrows human search time when using `log` search filters.

#### Further reading
* [Git revision specificat
ion syntax](https://www.kernel.org/pub/software/scm/git/docs/gitrevisions.html)

#### Video
<iframe src="//player.vimeo.com/video/95811891" width="100%" height="350" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>


{% capture slide %}
### Temporary Changes

* Name your stash
* List stashes
* Use specific stashes
{% endcapture %}
{% include slide-section %}


```shell
$ git stash
$ git stash save "<description>"
$ git stash --include-untracked
$ git stash list
$ git stash pop <name>
$ git stash drop <name>
$ git stash apply
$ git stash clear
$ git stash -p
```

{% capture slide %}
### Incorporating History
{% endcapture %}
{% include slide-section %}


* Reusing small pieces of code with `cherry-pick`
* Why use `cherry-pick` instead of `merge`?
* What happens when you `cherry-pick`?
* Maintaining `author` and `committer` fields
* Tracing any cherry-picks with `-x` commit message metadata
* `-x` metadata hyperlinked on GitHub
* `$ git cherry` to view absent commits
* Can include cherry-pick during rebase interactive

```shell
# Generate new commit on current branch
# with patch of specified commit

$ git cherry-pick [commit]
```

#### Identifying incorporated commits
```shell
# List branches containing same patch

$ git cherry [comparison-branch]
```

#### More examples
```shell
$ git cherry-pick [ref]
$ git cherry-pick [ref1] [ref2]

$ git branch --contains [noncherrypickedref]
$ git cherry [upstreambranch]

+ bd650366fa8c39f03cfc9dd5290f60e7331a631d
+ ea62f9f6a7cef55a8a3028e617d28819408a63c4
+ 874628c0e405390130d6457776273451bb66d3a8
+ 046a9b8d0f2363361e45cfbc7e0f6d82968f2f9f
+ 315fe16408f9a9080527e00df3d9a8c1ba0dc97a
```

{% capture slide %}
### Rewriting history with rebase
{% endcapture %}
{% include slide-section %}

{% capture svg_path %}../assets/diagrams/rebase.svg{% endcapture %}
{% include svg %}

#### What is rebase?
* Branch Preparation
* Rebasing __is not__ merging
* Conflicts can occur
* Resolution is simple
* Small variation to merge conflict

#### Rebasing a branch
Re-playing branch-specific commits against a base is the most common use case for rebase.

```shell
$ git checkout <featurebranch>
$ git rebase master
```

#### Rebase configuration
The behavior of `pull` can be configured to replay all local commits ahead of the incoming upstream ones.

```shell
$ git config pull.rebase true
```

#### Handling conflicts
Resolving a conflict during a rebase requires intervention, and then signaling that the conflict is resolved.

```shell
$ git add [conflicting-file]
$ git rebase --continue
```

#### Reordering History

* Reorder commits
* Rewrite history entirely
* Discard commits
* Revise/edit commits
* Safe patterns for rebasing local history
* Verbs (cheat sheet of commands)

```bash
$ git rebase -i <REF>
```

#### Reordering all commits on a branch

```bash
$ git rebase -i [remote]/[branch]
```

#### Rebase markers
Automatically arrange commits and rebase with `fixup!` and `squash!` message prefixes

```bash
$ git rebase -i --autosquash [ref]
```


#### Fixing Branches
* This mode of rebase change where branch history begins
* Moving blocks of history around

To change which base a branch is placed upon:

```bash
$ git rebase --onto <newbase> <upstream> <HEAD|branch>
```

#### Further reading
* [Rebasing chapter of Pro Git book](http://git-scm.com/book/ch3-6.html)
* [Git rebase --onto section of Pro Git book](http://git-scm.com/book/ch3-6.html#More-Interesting-Rebases)



{% capture slide %}
### Cutting Releases
{% endcapture %}
{% include slide-section %}

#### Summary
* Why create a tag through the web UI?
* Not a branch HEAD. Points to a specific commit.
* Attaching binaries to releases (Web UI and API)
* Tag with message (defaults to annotated)
* Force existing tag to new ref
* Delete a tag
* `$ git describe` to name the most recent reachable tag
* Tag types (reference, annotated, signed)
* Deleting a tag locally
* Deleting tag on a remote

{% capture svg_path %}../assets/diagrams/tag.svg{% endcapture %}
{% include svg %}

#### Reference tags
```shell
$ git tag [TAGNAME] [commit]
```

#### Annotated tags
```shell
$ git tag -a [TAG_NAME] [commit|branch]
$ git tag -a -m [TAG_NAME] [commit|branch]
```

#### Other tag options
```shell
$ git tag -s -m[message] [TAGNAME]
$ git tag -f [TAGNAME]
$ git tag -d [TAGNAME]
$ git describe
$ git describe [SHA]
$ git tag -d 12345
$ git push origin :[tag-name-to-delete]
```

{% capture slide %}
### Reviewing & synchronizing
{% endcapture %}
{% include slide-section %}


#### Reviewing remote branches
* PRs to horizontal contributors
* PRs multiple levels up
* Converting issues to PRs
* PRs as Issues with code
* Automatic closing of PRs by local merges
* Merges must be _made by recursive_
* Retrieving PRs locally to resolve conflicts
(without locally merging to target branch)

```shell
$ git ls-remote origin
$ git fetch origin refs/pull/1/head

$ git show FETCH_HEAD
$ git merge --no-commit --no-ff FETCH_HEAD
```

#### Examining remote branches
```shell
$ git remote -v
$ git remote show <remote-name>
$ git ls-remote
$ git branch -vv
```

#### Retrieving arbitrary commits
To merely retrieve the commits to `FETCH_HEAD`:

```shell
$ git fetch [remote] [pull-request-namespace]
```

To merge the retrieved commits into a branch:

```shell
$ git pull [remote] [pull-request-namespace]
```

#### Leveraging FETCH_HEAD
```shell
$ git fetch <URL> <branch>
$ git checkout FETCH_HEAD
$ git branch <newbranchname> FETCH_HEAD
```

#### Maintaining, customizing remotes
* Remove non-matching _local_ remote branches
* Remove non-matching remote upstream branches
* Remove only remote upstream branch

```shell
# Discard remote local branches
# not present on upstream
$ git fetch --prune

# Delete an upstream branch
$ git push origin :<branch-name>
```

#### Customizing Interaction
* Specification for retrieval and pushing
* Implied on fetch, pull, and push
* Altered by option switches like `--tags`
* Stored in `.git/config`
* Ability to retrieve Pull Request branches

```shell
$ git fetch [repo-url] [source]:[destination]
$ git config --add remote.[upstream].fetch "+refs/pull/*/head:refs/remotes/[upstream]/pull/*"
```


{% capture slide %}
### Aggregating repositories
{% endcapture %}
{% include slide-section %}

#### Adding submodules
Add a separate repository as a subdirectory:

```
$ git submodule add [repo-url] [folder]
```

#### Using submodules
For a freshly cloned repository with submodules

```
$ git submodule init
$ git submodule update
```

or

```
$ git submodule update --init --recursive
```

#### Dependencies with subtree

* Alternative to submodule
* All files available advantage

First a remote connecting to the dependency and a branch in which to read from is needed.

```shell
$ git remote add
    [dependency-bookmark]
    [repository-url]

$ git fetch [dependency-bookmark]

$ git branch [branch]
    [dependency-bookmark]/[branch]
```

* Notice the working tree content differs between the dependency and the main project.
* Establishing the association of a subdirectory and the branch is necessary when creating the association.
* Whenever the branch needs updating, switch to it, retrieve the changes and commit them against the main project branch(es).

```shell
$ git read-tree
  --prefix=[directory]/
    -u [branch]
```

```shell
$ git merge --squash
  -s subtree [branch]
```


{% capture slide %}
### GitHub CLI
{% endcapture %}
{% include slide-section %}

* Uses the API for interfacing with your repos
* Stores OAUTH token, credentials
* Highly efficient for power-users
* Hub and GH merging into one project

```shell
# Create a new public repository on your GitHub account
$ gh create

# Create a new private repository on your GitHub account
$ gh create -p

# Open a Pull Request for the current branch
$ gh pull-request

# Create a fork of the cloned repository on your GitHub Account
$ gh fork

# Launch a web browser with the branch comparison view
$ gh compare

# Launch a web browser to the repository home page
$ gh browse
```



{% capture slide %}
### Signing work
{% endcapture %}
{% include slide-section %}

#### By commit message
Adds a rigorously formatted text block to commit messages:

#### Configuring GPG
```shell
$ gpg --list-keys
pub   1024D/627CBB21 2014-08-01
uid                  Matthew McCullough

# Use 627CBB21 as the signing key's ID
$ git config --global user.signingkey [ID]
```


#### Using GPG signatures on commits
```shell
$ git commit --signoff
# or the shorthand invocation...
$ git commit -S

$ git log --show-signature
```

#### Using GPG signatures on tags
```shell
$ git merge --verify-signatures
```

```shell
$ git tag -s [tag-name] [commit]

$ git tag -v [tag-name]
```



{% capture slide %}
### Cleaning up history
{% endcapture %}
{% include slide-section %}

```shell
$ git filter-branch
    --subdirectory-filter [dir]
    -- --all
```

```shell
$ git filter-branch --index-filter
    'git rm --cached
    --ignore-unmatch [file]' HEAD
```



{% capture slide %}
### Avoiding Repetitive Conflicts
{% endcapture %}
{% include slide-section %}

* *Re*use *re*corded *re*solution
* Preserves pre-image to simplify conflicts

```shell
$ git config rerere.enable true
```

### The GitHub API

```shell
# Anonymous
$ curl <URL>

# Pass credentials on CLI
$ curl -u <user:password> <URL>

# Use .netrc file
$ curl -n <URL>
```


{% capture slide %}
### Cleaning
{% endcapture %}
{% include slide-section %}

#### Summary
* Purge untracked in working dir
* for directories
* for removing ignored files (useful for tidying build artifacts)

#### Details
```
$ git clean -f
$ git clean -fd
$ git clean -fx
```


{% capture slide %}
### Diff & merge tool
{% endcapture %}
{% include slide-section %}

#### Summary
* [P4Merge](http://www.perforce.com/downloads/Perforce/20-User)
* Opendiff
* KDiff
* Kaleidoscope
* Vimdiff
* Meld

#### Details
Difftool execution:

```
$ git difftool --tool-help
$ git config diff.tool <tool-name-in-config>
$ git config difftool.prompt false
$ git config difftool.<tool-name>.cmd "<path [args]>"
```

A sample `.gitconfig` file:

```
[diff]
    tool = p4merge
[difftool "p4merge"]
    cmd = "/Applications/p4merge.app/Contents/Resources/launchp4merge $LOCAL $REMOTE"
[difftool]
    prompt = false
```


Mergetool execution:

```
$ git config --global merge.tool p4mergetool

$ git config --global mergetool.p4mergetool.cmd "/Applications/p4merge.app/Contents/Resources/launchp4merge \$PWD/\$BASE \$PWD/\$REMOTE \$PWD/\$LOCAL \$PWD/\$MERGED"

$ git config --global mergetool.p4mergetool.trustExitCode false

$ git config --global mergetool.keepBackup false
```

A sample `.gitconfig` file:

```
[merge]
    tool = Kaleidoscope
[mergetool "p4mergetool"]
    cmd = " /Applications/p4merge.app/Contents/Resources/launchp4merge $PWD/$BASE $PWD/$REMOTE $PWD/$LOCAL $PWD/$MERGED"
    keepBackup = false
```


{% capture slide %}
### Refspecs
{% endcapture %}
{% include slide-section %}

{% capture slide %}
#### What are refspecs?
* Specification for retrieval and pushing
* Implied on fetch, pull, and push
* Altered by option switches like `--tags`
* Stored in `.git/config`
* Ability to retrieve Pull Request branches
{% endcapture %}
{% include slide-section %}

{% capture slide %}
#### Refspec examples

```
# Source and destination refspecs
$ git fetch [repo-url] [source]:[destination]

$ git fetch [repo-url] master
 * branch     master     -> FETCH_HEAD

$ git fetch origin refs/pull/1/head
 * branch     refs/pull/1/head -> FETCH_HEAD
```
{% endcapture %}
{% include slide-section %}

{% capture slide %}
#### Refspec to retrieve pull requests

```
$ git config --add remote.[upstream].fetch "+refs/pull/*/head:refs/remotes/[upstream]/pull/*"
```
{% endcapture %}
{% include slide-section %}


{% capture slide %}
#### Git Refspec Documentation
* [Git `rev-parse` command and reference specifications](https://www.kernel.org/pub/software/scm/git/docs/git-rev-parse.html)
* [ProGit book chapter on refspecs](http://git-scm.com/book/en/Git-Internals-The-Refspec)
{% endcapture %}
{% include slide-section %}



{% capture slide %}
### Additional Resources
This course covers many advanced uses of Git and GitHub, and yet there is still more to explore. We've included some of the most useful resources for our students with insatiable appetites.
{% endcapture %}
{% include slide-section %}

{% capture slide %}
#### Advanced Git Videos
* [Advanced Git, presented at JavaZone](http://vimeo.com/49444883)
* [Mastering Advanced Git, O'Reilly video series](http://bit.ly/ogitvid2)
* [The Fringes of Git, Git internals video](http://www.youtube.com/watch?v=qh-R0-7Ii_U)
{% endcapture %}
{% include slide-section %}

{% capture slide %}
#### Tools
* [`gh`, GitHub command line utility](https://github.com/jingweno/gh)
* [oh-my-zsh, ZSH plugin framework](https://github.com/robbyrussell/oh-my-zsh)
{% endcapture %}
{% include slide-section %}

{% capture slide %}
#### Git Documentation
* [Git `man` page command documentation](https://www.kernel.org/pub/software/scm/git/docs/git.html)
{% endcapture %}
{% include slide-section %}
