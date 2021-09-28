---
title: "Setup dbt Cloud Project"
chapter: true
weight: 1
---

## Setup dbt Cloud Project
In this video, we will go through 
- setting up your dbt project
- running and testing the sample models
- see what it will look like to correct a broken test. 

<script src="https://fast.wistia.com/embed/medias/q0xm7mdt61.jsonp" async></script><script src="https://fast.wistia.com/assets/external/E-v1.js" async></script><div class="wistia_responsive_padding" style="padding:73.13% 0 0 0;position:relative;"><div class="wistia_responsive_wrapper" style="height:100%;left:0;position:absolute;top:0;width:100%;"><div class="wistia_embed wistia_async_q0xm7mdt61 videoFoam=true" style="height:100%;position:relative;width:100%"><div class="wistia_swatch" style="height:100%;left:0;opacity:0;overflow:hidden;position:absolute;top:0;transition:opacity 200ms;width:100%;"><img src="https://fast.wistia.com/embed/medias/q0xm7mdt61/swatch" style="filter:blur(5px);height:100%;object-fit:contain;width:100%;" alt="" aria-hidden="true" onload="this.parentNode.style.opacity=1;" /></div></div></div></div>

*Summary of this video:*

1. Click on the hamburger menu and click on `Develop` to go to the IDE.
2. To initialize the dbt project, click on the `initialize your project`.
3. Take a look around the project after it is initialized. The dbt_project.yml is the key file that dbt looks for in order to understand that a directory is a dbt project. 
4. Next we are going to run the example dbt models by running the command `dbt run` on the command line. 
5. To run the tests on the models, run the command `dbt test`.
6. To fix the failing model `my_first_dbt_model`, click on the model file and update the select statement from 

```sql 

with source_data as (
    
    select 1 as id 
    union all 
    select null as id 
    
)

select * from source_data

```

to 

```sql 

with source_data as (
    
    select 1 as id 
    union all 
    select 2 as id 
    
)

select * from source_data

```
7. To only rerun the previously broken model, run the command `dbt run -m my_first_dbt_model`
8. To only rerun the previously failing test, run the command `dbt test -m my_first_dbt_model`
9. Now let's commit the work by clicking on the commit button on the left, provide a commit message `setup dbt project`, and click on `Commit`. This is the first and last time we will be committing directly to the master branch.

## Helpful Links
- To learn more about the dbt_project.yml, [click here](https://docs.getdbt.com/reference/dbt_project.yml)
- To learn more about dbt commands, [click here](https://docs.getdbt.com/reference/dbt-commands)
- [dbt Materializations](https://docs.getdbt.com/docs/building-a-dbt-project/building-models/materializations)
- [dbt tests](https://docs.getdbt.com/docs/building-a-dbt-project/tests)
