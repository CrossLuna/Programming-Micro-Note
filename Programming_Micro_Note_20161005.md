#Programming Micro Note 20161005

##Git - conflict when pulling (Github)
Source:  
[Resolve conflicts using remote changes when pulling from Git remote](http://stackoverflow.com/questions/4785107/resolve-conflicts-using-remote-changes-when-pulling-from-git-remote)  
[Git denying non-fast forward 問題](https://blog.wu-boy.com/2013/03/git-denying-non-fast-forward/)  

Q:  
Situation:  
I forked one repo, didn't touch it for a while. Today I wanted to keep my forked repo up to date so I used
```bash
$ git pull upstream master
```
where `upstream` is the original repo and `origin` is my forked one.
Then I got tons of conflict error messages, there must have been some problems with local changes. In today's case, I don't care about my local changes (or some malfunctions or whatever) and just want to update my forked repo to the latest commit.

A:  
Here is the solution.
```bash
# fetch from the remote, upstream
$ git fetch upstream
# reset your current branch (master) to upstream's master
$ git reset --hard upstream/master
```
Warning: `--hard` option can be fatal, make sure what you're doing!  
Then I tried to push back to Github, got the message
```bash
$ git push origin master
To https://github.com/CrossLuna/algorithm-exercise.git
 ! [rejected]        master -> master (non-fast-forward)
```
and the solution is
```bash
$ git push --force origin master
```