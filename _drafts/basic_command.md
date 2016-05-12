# install

    > sudo apt-get install git  
    > homebrew git

# init

    > git config --global user.name "Your Name"  
    > git config --global user.email "email@example.com"
    > git init  
    Create an empty Git repository or reinitialize an existing one

# add files

    > git add file
    > git checkout -- <file>
    
    > git commit -m "desciption"
    > git commit --amend
    > git reset HEAD <file>...

# remove file

    > git rm file
    > git commit

# look difference

    > git diff
    > git diff HEAD -- <file>

# log 

    > git log
    > git reflog

# rollback

    > git reset --hard <ref>
    > git revert <ref>

# push 

    > ssh-keygen -t rsa -C "youremail@example.com"
    > git remote add origin git@github.com:username/XXXX.git
    > git remote add origin https://github.com/username/XXXX.git
    > git push -u origin master

# clone

    > git clone git@github.com:username/learngit.git
    > git clone https://github.com/XXXX/learngit.git
    
    > git push (origin master)


# branch

    > git checkout -b <branch_name>
    Switched to a new branch <branch_name>
    
    > git branch <branch_name>
    > git checkout <branch_name>
    Switched to branch '<branch_name>'
    
    > git branch
    > git branch -f <branch_name> <ref>
    > git merge <branch_name>
    > git branch -d <branch_name> commit_id

# stash

    > git stash
    > git stash list
    > git stash apply@{num}; git stash drop
    > git stash pop

# merge 

    > git merge
    > git merge -no-ff -m "description" <branch_name>

# rebase

    > git rebase (<ref>) <ref>
    > git cherry-pick <ref> <ref> …
    > git rebase -i （<ref>）<ref>（--aboveAll）

# remote

	> git remote -v
    > git fetch 
    > git pull == git fetch;git merge
    > git pull --rebase == git fetch;git rebase
	> git push/fetch <remote> <place> (origin branch-name)
    > git push/fetch origin <source>:<destination> 
    > git push/fetch origin :<branch-name>
	> git checkout -b branch-name origin/branch-name
    > git fakeTeamwork 
    
    > git branch --set-upstream/-u branch-name origin/branch-name

# tag

	> git tag <tag_name>(v1.0)
	> git tag -a <tag_name> -m "..."
	> git tag -s <tag_name> -m "..." (PGP)
	> git tag
    > git describe <ref>
	> git push origin <tag_name>
	> git push origin --tags
	> git tag -d <tag_name>
	> git push origin :refs/tags/<tag_name>
	> git push origin --delete tag <tag_name>

# config

	> git config (--global) color.ui true

# alias

	> git config (--global) alias.xx 'option'
     
	> git config --global alias.unstage 'reset HEAD'
	> git config --global alias.last 'log -1'
	> git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

# server

[build git server](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137583770360579bc4b458f044ce7afed3df579123eca000)
