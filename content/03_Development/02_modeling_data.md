---
title: "Transform Raw Data"
chapter: true
weight: 2
---

## Transform Raw Data

In this video, we will be modeling our raw data into two staging models and one fact model, using dimensional modeling paradigms. We will be joining the two staging models (which have a 1:1 to the raw data source table) via the order_key as the foreign key. 

For more information on how we structure our dbt project, [click on this link](https://discourse.getdbt.com/t/how-we-structure-our-dbt-projects/355). It should be noted that dbt is agnostic to 
all modeling paradigms ([Data Vault](https://dbtvault.readthedocs.io/en/latest/), Kimball, etc). So while we will be following a dimensional modeling paradigms, as long as your models are in the `Models` subdirectory, dbt will be able to compile and execute. 

<script src="https://fast.wistia.com/embed/medias/6qocbhe33q.jsonp" async></script><script src="https://fast.wistia.com/assets/external/E-v1.js" async></script><div class="wistia_responsive_padding" style="padding:71.46% 0 0 0;position:relative;"><div class="wistia_responsive_wrapper" style="height:100%;left:0;position:absolute;top:0;width:100%;"><div class="wistia_embed wistia_async_6qocbhe33q videoFoam=true" style="height:100%;position:relative;width:100%"><div class="wistia_swatch" style="height:100%;left:0;opacity:0;overflow:hidden;position:absolute;top:0;transition:opacity 200ms;width:100%;"><img src="https://fast.wistia.com/embed/medias/6qocbhe33q/swatch" style="filter:blur(5px);height:100%;object-fit:contain;width:100%;" alt="" aria-hidden="true" onload="this.parentNode.style.opacity=1;" /></div></div></div></div>


*Summary of this video:*

1. In your `tpch` folder, create a new file called `stg_tpch_line_items.sql`.
2. In the file, paste in the following code:

```sql

{{ config(materialized='table') }}

with source as (

    select * from {{ source('tpch', 'lineitem') }}

),

renamed as (

    select
    
        {{ dbt_utils.surrogate_key(
            ['l_orderkey', 
            'l_linenumber']) }}
                as order_item_key,
        l_orderkey as order_key,
        l_partkey as part_key,
        l_suppkey as supplier_key,
        l_linenumber as line_number,
        l_quantity as quantity,
        l_extendedprice as extended_price,
        l_discount as discount_percentage,
        l_tax as tax_rate,
        l_returnflag as return_flag,
        l_linestatus as status_code,
        l_shipdate as ship_date,
        l_shipmode as ship_mode, 
        l_commitdate as commit_date,
        l_receiptdate as receipt_date

    from source

)

select * from renamed


```

3. Run the command `dbt run -m stg_tpch_line_items` to create the table in your Redshift database.
4. Create a new file in the `tpch` folder called `stg_tpch_orders.sql`.
5. Paste the following code into the file:

```sql
{{ config(materialized='table') }}

with source as (

    select * from {{ source('tpch', 'orders') }}

),


renamed as (

    select
    
        o_orderkey as order_key,
        o_custkey as customer_key,
        o_orderstatus as status_code,
        o_totalprice as total_price,
        o_orderdate as order_date,
        o_orderpriority as priority_code,
        o_clerk as clerk_name,
        o_shippriority as ship_priority

    from source

)

select * from renamed

```
6. Run `dbt run -m stg_tpch_orders` to create the object. 
7. Create the folder `marts` in your `models` subdirectory.
8. Create the folder `core` in your `marts` folder. 
9. Create the file `fct_order_item.sql` in the core folder.
10. Paste in this code into the file: 

```sql


with orders as (
    
    select * from {{ ref('stg_tpch_orders') }}

),

line_item as (

    select * from {{ ref('stg_tpch_line_items') }}

)
select 

    line_item.order_item_key,
    orders.order_key,
    orders.customer_key,
    line_item.part_key,
    line_item.supplier_key,
    orders.order_date,
    orders.status_code as order_status_code,
    
    
    line_item.return_flag,
    
    line_item.line_number,
    line_item.status_code as order_item_status_code,
    line_item.ship_date,
    line_item.commit_date,
    line_item.receipt_date,
    line_item.ship_mode,
    line_item.extended_price,
    line_item.quantity

from
    orders
inner join line_item
        on orders.order_key = line_item.order_key
order by
    orders.order_date
```

11. Run model using `dbt run -m fct_order_item`
12. Rename the column `ship_mode` in `fct_order_item` to `ship_method`. Rename the column `l_shipmode` in `stg_tpch_line_items`
13. Run the command `dbt run -m stg_tpch_line_items+` to run the staging model and its dependencies.
14. Create a new file called `tpch.yml` in your tpch folder. 
15. In the model, paste the following code:

```yml 
version: 2

    models:
        - name: stg_tpch_line_items
          description: "Staging model for raw external line items table in S3"
          columns:
              - name: order_item_key
                description: "The primary key for this table"
                tests:
                    - unique
                    - not_null
```
16. Add to the schema.yml file with a description and primary key tests for the `stg_tpch_orders` model. Your final schema.yml file will look like this:


```yml 
version: 2

    models:
        - name: stg_tpch_line_items
          description: "Staging model for raw external line items table in S3"
          columns:
              - name: order_item_key
                description: "The primary key for this table"
                tests:
                    - unique
                    - not_null
    
        - name: stg_tpch_orders
          description: "Staging model for raw external orders table in S3"
          columns:
              - name: order_key
                description: "The primary key for this table"
                tests:
                    - unique
                    - not_null    
``` 
17. Add a `core.yml` file to the `core`. 
18. Add a description and primary key tests for the `fct_order_items` model. It will look like this: 

```yml
version: 2

models:
    - name: fct_order_items
      description: "fct model for order items"
      columns:
          - name: order_item_key
            description: "The primary key for this table"
            tests:
                - unique
                - not_null
```
19. Run the tests on your models with the command `dbt test -m +fct_order_item`
20. Generate the documentation by running the command `dbt docs generate` and explore the docs site. 



## Helpful tips
- If you would like to see what you created by doing `dbt run` commands, go into the Redshift Query Editor, connect and check out the objects in your development schema. 
- If you come across an partial parsing compilation error while working with the yml files, go into your target folder and delete the file `partial_parse.msgpack` and rerun. 