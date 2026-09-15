# Developer Workflow

## Clone the repo

- cd into the folder you want to clone the repo in (for example, ACIT 4880/Projects).
- run the command: `git clone https://github.com/BCIT-ACIT4880-2026-Fall/CRN-45883-5.git`
- run `cd CRN-45883-5`

## Branching off master:

We will not pull directly from the main branch. Instead as a standard of dev work we must pull from the staging branch (ideally named "master").

- Once, in the `CRN-45883-5` run `git pull master`. This will add all the latest changes into your local work environment.
- Once pulled, we will create branches using `git checkout -b <branch_name>`. Ideal branch names will include your initials and the feature/area of the work to be done, example for someone named John Wills working on parsing a csv file the branch name will be `JW/parsing-csv`.
- Once the work is done on the branch, we will add the changes using `git add <changes>` where <changes> include what files were changed during the work. Next step will be committing the added work using `git commit -m "YOUR COMMIT MESSAGE"`, please use a meaningful commit message that are ideally the description the work you did. then we push to the branch using `git push origin <branch-name>` **IMPORTANT!**: DO NOT PUSH TO **main** or **master**. PLEASE PUSH TO THE BRANCH NAME YOU WORKED ON.
- Once pushed, please go to the github repo -> Pull requests. Click on open a new pull request, select base as `master` (NOT main) and the compare branch as the branch you pushed.
- Someone will review the branch once the CI/CD checks pass and will merge it into master
- Onced merged, go to your work environment terminal and run `git checkout master; git pull`.

#### Now you have all the latest changes you made. Happy Coding :)
