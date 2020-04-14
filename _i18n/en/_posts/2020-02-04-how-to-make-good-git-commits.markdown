---
layout: post
title:  "How to make good Git commits"
date:   2020-02-04 21:15:00
tags:   Git, Commit, GitHub, GitLab
image: paper-pencil.jpg
image-description: Open note pad with a pencil
image-author: Jan Kahánek
image-author-link: https://unsplash.com/@honza_kahanek?utm_medium=referral&amp;utm_campaign=photographer-credit&amp;utm_content=creditBadge
comments: true
---

Git is a very important tool to develop quality software and its use became a well known pattern in the industry. It has multiple features that make our life easier when writing code and one of these is the ability to create **commits**.

Git is an important **documentation** tool. The commit history of a project is a great place to see how the code and the software evolved over time. Having this information available is very useful in a lot of cases.

In this text you will get a better knowledge of this Git feature and learn good practices on how to use it.

## What is a commit

Git is a version control tool. That means that it is used to control how software projects change and evolve over time, a commit is the main tool for doing that.

A commit functions like a **snapshot** of the project, it shows how the project's code was at a certain point in time. Git has tools that allow you to check the state of the project when each commit was made. This brings some benefits like more confidence to make new changes in the project (since the changes can be easily reverted if something goes wrong) or making it easier to debug the code, since you can run the project as it were in different points in time to know exactly when the unwanted behavior started.

This shows how Git is an important tool for **documentation** in a software project. If you need to know when a feature was included in the project or when some external library was replaced for an in-house solution? The project's commit history is there to help you.

But in order to get these benefits, the project needs to have a good commit history. Here are some tips to make good commits that help the person who will need to maintain this code in the future (if this person is yourself).

## How to make a commit

There are two main steps for creating a commit: choosing which changes will be included in the commit, and creating the commit itself.


You can use the `git status` command to check which files were updated in the project since the last commit:

```
On branch my-branch-name
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   index.html
	modified:   index.css

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	images/my-image.png
```

Knowing which files were modified, you can run `git add` to stage a file so it will be included in the next commit. In this example, if you want to create a commit with the `index.html` and `index.css` files, it is possible to run `git add` so both files are staged:


```
git add index.html
git add index.css
```

If you want to stage all the files that were modified in the project for the next commit, you can do that by running `git add .`.

With `git status` you can also see which files are staged on the `changes to be committed` section:

```
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
  modified:   index.html
  modified:   index.css
  new file:   my-image.png

```

With the files staged, now we can run `git commit` to create the commit itself. This command will open a text editor with a file showing the commit changes on the following format:

```

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch translate-nerves-page
# Changes to be committed:
#       modified:   index.html
#       modified:   index.css
#       new file:   my-image.png
```

Here we must use the editor to write a commit message, using one blank line to separate the title and the body of the message:

```
Commit message title

Commit message body. This is an optional text where you can
explain with details that change being made in commit. Use
this space to explain what is changing and why the changes
are happenning.

Use a blank line before a new paragraph e wrap the lines to
about 72 characters.

 - Bullet points are okay

 - Typically hypens (-) or asterisks (*) are used for the
   bullets, preceeded by a single space with blank lines
   in between, but conventions may vary

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch translate-nerves-page
# Changes to be committed:
#       modified:   index.html
#       modified:   index.css
#       new file:   my-image.png
```

If you do not want to add a message body, it is possible to run the commit command with the `-m` flag passing the message title between quotes:

```
git commit -m "Commit message title"
```

## How much code should go in a commit

A good commit does one thing. This makes it easier to understand how the project evolved over time and to revert changes if something goes wrong.

For example, imagine that you need to implement a new feature in a project and you start writing the code for that. After some time, you realize that the code for this new feature needs to call a module on a different part of the system, but this module is very confusing and hard to understand. Since you are already working on that, you decide to make a quick refactoring in this module before returning to the new feature code.

With the code written, you start writing the automated tests. The process goes well, but you see that there is one disabled configuration on the testing library that, if enabled, would show better results for the test suite execution. So you go on and enable this configuration on the project.

Work done, time to commit.

