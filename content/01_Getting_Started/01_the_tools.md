---
title: "The Tools"
chapter: true
weight: 1
---

## The Tools

In these videos, we will be providing a high level overview of the tools that we will be using for this workshop. We will be using Redshift, S3 Bucket, Github, and of course dbt. If you're curious about what other data warehouses/data lakes dbt supports, [check out this link](https://docs.getdbt.com/docs/available-adapters). dbt Cloud also works with all git providers with advanced functionality with Github and Gitlab. 

In terms of understanding git for this workshop, dbt Cloud will guide you through a simplifed git workflow, where you don't need to write a single git command. However if you're interested in learning git basics, [check out this video to get an overview of git and version control](https://getdbt.wistia.com/medias/zaaege6v76). You do not need to understand git for this workshop.

## Overview of Redshift, S3 Bucket, Github

<script src="https://fast.wistia.com/embed/medias/6gc3ojy45n.jsonp" async></script><script src="https://fast.wistia.com/assets/external/E-v1.js" async></script><div class="wistia_responsive_padding" style="padding:73.33% 0 0 0;position:relative;"><div class="wistia_responsive_wrapper" style="height:100%;left:0;position:absolute;top:0;width:100%;"><div class="wistia_embed wistia_async_6gc3ojy45n videoFoam=true" style="height:100%;position:relative;width:100%"><div class="wistia_swatch" style="height:100%;left:0;opacity:0;overflow:hidden;position:absolute;top:0;transition:opacity 200ms;width:100%;"><img src="https://fast.wistia.com/embed/medias/6gc3ojy45n/swatch" style="filter:blur(5px);height:100%;object-fit:contain;width:100%;" alt="" aria-hidden="true" onload="this.parentNode.style.opacity=1;" /></div></div></div></div>

*Summary of this video:*
- We will be using Redshift as our Data Warehouse to compute and store our transformations. We will be using the Spectrum feature to query from S3. 
- Our S3 bucket is our object storage. It's great for storing large amounts of data. 
- Github will be our version control/git provider. It will be our code storage and code change management system.

## Overview of dbt

<script src="https://fast.wistia.com/embed/medias/mwymobgl5w.jsonp" async></script><script src="https://fast.wistia.com/assets/external/E-v1.js" async></script><div class="wistia_responsive_padding" style="padding:73.33% 0 0 0;position:relative;"><div class="wistia_responsive_wrapper" style="height:100%;left:0;position:absolute;top:0;width:100%;"><div class="wistia_embed wistia_async_mwymobgl5w videoFoam=true" style="height:100%;position:relative;width:100%"><div class="wistia_swatch" style="height:100%;left:0;opacity:0;overflow:hidden;position:absolute;top:0;transition:opacity 200ms;width:100%;"><img src="https://fast.wistia.com/embed/medias/mwymobgl5w/swatch" style="filter:blur(5px);height:100%;object-fit:contain;width:100%;" alt="" aria-hidden="true" onload="this.parentNode.style.opacity=1;" /></div></div></div></div>

*Summary of this video:*
- dbt was created to allow data teams to unite on SQL and then work with software engineer best practices. 
- dbt allows you to develop, document, test, deploy your transformations inside of your data warehouses. 
- Developing in dbt can be done via the dbt Cloud IDE or the command line. dbt helps folks express business logic in SQL, removing any black box around data transformations and improve on data trust. 
- Using dbt's ref function and ability to write DDL and DML, you can create repeatable builds and promote through environments without having to change the code. The ref function also builds dependencies automatically so you can focus on modeling, not run order or having to manually create the DAG via a third party tool.
- dbt docs compiles the information you supply dbt via the project and the data warehouse information schema to a sharable documentation site that you can use for yourself and stakeholderse. Documentation also can automatically display lineage from raw objects to transformation to third party dependencies.
- dbt Tests are all written in SQL and can be used to validate your data assumptions. 
- By using dbt, you can provide a version control and CI/CD workflow to anyone comfortable with SQL.




