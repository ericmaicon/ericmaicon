title: "SVN: Revert changes on an entire folder"
date: 2015-06-20 20:21:43
categories:
- SVN
tags:
- SVN
---
![SVN](/thumbnails/svn.jpg)

In a former project, I needed to deal with a SVN repo. To revert changes in an entire folder, I used the following command:

```sh
svn revert somefolder --recursive
```

To revert to a specific revision, you can use the command:

```sh
svn merge -r HEAD:12345 .
```

You can check more about revisions in [https://josephscott.org/archives/2010/01/revert-to-a-previous-version-in-subversion/](https://josephscott.org/archives/2010/01/revert-to-a-previous-version-in-subversion/).