In this case, it makes sense to create three different commits: one to change the test library configuration, one with the code refactoring, and a third one with the new feature (including tests). This may sound redundant, but it improves the project's commit history. Making different commits for different changes makes it easier to revert the changes in the future, if this is needed.

If, for example, the team decides that using this new test configuration does not add much value, or if a bug is caused by the refactoring, it is possible to revert the commit that does only that without having to revert the feature code.

It is very important that a commit makes one change. Be it altering one line of code or various different files. The main thing to remember is that the commit can be accessed and reverted in the future. Having this in mind when creating a commit will help you measure how much code is enough for one commit.

## Commit message

The commit message is a space to document what the commit does. Having a good message is very important for a good commit, because this makes it easier to understand what happened in the project at each point in time. The commit message is divided in two parts: title and body.

### Title

The commit message title is a succinct phrase that says **what** the commit does.  It must be succinct, descriptive and specific.

For instance, check these three commits:

```
623509 style buttons
f12144 bugfix
23c30c refactoring
```

Even though these messages describe what the commit does, they are too generic. Compare them with this example:

```
623509 Style login page buttons
f12144 Fix duplicate email delivery bug
23c30c Refactor UserAccount module
```

Using specific titles helps differentiate commits by the message title. If on a week of paying technical debts the team creates 10 different commits with refactors in various parts of the code, having 10 different commits with a message that only says `Refactoring` is going to make the commit history confusing and difficult to read. But if each refactor commit says which code was refactored on its message, this will make the commits more descriptive and the history easier to read.

Git does not impose a character limit on the commit message title, but it is a good practice to keep them at less than 50 characters. This makes the history easier to read and forces the author to stop and think on a succinct way to describe what the commit does. GitHub's UI knows about these conventions and shows a warning when we try to create a title with more than 50 characters.

![Image of a text input with the title "Commit message" and the message "Long commit subject message to show that GitHub will collapse it when it has more than 72 characters" and a warning text with the message "Pro tip! Great commit summaries contain fewer than 50 characters. Place extra information in the extended description"]({{site.baseurl}}/images/git-commits/long-commit-message.png)

Besides that, when showing commits whose title has more than 72 characters, GitHub's UI will collapse the title.

![Image of a commit on GitHub with the message "Long commit subject message to show that GitHub will collapse it when..."]({{site.baseurl}}/images/git-commits/collapsed-commit-message.png)

You can consider 50 characters as a soft limit for a commit title message and 72 characters as a hard limit. If it is hard to summarize everything the commit does with this number of characters, this may be a sign that the commit is making too many different changes. If that is the case it makes sense to split this into other smaller commits.

### Body

The commit may also have an extended description, or message body. This is the place to explain in further details what the commit does. The message body can be a long text so it makes sense to write it as a common text, you can use multiple paragraphs, add links to other services that will help understand the commit (like a task on an issue tracker, for example), or even use bullet points. The important thing here is to communicate well.

A very important point is that the message body should focus on explaining in detail **what** was made in the commit and **why** these changes happened. Communicating context about the changes will be a huge help for anyone who wants to navigate through the commit history.

It may seem like a good idea to use the message body to explain how the change was made but, in most cases, this information is already present on the commit's code (that can be accessed using `git diff`). Adding this information on the message body, besides being redundant, can make the text unnecessarily long and make it harder to find information in it that is not available anywhere else.

Even though we have the message body available, it is important to remember that a good message body does not remove the need of having a good message title. Some commands that show a project's history like `git log --oneline` and `git shortlog` only show the commit title, with the body being more specific for the cases where we want a more complete version of the history of when we want to look at a commit individually. A good message body is important, but it does not replace a good message title.

It is also worth mentioning that not every commit needs to have a long message, sometimes only the title is enough to explain what the commit does. For instance, a commit that fixes a typo on the contribution guide of a project can communicate the changes effectively only with the title, without needing an extended description.

```
a73197 Fix typo on contribution guide
```

The main goal here is to give context so when someone looks at the commit in the future they know **what** change and **why** the change happenned.

## Style

Here are some small tips on how to make good commits, but that can help keep a good history in a project.

