---
title: "Setup dbt Cloud Account"
chapter: true
weight: 5
---

## Setting up dbt Cloud account

In this video, we will walk you through setting up your dbt Cloud account and dbt cloud project. 

<script src="https://fast.wistia.com/embed/medias/uwg23pkfa0.jsonp" async></script><script src="https://fast.wistia.com/assets/external/E-v1.js" async></script><div class="wistia_responsive_padding" style="padding:66.88% 0 0 0;position:relative;"><div class="wistia_responsive_wrapper" style="height:100%;left:0;position:absolute;top:0;width:100%;"><div class="wistia_embed wistia_async_uwg23pkfa0 videoFoam=true" style="height:100%;position:relative;width:100%"><div class="wistia_swatch" style="height:100%;left:0;opacity:0;overflow:hidden;position:absolute;top:0;transition:opacity 200ms;width:100%;"><img src="https://fast.wistia.com/embed/medias/uwg23pkfa0/swatch" style="filter:blur(5px);height:100%;object-fit:contain;width:100%;" alt="" aria-hidden="true" onload="this.parentNode.style.opacity=1;" /></div></div></div></div>

*Summary of this video:*

1. The IDE is where we will be developing our dbt code. 
2. To setup the Redshift connection, you will need to choose Redshift as the data warehouse/database. Fill out the Redshift information from Cloudformation output. Your hostname is the entire hostname. The port is `5439` and the database is `dbtworkshop`.
3. When you setup your Redshift connection, you will be asked for your development credentials. Those credentials (as provided in your cloudformation output) will be:
- username:`dbtadmin` 
- password: `Dbtadmin108!`
- schema: This is your sandbox schema where you will build all of your development objects into. 
5. You will need to setup the Github application first before setting up the Github connection. In order to do this, you're going to integrate your dbt User with github, authorize the Github application, and then setup the repository connection. 

## Helpful Links
[Here are our docs for connecting to Redshift](https://docs.getdbt.com/docs/dbt-cloud/cloud-configuring-dbt-cloud/connecting-your-database)
Here are our docs for connecting to different git providers: 
- [Github](https://docs.getdbt.com/docs/dbt-cloud/cloud-configuring-dbt-cloud/cloud-installing-the-github-application)
- [Gitlab](https://docs.getdbt.com/docs/dbt-cloud/cloud-configuring-dbt-cloud/connecting-gitlab)
- [other git providers](https://docs.getdbt.com/docs/dbt-cloud/cloud-configuring-dbt-cloud/cloud-import-a-project-by-git-url)