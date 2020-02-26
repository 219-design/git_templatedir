## How to Use

In your ~/.gitconfig (global git config in `$HOME`), you will want to add an
entry for "templatedir"

Your "templatedir" is a directory on disk that has a structure similar to:

```
/home/username/.git_template
└── hooks
    ├── check-authorship
    ├── pre-commit
    └── pre-push
```

Once you have an on-disk directory as shown, and a git global config field that
points to that directory, then your set of hooks will get automatically placed
into **every** local repository **every** time you `git clone` from then onward.

If there are already repositories on your computer that were cloned before you
set this up, then you can navigate to the root of each repository and run:

```
git init
git submodule foreach git init   # if the repository has a .gitmodules file.
```

**CAVEAT:** `git init` will ONLY CREATE NEW hooks in an existing repository
where no prior hook of that name existed. In other words, it will copy over
templatedir hooks only for those hooks that *won't collide* with a preexisting
hook of that name. Therefore, a "sure-fire" but dangerous way to make sure your
latest templatedir is copied over is to:

```
# rm .git/hooks/*   # only run this if you are sure about it
# ... then ...
git init
git submodule foreach git init
```
