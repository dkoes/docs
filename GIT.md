#`git` Version Control

## Contributing to the docs

[Docs Repo](https://github.com/dkoes/docs) , 
[How to Fork](https://gist.github.com/Chaser324/ce0505fbed06b947d962).

### Setup Your Docs Repo Locally
1. Create (academic) github account.
2. Click Fork.
3. Clone with SSH.
    * `git clone <url from your forked git repository>`
4. Set upstream repo to David's.
    * `git remote add upstream git@github.com:dkoes/docs.git`


### Time to make a change?
1. Get updates from David's repo.
    * `git fetch upstream`
2. Checkout your own local master branch and merge it with David's master.
    * `git checkout master`
    * `git merge upstream/master`
3. **Create and checkout a new branch.**
    * `git checkout master`
    * `git branch <new-name>`
    * `git checkout <new-name>`
4. Make your edits, commit, and push them.
    * `git add <your-new-file>`
    * `git commit -m "descriptive message"`
    * `git push`
5. Go to your github repo online and select the branch you've made. Click on "New Pull Request", and review your changes below before submitting.
