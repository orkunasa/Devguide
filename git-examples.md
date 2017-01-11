# GIT Examples
## Adding a feature to PX4

Adding a feature to PX4 follows a defined workflow. In order to share your contributions on PX4, you can follow this example.

* [Sign up](https://github.com/join) for github if you haven't already
* Fork the Firmware (see [here](https://help.github.com/articles/fork-a-repo/#fork-an-example-repository))
* Clone your fork to your local computer<br>
```sh
cd ~/wherever/
git clone https://github.com/<your git name>/Firmware.git
```
* Go into the new directory, initialize and update the submodules, and add the original upstream Firmware<br>
```sh
cd Firmware
git submodule update --init --recursive
git remote add upstream https://github.com/PX4/Firmware.git
```
* You should have now two remote repositories: One repository is called upstream that points to the PX4 Firmware,
and one repository that points to your own fork of the PX4 repository. 
* This can be checked with the following command:
```sh
git remote -v
```
* Make the changes that you want to add to the current master.
* Create a new branch with a meaningful name that represents your feature<br>
```sh
git checkout -b <feature branch name>
```
you can use the command ```git branch``` to make sure you're on the right branch.
* Add your changes that you want to be part of the commit<br>
```sh
git add .
```
to add all your files or<br>
```sh
git add <file name>
```
to add single files
* Commit the added files with a meaningful message explaining your changes<br>
```sh
git commit -m "<your commit message>"
```
For a good commit message, please refer to [Contributing](starting-contributing.md) section.
* Some time might have passed and the [upstream master](https://github.com/PX4/Firmware.git) has changed. PX4 prefers a linear commit history and uses [git rebase](https://git-scm.com/book/de/v1/Git-Branching-Rebasing). To include the newest changes from upstream in your local branch, switch to your master branch<br>
```sh
git checkout master
```
Then pull the newest commits from upstream master<br>
```sh
git pull upstream master
```
Now your local master is up to date. Switch back to your feature branch<br>
```sh
git checkout <your branch name>
```
and rebase on your updated master<br>
```sh
git rebase master
```
* Now you can push your local commits to your fork<br>
```sh
git push origin <your branch name>
```
* You can verify that the push was successful by going to your forked repository in your browser: ```https://github.com/<your git name>/Firmware.git```<br>
There you should see the message that a new branch has been pushed to your fork.
* Now it's time to create a pull request (PR). On the right hand side of the "new branch message" (see one step before), you should see a green button saying "Compare & Create Pull Request". Then it should list your changes and you can (must) add a meaningful title (short) and message (explain what you did for what reason. Check [other pull requests](https://github.com/PX4/Firmware/pulls) for comparison)
* You're done! Responsible members of PX4 will now have a look at your contribution and decide if they want to integrate it. Check if they have questions on your changes every once in a while.

## Common pitfalls
After having done the first PR, people from the PX4 community will review your changes. In most cases this means that you have to fix your local branch according to the review. Afther the changes have been done locally, the feature branch needs to be rebased again with the most recent upstream/master. However, after the rebase, it is no longer possible to push the feature branch to your local fork repository directly, but instead you need to use a force push:
```sh
git push --force-with-lease origin <your branch name>
```
### How to handle merge conflicts