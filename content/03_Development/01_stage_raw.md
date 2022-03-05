---
title: "Stage Raw Data"
chapter: true
weight: 1
---

## Stage Raw Data

In this video, we will demostrate how to install a package and then use the package to stage our data that lives in the S3 bucket.

<script src="https://fast.wistia.com/embed/medias/s2f0zjie0o.jsonp" async></script><script src="https://fast.wistia.com/assets/external/E-v1.js" async></script><div class="wistia_responsive_padding" style="padding:73.13% 0 0 0;position:relative;"><div class="wistia_responsive_wrapper" style="height:100%;left:0;position:absolute;top:0;width:100%;"><div class="wistia_embed wistia_async_s2f0zjie0o videoFoam=true" style="height:100%;position:relative;width:100%"><div class="wistia_swatch" style="height:100%;left:0;opacity:0;overflow:hidden;position:absolute;top:0;transition:opacity 200ms;width:100%;"><img src="https://fast.wistia.com/embed/medias/s2f0zjie0o/swatch" style="filter:blur(5px);height:100%;object-fit:contain;width:100%;" alt="" aria-hidden="true" onload="this.parentNode.style.opacity=1;" /></div></div></div></div>

*Summary of this video:*

1. Check a new branch. To do this, you will need to check out the `main`/`master` branch first and then click on create a new branch (`feature/stage_tpch_data`). If you get the button `Pull from Remote`, feel free to do so. This is an indictation that something has changed the remote branch and you will want to pull those changes into your remote branch. 
2. Create a `packages.yml` file on the same level as your `dbt_project.yml` file
3. Add the following code to the file. 

```yml 
packages:
   - package: dbt-labs/dbt_external_tables
      version: 0.8.0
   - package: dbt-labs/dbt_utils
      version: 0.8.1  
```

The video mentions that installing the `dbt_external_tables` package will also install the `dbt_utils` package because it is used as a dependency. While this was true in previous versions, the updated version being used now does not perform the same auto-install. It's important to include the `dbt_utils` package as shown above when creating your `packages.yml` file to avoid errors when creating your external tables in step 11.
4. Run `dbt deps` to install the package. A way to remember this command is deps = dependencies. 
5. Create a `staging` folder in the `models` folder. 
6. Create a folder named `tpch` inside of the `staging` folder.
7. Create the `sources.yml` file inside of the tpch folder.
8. Paste this code into the `sources.yml` file: 

```yml 

version: 2

    sources:
      - name: tpch
        database: dbtworkshop
        schema: tpch_s3_data
        loader: s3
        loaded_at_field: collector_tstamp
      
        tables:
                
          - name: lineitem
            external:
                location: "s3://dbt-data-lake-[Insert AWS Account ID]]/dbtworkshopdata/lineitem/" 
                row_format: serde 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
                table_properties: "('skip.header.line.count'='1')"
            columns:
              - name: l_orderkey
                data_type: varchar(255)
                description: "primary key"
              - name: l_partkey
                data_type: varchar(255)
              - name: l_suppkey
                data_type: varchar(255)
              - name: l_linenumber
                data_type: varchar(255)
              - name: l_quantity
                data_type: varchar(255)            
              - name: l_extendedprice
                data_type: varchar(255)
              - name: l_discount
                data_type: varchar(255)
              - name: l_tax
                data_type: varchar(255)                       
              - name: l_returnflag
                data_type: varchar(255)  
              - name: l_linestatus
                data_type: varchar(255)   
              - name: l_shipmode
                data_type: varchar(255)             
              - name: l_shipdate
                data_type: timestamp  
              - name: l_commitdate
                data_type: timestamp
              - name: l_receiptdate
                data_type: timestamp           
         
          - name: orders
            external:
                location: "s3://dbt-data-lake-[Insert AWS Account ID]/dbtworkshopdata/orders/"      
                row_format: serde 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
                table_properties: "('skip.header.line.count'='1')"
            columns:
              - name: o_orderkey
                data_type: varchar(255)
                description: "primary key"
              - name: o_custkey
                data_type: varchar(255)
              - name: o_orderstatus
                data_type: varchar(255)
              - name: o_totalprice
                data_type: varchar(255)
              - name: o_orderdate
                data_type: varchar(255)
              - name: o_orderpriority
                data_type: varchar(255)
              - name: o_clerk
                data_type: varchar(255)
              - name: o_shippriority
                data_type: varchar(255)
              - name: o_comment
                data_type: varchar(255)
     
```

9. Now go to the S3 Management Console and find a S3 bucket that starts with the prefix `dbt-data-lake-`
10. Update the location field in the sources.yml file to point to your lineitem and orders files. They will be almost the same as this `s3://dbt-data-lake-486758181003/dbtworkshopdata/lineitem/` with different numbers for you S3 bucket name. Do not include the `.csv`
11. Run the command `dbt run-operation stage_external_sources` to create the external tables.
12. Run `dbt docs generate` to the documentation site. 
13. Click on `view docs` to view the documentation.



## Helpful Links 
- If you wish to see the external tables you created via the `dbt run-operation stage_external_sources`, go into the Redshift Query editor, connect and check out the tables in the schema `tpch_s3_data`
- [Operations Macros](https://docs.getdbt.com/reference/commands/run-operation)
