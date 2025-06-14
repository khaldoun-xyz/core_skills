# Internal memo for new Khaldoun members

Welcome to the team!

Khaldoun wants to help its clients do more with less.
And we hope you'll help make that a reality.
Therefore, at first we want to help *you* do more with less.
We want you to be the surfer who uses a wave to move forward effortlessly.

## Our plan with Khaldoun

Khaldoun is an automation & data collection company for insurance companies.
[Our plan](/docs/plan.md) is usually outdated.
Still, it's a good guide to better understand our thinking.

## Systems that help us

We deliberately integrated certain behaviours
because they give us speed and focus
while maintaining independence and creativity.
We would like to ask you to adapt to our way.
Feel free to propose changes at any time.

Below is a list of the shared systems we currently use:

- [extensive documentation](#extensive-documentation)
- [asynchronous check-ins](#asynchronous-check-ins)
- [quarterly planning](#quarterly-planning)
- [a proper dev setup](#a-proper-dev-setup)

### Extensive documentation

We write a lot. We deal with many things asynchronously.
You might not be used to this yet. Still, we would like
to ask you to structure your thoughts and write them down.
We're always happy to have an open discussion - after we had a look at something.

### Asynchronous check-ins

Very often, meetings are a waste of time. Still, we want to stay
in touch with each other and understand the general direction we're taking.
Therefore, on Mondays we write up and share our plan for the week.
You're invited to comment on anyone's plans.

### Quarterly planning

As we grow, the need for alignment increases. To make sure we're on the
same page and generally understand our overall direction, we set quarterly
Objectives and Key Results (OKRs). Please influence our OKRs.

### A proper dev setup

If you're highly experienced you might already have come up with your own
tool stack that works just right for you. Congrats! Please stick to that.
However, you're most likely not overly experienced yet. So, please consider
using our proposed tool stack.
On Linux you can install it with one command:
[Altadim](https://github.com/khaldoun-xyz/altadim)

## Technology skills

Many people seem to believe that because of AI, the skill to develop scalable
software will lose its value. We don't believe that.
Twenty years ago, a technologist with deep knowledge of how to use the terminal
was much more productive than the rest. The same is true today.
AI will disproportionally benefit those with the proper foundations.

Below you can see a list of technologies that we use on a daily basis.
It is generally useful if you familiarise yourself with our tech stack.

- [Terminal](#terminal)
- [Git](#git)
- [Sql](#sql)
- [Python](#python)
- [Docker](#docker)
- [Github Actions](#github-actions)
- [Power Point](#power-point)
- [Plotting](#plotting)
- [Vim](#vim)

### Terminal

#### Highlighting

If you're on Linux and want to have helpful env/git information in your terminal,
add [this](https://github.com/khaldoun-xyz/core_skills/blob/main/setup/README.md#bashrc)
to your .bashrc file.

If you're on Windows, install
[WSL](https://learn.microsoft.com/en-us/windows/wsl/install)
to use a Linux environment on Windows.

##### On Mac

If you're on Mac, use this for the git branch section instead:

``` bash
# show git branch in Terminal
function parse_git_branch () {
  git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}
RED="%F{red}"
YELLOW="%F{yellow}"
GREEN="%F{green}"
BLUE="%F{blue}"
NO_COLOR="%f"
PS1="${GREEN}%n${NO_COLOR}:${BLUE}%~${YELLOW}\$(parse_git_branch)${NO_COLOR}%# "
```

#### Bash

Being able to interact with a terminal console is helpful
to not be limited by GUI functionality.

- `cd ~/<path_to_folder>`: Jump into a directory.
- `ls -a`: Show all (also hidden) files in directory.
  (Use `ls -a -ll` for a more structured/detailed list.)
- `ctrl + r (keyboard shortcut)`: Reverse i search to find historical bash commands.
- `htop`: See cpu usage (similar to windows task manager, quit with "q").

#### Psql

Psql is a terminal-based frontend to a Postgresql database.
To install psql on Linux, simply run
`sudo apt install postgresql -y`.
You'll figure it out for Mac or Windows.

The easiest way to set up a database connection
for psql is to open your .bashrc and add a
line like this:
`alias psql_NAME='psql CONNECTION_STRING_TO_POSTGRES_DATABASE'`.
Save and close your .bashrc, restart your terminal
and type in `psql_NAME`. Et voilà.

### Git

Version control is a very basic and very useful tool.

- [This video series](https://www.youtube.com/watch?v=rH3zE7VlIMs)
  gives you a good basic overview.
- To test your git knowledge, [clone this repo](https://github.com/juanfresia/git-challenge)
  and complete the challenges.

#### Git commands

Shown below is only a subset of git commands. You'll use those a lot.
Feel free to dive deeper into git.
Just remember you're still considered a solid English speaker
even if you don't know what 'transmogrify' means.

- `git init`: Initializes a new Git repository in the current directory.
  (To set up an existing repo locally, use `git clone <git_url>`.)
- `git remote add origin <git_url>`: Adds a remote repository
  called "origin" to the local repository.
- `git status`: Displays the status of the repository, including any changes or conflicts.
- `git log`: Displays a log of all commits made in the repository.
- `git branch`: Show all existing branches.
- `git checkout -b <branch_name>`: Create a new branch and switch to it.
- `git checkout <branch_name>`: Switches to a different branch.
  (If switching to another branch is impossible due to
  irrelevant changes, type in `git stash` first.)
- `git add <file>`: Mark a file as "part of the next commit".
  (`git add .` marks all files in the current directory & subdirectories)
- `git stash`: Save uncommitted stages into temporary storage & remove them locally.
  (Use `git stash pop` to load the stages from temporary storage.)
- `git commit -m "<message>"`: Commits changes with a meaningful commit message.
  (For longer commit messages just write `git commit`.)
- `git rebase master`: Load the most recent changes from master into your branch.
- `git rebase -i HEAD~<number_of_commits>`: interact with historical commits.
  Use this to squash minor/irrelevant commits by marking
  to-be-squashed commits with "s".
- `git push origin <branch_name>`: Pushes changes to remote repository origin.
- `git pull origin`: Fetches and merges changes from remote repository origin.
- `git reset --soft HEAD^`: revert the last commit
  and keep the changes in uncommited stage.
  (Use `git reset --hard HEAD^` to revert the last commit and delete all changes.)

#### Pre-commit hooks

We use [pre-commit hooks](https://github.com/khaldoun-xyz/lugha/blob/main/.github/workflows/deploy.yml)
to make sure our PRs fulfill minimum requirements
before other people have a look at them.
To install pre-commit hooks in your local repo,
simply go to the root of the repo and run `pre-commit install`.
As one example, have a look at [Lugha's pre-commit hooks](https://github.com/khaldoun-xyz/lugha/blob/main/.pre-commit-config.yaml).

#### Git good case practices

Below is a basic list of good case practices when using git.
Please refer to this list when you're unsure
how to ask your colleagues for a PR review.

- When pushing a PR, rebase to the master branch with `git rebase master`
  (make sure you have the most recent master locally!)
  and resolve any merge conflict *before* asking for review.
- When your PR isn't ready for review yet (work in progress)
  but you still want to share it with others, open the PR as `draft`.
- Squash minor git commits into fewer more relevant commits.
  Set "Squash and merge" as default merge option of branches
  (this collapses a branch with many commits into one feature commit in master).
- Where helpful, use gitmojis in your commit messages (e.g. :bug:): <https://gitmoji.dev/>.
- Don't open PRs without descriptions.
  Make sure to minimise typos and formatting issues.
- PRs that are too large cannot be merged (extreme case: 5000+ files are too large).
- Once you dealt with a PR comment,
  click on "Resolve conversation" to indicate that you consider it resolved.
  Either resolve all comments or provide responses.
- Close open issues with a reference to the PRs
  in which they are resolved after you've resolved them.
- use at least these pre-commit hooks: end-of-file-fixer,
  trailing-whitespace, black, isort.
  Always make sure pre-commit hooks have run *before* asking for a review.

### Sql

Creating and accessing data is as fundamental as it gets.

#### Thoughts on sql

- never never never write a query like this
  `select * from table Where column = 'text' ORDER by id desc`;
  instead write it like this:

``` sql
select * 
from table 
where column = 'text'
order by id desc
;
```

### Python

#### Thoughts on python

- use intention-revealing names:
  in most cases `df` or `data` are terrible names for dataframes;
  be precise and specific in your naming (also for variables, function names, etc.)
- when you want to use global variable names,
  define them in all caps after your import statements: `GLOBAL_VAR = 42`

#### Running tests

We write basic unit tests for our products using `pytest` ([link](https://docs.pytest.org/en/stable/)).
Tests are stored in a folder called `tests`, which is on the same level as the `src` folder.
To run your tests, simply run `pytest` in your repo.

### Docker

Containerising applications with Docker removes
many of the headaches around server configuration.
If the docker runs on one system, it will run on another.

- `docker build -t NAME .`:
  build a container & give it the name NAME
- `docker run NAME`: run the NAME container
  (not additional parameters like `-p`, `-d`, `--env-file`, etc.)
- `docker ps`: see a list of running docker containers
- `docker exec -it INITIAL_DIGITS_OF_CONTAINER sh`:
  jump inside a container & get terminal access

### Github Actions

For Continuous Delivery, we rely on Github Actions.
As one example, check [Lugha's deploy script](https://github.com/khaldoun-xyz/lugha/blob/main/.github/workflows/deploy.yml).
Whenever we merge anything into our `main` branch, the `main` branch
is automatically deployed on our Digital Ocean droplet.

### Power Point

When used properly, Microsoft Power Point is a useful tool for concept work
and to quickly visualise what you have in mind.

#### Thoughts on Power Point presentations

- never forget: the only reason to create a presentation is *to sell*
- if it is unclear what the presentation is for, make it clear or cancel the presentation
- before creating slides, write down the key messages of your presentation
  (no more than 3); if they aren't clear, make them clear or cancel the presentation
- for each slide, write down its key message;
  if the key message isn't clear, make it clear or remove the slide
- move everything that doesn't support the key messages into the backup,
  the last section of the presentation
- whatever the time frame of your presentation, plan ~1/3 for the actual presentation
  and ~2/3 for discussion

#### Power Point shortcuts

[This Youtube video](https://www.youtube.com/watch?v=-Ab-HYN0WUo) is a good primer
on the power of shortcuts in Power Point.

- `alt` = *the one key to rule them all:* show ribbon key bindings
- `ctrl + shift + ./,` = increase/decrease font size
- `ctrl + shift + g/h` = group/ungroup selection
- `ctrl + shift + c/v` = copy/paste formatting
- `ctrl + backspace` = delete entire word
- `ctrl + mouse wheel` = zoom
- `shift + arrow keys` = increase/decrease box size
- `ctrl + mouse movement` = duplicate box
- `ctrl + shift + mouse movement` = duplicate box & move it in straight line
- `ctrl + alt + m` = create new comment
- `F4` = repeat last command
- `alt` = activate & show quick travel keys

### Plotting

Great graphs help understand the underlying data. [This Youtube video](https://www.youtube.com/watch?v=hVimVzgtD6w&t=57s)
is very educational thanks to graphs.

#### Thoughts on great graphs

- good graphs provide easy-to-understand answers to simple qs;
  great graphs provide easy-to-understand answers to complex qs

### Vim

We don't mind if you don't want use Vim or Vim motions.
Still, you might enjoy the benefits of using it.  
Besides, it's part of [Khaldoun's installer script](/setup/README.md).
So why wouldn't you give it a try?

#### Vim motions

Vim motions allow you to quickly work with your code.

- [This video series](https://www.youtube.com/watch?v=X6AR2RMB5tE&list=PLm323Lc7iSW_wuxqmKx_xxNtJC_hJbQ7R)
  gives you a good basic overview.
- [This cheatsheet](https://vim.rtorr.com/) contains many useful commands.

Here is a list of basic vim motions.

- `h/j/k/l`: move the cursor left/down/up/right
- `yy/dd`: copy/cut a line
- `y5y/d5d`: copy/cut 5 lines
- `p`: paste the previously copied/cut lines
- `u/ctrl + r`: undo/repeat the previous command
- `w/b`: jump ahead/back one word
- `gg/G`: jump to top/bottom of file
