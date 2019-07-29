# 📘 Repositories best-practices

The document describes the best-practices to create and maintain PDND repositories, including the repository structure, mandatory and optional files, readme files' structure, issue templates, branch rules, and more.

## Nomenclature

The majority of the PDND repositories live in a shared GitHub space. For this reason it's a good practice to prefix all the PDND related repositories using the word  *pdnd*, for example *pdnd-template*.

## Description

Descriptions are important to tell users what you're doing in few words. Try to always add one or two lines of descriptions to your repository.

## PDND template

To avoid confusion and style segmentation between repositories, the community has created a dedicated GitHub template repository, name [pdnd-template](https://github.com/teamdigitale/pdnd-template).

The repository template should be used

* to create new repositories (after clicking new, select as repository template the [pdnd-template](https://github.com/teamdigitale/pdnd-template))

* as source to verify the conformance of existing repositories. Simply go on GitHub or clone the repository and verify that the repository you're owner for has all the requirements needed

The [pdnd-template](https://github.com/teamdigitale/pdnd-template) repository includes the following features/files:

* **Repository description** - mandatory - The template repository comes with a description. Simply change the default one and adapt it to your needs.

* **README.md** - mandatory - Must have sections include the header (with the correct project nomenclature), the "What is the PDND (ex DAF)" section, the copyright section at the bottom. The rest of the sections can be imported from your actual readme.

* **AUTHORS** - mandatory

* **LICENSE** - mandatory - The work produced by the Team is generally committed under the *GNU AFFERO GENERAL PUBLIC LICENSE - version 3* license. Make sure this applies to your work as well or [talk to somebody of the Team](who-does-what.md) about this.

* **.circleci folder** - optional - The Team uses CircleCI as the default Continuous Integration tool to run tests and make sure the code works before it can be merged. The *.circleci* folder contains an exemplar CircleCI configuration, used to setup a generic Ansible linting job. The CI job uses a standard [pdnd-infra-test-env image](https://github.com/teamdigitale/pdnd-infra-test-env) that contains basic test tools (i.e. python, git, ansible-lint, ...). Once the configuration file has been merged, jobs triggering needs to be activated by one of the infrastructure [administrators](who-does-what.md) from the CircleCI portal.

* **.github (issue templates)** - mandatory - contains a template for your users to open issues. Simply copy it to your repository. GitHub will automatically render it when users open new issues.

* **.gitignore** - mandatory - removes standard MacOS files and IntelliJ files. Complete it for your needs.

* **.gitattributes** - mandatory - helps people with Windows and specific editors to commit code using the same format. 

## Additional steps (cannot be inherited by pdnd-template)

Some properties and checks cannot be inherited by the *template repository*, so it's up to its owner to enable them manually. This includes

* **Teams and Collaborators** - You should add teams and collaborators who can access your repository. Prefer predefined teams to single collaborators to avoid future complexity.

* **Branch rules** - Go to the *settings section* of your repository -> branches -> add rule -> insert the name of the branch the rule should match against (i.e. dev, master) -> select the options A) *"Require pull request reviews before merging"*, then *"Require review from Code Owners"* B) Require status checks to pass before merging C) Restrict who can push to matching branches. This will guarantee users to need a *"+1"* from someone else before the code could be merged, that possible CircleCI jobs pass, and that only administrators -in case of emergencies- can directly push fixes to branches.

* **Security Team and Alerts** - The *security* GitHub Team is an alias pointing to the [people responsible for the ciber security] issues. The team should be alerted at any time GitHub finds a vulnerability in your code. To make this happen: 1) add the *security* team under the settings/Collaborators and Team section of your repository 2) add the *security* team under the settings/Security Alerts section of your repository.

## Branches structure and versioning 

Branches structure is predefined and should be consistent between all projects, in order to make everyone's life easier.

Repositories can be grouped in two categories:

* **application and services** - for example parts of the front-end, or back-end components running on Kubernetes. Each of these repositories should have a *dev* branch where all commits should be first merged and tested. Commits should be then promoted to the master branch, representing the production. Periodically, the master branch should be tagged.

* **infrastructure/operational repositories** - usually, these repositories are used to provision the infrastructure (i.e. Azure resources, virtual machines). In this case, different branches apply to different environments (i.e. development, staging, production). As such, the master branch has been removed many branches -as many as the environments are- have been created. In principle, commits should first be committed to development, then promoted to staging, then production. Periodically, at least master should be tagged.

This *pdnd-handbook* repository is an exception and only uses the *master* branch, that should be periodically tagged.

Tagging follows the classic [Semantic Versioning model](https://semver.org/).
