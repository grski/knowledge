# giBranching and workflow

In this document we will describe how we work with tasks.


## Branching model and workflow

Gitflow inspired process.

### General rules

Only one long living branch 

We have only one long living branch - we call it master (no surprise here)
each merge to master triggers build process for development environment - which from the partner perspective is staging environment
(more on that in the next section)
we have a special build defined that will do the deploy to the production from a master time - it is either triggered by the developer or
triggered automatically. And we prefer section option - automatic nightly builds on production force us to have a lot of processes in place
\- to avoid downtimes;
Workflow
you find a task in jira
you create feature branch from newest master branch
you implement the feature
you push the changes for the PR review (CI/CD needs to be green - otherwise noone will check it, unless you ask them - this is a valid
approach in some WIP validation)
after approval - the PR is merged to master and instantly deployed to a development environment
over the night your changes will hit the production environment automatically (usually)
We have some basic rules about branch naming:
feature* those are feature branches
bug* related to bug type of the issue
fix* some potential 'one-liner' that does not introduce new functionality
In an ideal world, we would like to have a reference in the branch with the Jira board, so:
git check -b feature-DEEP-899/add-something-something
will be a good approach here.
Why do we think that a 3-tier environment setup is not for us?
The classic 3-tier setup is as follows:
development
staging
production
environments. Without going to the details - development is for developers, it doesn’t need to work, can be broken, and it is open for some heavy
tests done by developers (like infrastructure morphing); staging environment is an environment in which we can describe as pre-production. In
this environment, a partner can check if features are implemented in the correct way before they go to production. The production environment -
well here is where the end-user lives - so this MUST work and MUST work well.
Now - this is not how we do things at thirty3. We merged the development and staging environments and it meets expectations of both groups:
developers and partners. The reason behind that are:
“ “
We are doing ‘zero’ phase projects mostly - having a 3-tier setup adds some complexity and time needed to manage all of the
environments. We wanted to avoid that. We have nothing against 3-tier setup, but we believe that the full benefits of it demonstrate in
later phases of product development.
it forces developers to take care of the development environment - common case is that the development environment in a 3-tier
environment model - doesn’t work, cause it doesn’t need to. It is a simple human bias we would like to fight with.
Cause of the above - we believe it forces us to have better processes and result in better quality.
Where the tests of huge changes happen then? - you can ask - mostly it is done on a local development environment if the development
environment is needed for some breaking tests - we just inform the stakeholders than it can be unavailable for some time, or do the
experiments over the night or late evening.
Worth to note here that development and productions environments not really differs in terms of infrastructure - so we are almost
sure that correct development deployment will result in correct production deployment. The differences in those environments
are quantitive - meaning that production env has usually more nodes of specified type - but the topology of the infastructure is
the same. ”
How to commit
Git log is a powerful database of what happened in the project. We are constantly trying to do a better job here, and we are refusing by default
PR with the poor commit message, poor commit messages are:
fix
implemented
dupa
So how the commit message should look like?
it should have a header with a task number and short message with the context of what changed;
it should have answers to the questions: Why? How? What for?
Note that the best way of work here is to have one commit per pull request - it makes git log much cleaner; you can always
rebase your PR before pushing for review; you can work with as many commits as you want until it is proposed for review - then
ideal case is to have single commit. ”
So how good PR should look like? (it is not perfect yet, but it is a step into good direction)  