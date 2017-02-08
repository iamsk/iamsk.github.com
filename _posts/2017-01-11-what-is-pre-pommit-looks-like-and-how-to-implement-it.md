---
layout: single
title: what is pre commit looks like and how to implement it 
tags: [git, pre-commit, refactoring, git, hook]
---
The `pre-commit` can find and fix common issues before changes are submitted for code review;

Code reviewers should pay attention to the architecture of a change and not worry about trivial errors like `syntax error`, `not following code style`, `test missing`.

## How to implement pre-commit [TL;DR]

1. write a python script(`pre-commit.py`) to check all the checkable files and print error messages;
	1. get all committed files;
	2. filter with exclude files;
	3. split files into `.py`, `.js` and `.html`;
	4. check with customize pep8, pylint, isort, jshint, jscs etc;
	5. commit continue if all check pass, else we will have more details in report file.
2. write a shell script(`pre_commit`)(name should not change) which actually called by git command;
	1. active the specific env(which create by step 3);
	2. execute the real checker script.
3. write another shell script(`install_pre_commit.sh`) to install pre-commit;
	1. make a independent env with virtualenv;
	2. install third libs in this env, such as pep8, pylint, isort etc(make sure they have specific version number);
	3. copy the `pre_commit` shell script to git directory and make it executable.

## Actually you should not reinvent the wheel
1. pip install pre-commit;
2. pre-commit install;
3. create file `.pre-commit-hooks.yaml` at the root of your repo and configure your hooks.

### the simplest hooks configuration like this:

```python
- repo: git://github.com/pre-commit/pre-commit-hooks
  sha: v0.4.2
  hooks:
  - id: trailing-whitespace
```

### additional information

* [Out of box hooks][1]
* [How to create custom hooks][2]
* [Tutorial][3]

[1]:	http://pre-commit.com/hooks.html
[2]:	http://pre-commit.com/#new-hooks
[3]:	http://pre-commit.com/#install