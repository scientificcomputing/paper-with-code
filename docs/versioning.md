(versioning)=
# Versioning

When working with a paper it is important to keep track of the history of your projects. For example, you might be introducing some changes that might change the output, and being able to go back to an earlier version is therefore important. Furthermore, if you are more than one person working on a project it would be good to work independently on separate versions and merge your changes into the main branch when ready (of course after a review by someone else in the team)

## Git and GitHub
Git is a version control system that solves all of these issues by making commits containing messages of what has changed since the last commit. It also allows different people to work on independent branches that can be merged into the main branch via a pull request. A pull request is an action where you ask another person in the team whether the changes you made are OK to merge into the main branch. The other team members can then use GitHub to review your changes and comment on the changes you made.

## Tagging specific versions of your repository
Some versions of your repository are more important than others. For example, the version of your repository when you submit the paper after you addressed the first review of your paper, and the final version that contains the code for the journal publication. Being able to easily go back to these versions might be a good idea. You can achieve this by [creating a tag](https://www.atlassian.com/git/tutorials/inspecting-a-repository/git-tag)

When the correct git commit is checked you create a tag as follows
```bash
git tag -a v_first_submission -m "First submission"
```
or
```bash
git tag -a v_final -m "Final submission"
```
Here the prefix `v` is meant to represent *version*. You can push that tags to GitHub using the `--tags` flag, i.e
```
git push --tags
```
It is good to set up a GitHub action that will build and deploy a [Docker image](environment.md) every time you push a tag to the repository. That way, you will be able to reproduce the environment for all the important versions of your code.

## Changelog
It is also good practice to keep track of the changes you make between two version. You can do this by writing a [changelog](https://en.wikipedia.org/wiki/Changelog). You can write a markdown file called `CHANGELOG.md` with the following version

```markdown
# Changelog

---

## Final version
- tag: `v_final`

### Changes
- Added figure 3.1
- Rewritten section about ..

---

## Second submission
- tag: `v_second_submission`

### Changes
- Run new experiments
    - Added descriptions in section 2.4
    - Added results in Section 3.4
- Change Table 2.1

---

## First submission
- tag: `v_first_submission`


---

```
Note that if you write descriptive commit messages you can use these messages in your changelog. For example to get all commit messages between the `v_first_submission` and `v_second_submission` tags you can e.g

```bash
git log --pretty=oneline v_first_submission...v_second_submission
```
If you need to get all commit messages from the very beginning to e.g `v_first_submission` you can do
```bash
git log --pretty=oneline $(git rev-list --max-parents=0 HEAD)...v_first_submission
```