#### Capitalize the title

Capitalizing the title is a good practice when writing and it also applies here.

#### Do not end the title with a period

This is also a good practice for writing. Titles do not need to end with a period, and this also applies for commit message titles.

#### Use a blank line to separate the message title and body

Adding this line break before the message body makes the message easier to read. Besides that, some tools like `git log`, `git shortlog` and `git rebase` may get confused if this line break is not there.

#### Limit the lines on the message to 72 characters

It is a good practice to limit the message body lines at 72 characters. This makes the message easier to read and decreases the chance of breaking the text formatting when it is shown on the command line or on some graphical UI.

#### Use the imperative mood on the title

This point is very important to make a more readable commit history, but it is easy to miss when writing a commit message.

When writing a commit message, it is easy to just say what _was_ done or what _is being done_, using the indicative mood:

  * `Fixed bug with Y`
  * `Changing behavior of X`
  * `Removed deprecated methods`
  * `Releasing version 1.0.0`

Writing this way may seem more natural, but it can make the history harder to read.

Always use the imperative mood when writing message titles:

  * `Refactor subsystem X for readability`
  * `Update getting started documentation`
  * `Remove deprecated methods`
  * `Release version 1.0.0`

This follows the standard that Git itself uses when creating commit messages automatically, as it does in some cases like `git merge`:

```
Merge branch 'myfeature'
```

Or in `git revert`:

```
Revert "Add the thing with the stuff"

This reverts commit cc87791524aedd593cff5a74532befe7ab69ce9d.
```

The tip for remembering this practice is that a good commit message must always be able to complete the sentence: `if applied, this commit will`. For example:

  * if applied, this commit will `refactor subsystem X for readability`
  * if applied, this commit will `update getting started documentation`
  * if applied, this commit will `remove deprecated methods`
  * if applied, this commit will `release version 1.0.0`

## Tests

Is it necessary to have all the test suite passing so a commit can be made?

I consider it important to have passing tests before creating a commit. Considering that a commit is a snapshot of the project that can be accessed in the future, having passing tests will make it easier to run the project in any commit that is in the past. Besides that, having broken tests can be a sign that the changes the commit wants to make are not complete.

## Practical tips

#### Configure which editor is used with Git

By default, Git uses the default text editor on the system (in most cases this is `vi`) to edit commit messages. You can use other text editors for that by altering the `core.editor` configuration. For instance, by running the following command:

```
git config --global core.editor atom
```

Git will now use Atom as the standard text editor to be used for commit messages and for some other cases like interactive rebases.

#### Edit last commit message

If you want to edit the last commit's message, you can do that by running `git commit --amend`. This will open your text editor showing the last commit and from there you can edit the message. If you just want to edit the commit message title you can do that by running:

```
git commit --amend -m "New commit message"
```

#### Add more files to the last commit

You can also do that by running `git commit --amend`.

Do the changes in the project that you want to add to the last commit, stage the changes with `git add` and then run `git commit --amend`. As I mentioned in the previous section, this will open your text editor and you can also use it to edit the commit message.

In case you just want to add more file changes to the commit without editing its message, you can do that by running `git commit --amend --no-edit`.

## Final tips

Even though making commits is a recurring task in writing software, creating good commits is not something trivial. Git is a very useful communication tool and communicating effectively is also not trivial. It is important to have this in mind when using Git.

Making good commits requires work, but it is beneficial. The person who will maintain the project in the future will be thankful for that, and this person can be yourself.

Here are some resources I used to write this text and that I recommend if you want to know more about Git:

  * [Pro Git book](https://git-scm.com/book/en/v2)
  * [Git field guide](https://afterhours.io/git-field-guide.html) by [Lucas Mazza](https://twitter.com/lucasmazza/)
  * [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/) by [Chris Beams](https://twitter.com/cbeams)

If you have any suggestions, questions of feedback about the text you can comment here or reach me on [Twitter](https://twitter.com/RuanBrandao). Thank you!

This text was originally published in my [personal blog](https://ruanbrandao.com.br/2020/02/04/como-fazer-um-bom-commit/).
