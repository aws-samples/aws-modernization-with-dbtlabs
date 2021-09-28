---
title: "Validate Code"
chapter: true
weight: 3
---

## Use CI/CD Workflow for Code Validation

In this video, we will walk through 
- creating a good pull request
- using a SlimCI job to validate your code 
- merging code into your production git branch
- deploying the code to Redshift

<script src="https://fast.wistia.com/embed/medias/rkjwdpo8lx.jsonp" async></script><script src="https://fast.wistia.com/assets/external/E-v1.js" async></script><div class="wistia_responsive_padding" style="padding:73.33% 0 0 0;position:relative;"><div class="wistia_responsive_wrapper" style="height:100%;left:0;position:absolute;top:0;width:100%;"><div class="wistia_embed wistia_async_rkjwdpo8lx videoFoam=true" style="height:100%;position:relative;width:100%"><div class="wistia_swatch" style="height:100%;left:0;opacity:0;overflow:hidden;position:absolute;top:0;transition:opacity 200ms;width:100%;"><img src="https://fast.wistia.com/embed/medias/rkjwdpo8lx/swatch" style="filter:blur(5px);height:100%;object-fit:contain;width:100%;" alt="" aria-hidden="true" onload="this.parentNode.style.opacity=1;" /></div></div></div></div>

*Summary of this video:*

1. Commit any code that you might not have since the previous video.
2. Click on `Open Pull Request`
3. Fill out the Pull Request Template to the best of your abilities. 
4. Click on `Create Pull Request`
5. Wait for the dbt Cloud CI/CD job to kick off and complete. 
6. Click into the specific run and explore the run steps. 
7. After getting a successful run, merge in the code and delete your branch. 
8. Go into dbt Cloud and kick off your Production job. 

## Helpful Tips

- Always let your CI/CD job run to completion. This is because dbt Cloud creates a temporary schema to build into for the run. Once the job is complete, dbt Cloud will then drop the temporary schema which will help maintain your clean database.