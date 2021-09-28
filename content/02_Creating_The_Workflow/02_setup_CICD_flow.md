---
title: "Setup CI/CD Workflow"
chapter: true
weight: 2
---

## Setup your Environments 

In this video, we will be creating the Production and CI/CD Environments that our jobs will run on.

<script src="https://fast.wistia.com/embed/medias/r2ko3r4n5a.jsonp" async></script><script src="https://fast.wistia.com/assets/external/E-v1.js" async></script><div class="wistia_responsive_padding" style="padding:75.21% 0 0 0;position:relative;"><div class="wistia_responsive_wrapper" style="height:100%;left:0;position:absolute;top:0;width:100%;"><div class="wistia_embed wistia_async_r2ko3r4n5a videoFoam=true" style="height:100%;position:relative;width:100%"><div class="wistia_swatch" style="height:100%;left:0;opacity:0;overflow:hidden;position:absolute;top:0;transition:opacity 200ms;width:100%;"><img src="https://fast.wistia.com/embed/medias/r2ko3r4n5a/swatch" style="filter:blur(5px);height:100%;object-fit:contain;width:100%;" alt="" aria-hidden="true" onload="this.parentNode.style.opacity=1;" /></div></div></div></div>

*Summary of this video:*

1. To create the Production environment, click on Environments under the hamburger menu. Click on `New Environment`. Name the Environment. Keep the `Deployment` type and the default dbt version (which is always the latest stable version). Use your user's Redshift credentials for the Deployment environment and called the schema `analytics`.
2. To create the CI/CD environment, repeat the above but name the default schema `qa`.

## Setup CI/CD Workflow

In this video, we will be adding a Pull Request Template and creating the Production and CI/CD jobs.

<script src="https://fast.wistia.com/embed/medias/75k82wvx45.jsonp" async></script><script src="https://fast.wistia.com/assets/external/E-v1.js" async></script><div class="wistia_responsive_padding" style="padding:73.13% 0 0 0;position:relative;"><div class="wistia_responsive_wrapper" style="height:100%;left:0;position:absolute;top:0;width:100%;"><div class="wistia_embed wistia_async_75k82wvx45 videoFoam=true" style="height:100%;position:relative;width:100%"><div class="wistia_swatch" style="height:100%;left:0;opacity:0;overflow:hidden;position:absolute;top:0;transition:opacity 200ms;width:100%;"><img src="https://fast.wistia.com/embed/medias/75k82wvx45/swatch" style="filter:blur(5px);height:100%;object-fit:contain;width:100%;" alt="" aria-hidden="true" onload="this.parentNode.style.opacity=1;" /></div></div></div></div>

*Summary of this video:*

1. Check out a new branch by clicking on `create new branch`. Name the branch `feature/add_pull_request_template`.
2. Create a new folder called `.github` at the same level as the analysis folder. 
3. Create a new file in the folder called `pull_request_template.md`. Paste the following pull request template in.

```md
<!---
Provide a short summary in the Title above. Examples of good PR titles:
* "Feature: add so-and-so models"
* "Fix: deduplicate such-and-such"
* "Update: dbt version 0.20.0"
-->

## Description & motivation
<!---
Describe your changes, and why you're making them. Is this linked to an open
issue, a Trello card, or another pull request? Link it here.
-->


## Changes to existing models:
<!---
Include this section if you are changing any existing models. Link any related
pull requests on your BI tool, or instructions for merge (e.g. whether old
models should be dropped after merge, or whether a full-refresh run is required)
-->

## Screenshots (DAG, query results):
<!---
Include a screenshot of the relevant section of the updated DAG and if you've
created a new model, then show us the results when you query the model. To see
your version of the DAG, run `dbt docs generate && dbt docs serve`.
-->

## Validation of models:
<!---
All PRs should have a test criteria to confirm that the quality of their changes,
which should have been established in your task card. This might look like a
link to an in-development Looker dashboard or a query that compares an existing
model with a new one.
-->

## Checklist:
<!---
This checklist is mostly useful as a reminder of small things that can easily be
forgotten – it is meant as a helpful tool rather than hoops to jump through.
Put an `x` in all the items that apply, make notes next to any that haven't been
addressed, and remove any items that are not relevant to this PR.
-->
- [ ] My pull request represents one logical piece of work.
- [ ] My commits are related to the pull request and look clean.
- [ ] My SQL follows the [dbt Labs style guide](https://github.com/dbt-labs/corp/blob/master/dbt_style_guide.md).
- [ ] I have materialized my models appropriately.
- [ ] I have added appropriate tests and documentation to any new models or fields.
```
4. Save the file by clicking on Save or CMD+S/Ctrl+S 
5. Click on `Open Pull Request`
6. Fill out the Pull Request template and Merge in the Pull Request. 
7. Delete the existing branch. 
8. Now go back to dbt Cloud. Go to Jobs by clicking on the hamburger and click on Jobs.
9. Click on `New Job` for a new Production Job.
10. Fill out the form this way: 
- Name the job `Production Daily`. 
- Choose the Production Environment. 
- Check off generate docs. 
- Add a new command `dbt test` under the `dbt run` command. 
- Update the schedule to run every 12 hours. 
11. Click off the Production job by clicking on `Run Now` 
12. Take a look through the run steps. Take a look at each step and view the documentation site the run generated.
13. Now create the CI/CD job. To do this, fill out the form in this way:
- Name the job: CI/CD 
- Choose the CI/CD Environment
- Check off generate docs 
- Defer to the Production Daily run state 
- Update the dbt run command to `dbt run -m state:modified+` 
- Add a new command `dbt test -m state:modified+` under the dbt run command. 
- Uncheck the `Run on Schedule` and check `Run on Pull Request`

## Helpful Links
- [Here are our docs on SlimCI builds](https://docs.getdbt.com/docs/dbt-cloud/using-dbt-cloud/cloud-enabling-continuous-integration-with-github#slim-ci)
- [Here are our docs on generating documentation](https://docs.getdbt.com/docs/dbt-cloud/using-dbt-cloud/cloud-generating-documentation)
- [Here are our docs on source freshness](https://docs.getdbt.com/docs/dbt-cloud/using-dbt-cloud/cloud-snapshotting-source-freshness)
