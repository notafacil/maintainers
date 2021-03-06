# CONTRIBUTING to Zend Framework Repositories

This documentation outlines the general procedure for contributing to the
various Zend Framework components and repositories.

## RESOURCES

If you wish to contribute to this project, please be sure to
read/subscribe to the following resources:

 - [Coding Standards](https://github.com/zendframework/zend-coding-standard)
 - [Forums](https://discourse.zendframework.com/c/contributors)
 - [Slack](https://zendframework-slack.herokuapp.com)
 - [Code of Conduct](CODE_OF_CONDUCT.md)

If you are working on new features or refactoring
[create a proposal](https://github.com/{org}/{repo}/issues/new).


## Filing Issue Reports

Before you file an issue report, we ask that you ensure that what you have is indeed a bug, by
doing a little due-diligence:

- See if your use case is covered in the manual.
- See if your use case is demonstrated by the API docs.
- Ask the mailing list about your particular use case.
- Discuss your issue with someone in one of the IRC channels: `#zftalk` (general help) or
  `#zftalk.dev` (contributors) on [Freenode IRC](http://freenode.net).
- Write a failing test case.

None of these are required steps. However, failure to do any of them can and likely will result in
closing of your issue, due to an inability to reproduce and/or understand the problem. The best
possible outcome is to provide the minimal amount of code required to reproduce the issue, along
with details of what you expect to happen, and what you observe. These can easily be translated to
unit tests, which will allow us to both diagnose and resolve your issue sooner.

One you have all the necessary details ready, submit to the issue tracker for the appropriate
component; if you have written a failing unit test, you can send a pull request with just the
failing unit test instead. See the [component list](#component-list) below for links.

Be aware that acceptable resolutions might include:

- the documented behavior is incorrect (in such cases, we will correct the documentation).
- the observed behavior is _expected_.

## Reporting Potential Security Issues

If you have encountered a potential security vulnerability, please **DO NOT** report it on the public
issue trackers: send it to us at [zf-security@zend.com](mailto:zf-security@zend.com) instead.
We will work with you to verify the vulnerability and patch it as soon as possible.

When reporting issues, please provide the following information:

- Component(s) affected.
- A description indicating how to reproduce the issue.
- A summary of the security vulnerability and impact.

We request that you contact us via the email address above and give the project contributors a
chance to resolve the vulnerability and issue a new release prior to any public exposure; this helps
protect users and provides them with a chance to upgrade and/or update in order to protect their
applications.

For sensitive email communications, please use [our PGP key](http://framework.zend.com/zf-security-pgp-key.asc).

## Contributing Bugfixes or Features

By and large, this framework is built and maintained by the community. This means that process for
submitting something back, be it a patch, some documentation, or new feature requires some level of
community interactions.

Committing code is easy:

- Fork the appropriate component repository (see the [component list](#component-list) below for
  links).
- Create a local development branch for the bugfix; we recommend naming the branch such that you'll
  recognize its purpose: `hotfix/mail-header-parsing`, `feature/yaml-serialization`, etc.
- Commit a change, and push your local branch to your github fork.
  ```console
  $ git commit
  $ git push {username} <branchname>:<branchname>
  ```
- Send us a pull request for your changes to be included (see the [component list](#component-list)
  below for links).

For more details, see the [Recommended Workflow for Contributions](#recommended-workflow-for-contributions)
section below.

## RUNNING TESTS

To run tests:

- Clone the repository:

  ```console
  $ git clone git://github.com/{org}/{repo}.git
  $ cd {repo}
  ```

- Install dependencies via composer:

  ```console
  $ composer install
  ```

  If you don't have `composer` installed, please download it from https://getcomposer.org/download/

- Run the tests using the "test" command shipped in the `composer.json`:

  ```console
  $ composer test
  ```

You can turn on conditional tests with the `phpunit.xml` file.
To do so:

 -  Copy `phpunit.xml.dist` file to `phpunit.xml`
 -  Edit `phpunit.xml` to enable any specific functionality you
    want to test, as well as to provide test values to utilize.

## Running Coding Standards Checks

First, ensure you've installed dependencies via composer, per the previous
section on running tests.

To run CS checks only:

```console
$ composer cs-check
```

To attempt to automatically fix common CS issues:

```console
$ composer cs-fix
```

If the above fixes any CS issues, please re-run the tests to ensure
they pass, and make sure you add and commit the changes after verification.

## Recommended Workflow for Contributions

Your first step is to establish a public repository from which we can
pull your work into the master repository. We recommend using
[GitHub](https://github.com), as that is where the component is already hosted.

1. Setup a [GitHub account](https://github.com/), if you haven't yet
2. Fork the repository (https://github.com/{org}/{repo})
3. Clone the canonical repository locally and enter it.

   ```console
   $ git clone git://github.com/{org}/{repo}.git
   $ cd {repo}
   ```

4. Add a remote to your fork; substitute your GitHub username in the command
   below.

   ```console
   $ git remote add {username} git@github.com:{username}/{repo}.git
   $ git fetch {username}
   ```

### Keeping Up-to-Date

Periodically, you should update your fork or personal repository to
match the canonical ZF repository. Assuming you have setup your local repository
per the instructions above, you can do the following:


```console
$ git checkout master
$ git fetch origin
$ git rebase origin/master
# OPTIONALLY, to keep your remote up-to-date -
$ git push {username} master:master
```

If you're tracking other branches -- for example, the "develop" branch, where
new feature development occurs -- you'll want to do the same operations for that
branch; simply substitute  "develop" for "master".

### Working on a patch

We recommend you do each new feature or bugfix in a new branch. This simplifies
the task of code review as well as the task of merging your changes into the
canonical repository.

A typical workflow will then consist of the following:

1. Create a new local branch based off either your master or develop branch.
2. Switch to your new local branch. (This step can be combined with the
   previous step with the use of `git checkout -b`.)
3. Do some work, commit, repeat as necessary.
4. Push the local branch to your remote repository.
5. Send a pull request.

The mechanics of this process are actually quite trivial. Below, we will
create a branch for fixing an issue in the tracker.

```console
$ git checkout -b hotfix/9295
Switched to a new branch 'hotfix/9295'
```

... do some work ...


```console
$ git commit
```

... write your log message ...


```console
$ git push {username} hotfix/9295:hotfix/9295
Counting objects: 38, done.
Delta compression using up to 2 threads.
Compression objects: 100% (18/18), done.
Writing objects: 100% (20/20), 8.19KiB, done.
Total 20 (delta 12), reused 0 (delta 0)
To ssh://git@github.com/{username}/{repo}.git
   b5583aa..4f51698  HEAD -> master
```

To send a pull request, you have two options.

If using GitHub, you can do the pull request from there. Navigate to
your repository, select the branch you just created, and then select the
"Pull Request" button in the upper right. Select the user/organization
"zendframework" (or whatever the upstream organization is) as the recipient.

#### What branch to issue the pull request against?

Which branch should you issue a pull request against?

- For fixes against the stable release, issue the pull request against the
  "master" branch.
- For new features, or fixes that introduce new elements to the public API (such
  as new public methods or properties), issue the pull request against the
  "develop" branch.

### Branch Cleanup

As you might imagine, if you are a frequent contributor, you'll start to
get a ton of branches both locally and on your remote.

Once you know that your changes have been accepted to the master
repository, we suggest doing some cleanup of these branches.

-  Local branch cleanup

   ```console
   $ git branch -d <branchname>
   ```

-  Remote branch removal

   ```console
   $ git push {username} :<branchname>
   ```
