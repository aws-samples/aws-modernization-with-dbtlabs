---
title: "Setup Redshift"
chapter: true
weight: 4
---

## Setup Redshift and S3

To setup Redshift and S3, follow these steps:

### For AWS Event

You will be provided to an AWS Account to run this workshop. The temporary account is being created using Event Engine. You will be provided a participant hash key to login to your temporary account.
Follow these steps to start using your account:

1. Connect to the portal by clicking the button or browsing to https://dashboard.eventengine.run/ 
1. Enter the provided hash in the text box. The button on the bottom right corner changes to Accept Terms & Login. Click on that button to continue.
1. Set Team Name to either individual name or a team name if part of a team.
1. Click on AWS Console on dashboard. This will open AWS Console in a new browser tab.
1. Launch the stack. <a href="https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=dbt-workshop&templateURL=https://tpch-sample-data.s3.amazonaws.com/create-dbtworkshop-infr" />Click Here</a>
1. Click `Next` till the end and then select acknowledgement checkbox. Then click "Create Stack"
1. When the stack creation is complete, click on the <b>Outputs</b> tab to view information that you will use during rest of the workshop. Keep it handy.

### For Non-AWS Event

1. Log into AWS account with your credentials. 
1. Launch the stack. <a href="https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=dbt-workshop&templateURL=https://tpch-sample-data.s3.amazonaws.com/create-dbtworkshop-infr" />Click Here</a>
1. Click `Next` till the end and then select acknowledgement checkbox. Then click "Create Stack"
1. When the stack creation is complete, click on the <b>Outputs</b> tab to view information that you will use during rest of the workshop. Keep it handy.


## Setup External Schema

In this video, we are going to walk you through creating an external schema in your Redshift Cluster.

<script src="https://fast.wistia.com/embed/medias/x07ogykj87.jsonp" async></script><script src="https://fast.wistia.com/assets/external/E-v1.js" async></script><div class="wistia_responsive_padding" style="padding:71.43% 0 0 0;position:relative;"><div class="wistia_responsive_wrapper" style="height:100%;left:0;position:absolute;top:0;width:100%;"><div class="wistia_embed wistia_async_x07ogykj87 videoFoam=true" style="height:100%;position:relative;width:100%"><div class="wistia_swatch" style="height:100%;left:0;opacity:0;overflow:hidden;position:absolute;top:0;transition:opacity 200ms;width:100%;"><img src="https://fast.wistia.com/embed/medias/x07ogykj87/swatch" style="filter:blur(5px);height:100%;object-fit:contain;width:100%;" alt="" aria-hidden="true" onload="this.parentNode.style.opacity=1;" /></div></div></div></div>

1. Copy down your output from your CloudFormation stack creation 
2. Type in Redshift to the search bar on the top and click on `Amazon Redshift`
3. Confirm that your new Redshift Cluster is listed under Cluster overview. 
4. Click on Query Editor from the lefthand sidebar 
5. Connect to your Redshift cluster. 
6. Paste in this create statement:

```sql 
create external schema tpch_s3_data
from data catalog
database 'dbtworkshop'
iam_role '<iam_role>'
create external database if not exists;
```

7. Run the query and you should then have successfully created your external schema. 




