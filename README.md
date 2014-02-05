linux-stable
============

This repo stores branches of the kernel.org linux-stable repo and modifications by Altiscale.

The master branch intentionally includes only this README file.  The release-* branches are exact copies of the kernel.org linux-stable repo release tag.  For example, the release-3.12.7 branch is copy of the kernel.org linux-stable v3.12.7 tag.  The altiscale-* branches contain changes against the stable kernel.org release.  For example, the altiscale-3.12.7 branch manages contain against the release-3.12.7 branch.

Branch Creation
---------------

To create a release-* and corresponding altiscale-* branch, follow the following process, which assumes that most Altiscale personnel will use this repo -- not the kernel.org repo.

##### Clone the kernel.org linux-stable repo.
```bash
$ mkdir kernel-src
$ cd kernel-src
$ git clone git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git
$ cd linux-stable
```

##### Find and check out the appropriate stable kernel.org linux-stable release tag.  For example:
```bash
$ git tag -l | grep v3.12.7
$ git checkout -b released-3.12.7 v3.12.7
```

##### Set up this repo as a remote in the same git repo.
```bash
$ git remote add altiscale git@github.com:Altiscale/linux-stable.git
```

##### Push the released branch to this repo.
```bash
$ git push altiscale released-3.12.7
```

##### Clone this repo.
```bash
$ cd ../..
$ mkdir altiscale-src
$ cd altiscale-src
$ git clone git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git
$ cd linux-stable
```

##### Check out the released-* branch as a tracking branch and use it to create the altiscale-* branch.  For example:
```bash
$ git branch released-3.12.7 origin/released-3.12.7
$ git checkout released-3.12.7
$ git checkout -b altiscale-3.12.7
$ git push origin altiscale-3.12.7
```

##### To make changes, check out a development branch to be used in pull requests.
```bash
$ git checkout -b dc_JIRA-number
```

All pull requests should request merges into altiscale-* branches.  release-* branches should never be modified.  Only changes to this README should be merged into master.

References
----------
- [Linux Kernel Newbies](http://kernelnewbies.org/) [KernelBuild wiki](http://kernelnewbies.org/KernelBuild)
