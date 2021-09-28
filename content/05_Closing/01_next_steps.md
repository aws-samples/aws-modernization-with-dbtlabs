---
title: "Next Steps"
chapter: true
weight: 1
---

<script src="https://fast.wistia.com/embed/medias/g2ix6gwksh.jsonp" async></script><script src="https://fast.wistia.com/assets/external/E-v1.js" async></script><div class="wistia_responsive_padding" style="padding:61.04% 0 0 0;position:relative;"><div class="wistia_responsive_wrapper" style="height:100%;left:0;position:absolute;top:0;width:100%;"><div class="wistia_embed wistia_async_g2ix6gwksh videoFoam=true" style="height:100%;position:relative;width:100%"><div class="wistia_swatch" style="height:100%;left:0;opacity:0;overflow:hidden;position:absolute;top:0;transition:opacity 200ms;width:100%;"><img src="https://fast.wistia.com/embed/medias/g2ix6gwksh/swatch" style="filter:blur(5px);height:100%;object-fit:contain;width:100%;" alt="" aria-hidden="true" onload="this.parentNode.style.opacity=1;" /></div></div></div></div>

Thank you for joining us for this AWS Dev Day Workshop with dbt. We hope you 
learned a lot!

If you're interested in learning more about dbt, we recommend these resources:

- [dbt Fundamentals course](https://courses.getdbt.com/collections)
- [Join 15,000+ data professionals in our Slack community](https://community.getdbt.com/)
- [Contact our Team for more information about dbt at your org](https://www.getdbt.com/contact/)
- [Join us at our Coalesce Conference](https://coalesce.getdbt.com/)


## Workshop cleanup

### AWS

In terms of cleaning up the Redshift and S3 bucket, here are the steps to spinning down the setup.

1. Delete the S3 buckets created by CloudFormation. To do this, you will have to first empty the S3 bucket and then delete them. 
2. After removing the S3 buckets, go back to CloudFormation and delete the stack. This will delete the Redshift cluster from your account as well as any IAM roles created for the workshop. 


### dbt 

The dbt Cloud account will lock up after 2 weeks. If you need additional time for the workshop, contact the #learn-aws-dev-day slack channel for an extension. You may also connect support via the chat icon on the top right.

If you wish to use the account for your own dbt projects, sign up for a plan. In terms of the Github repository, it is yours as it is on your personal/organization's account. You can either [delete it](https://docs.github.com/en/github/administering-a-repository/managing-repository-settings/deleting-a-repository) or you can use it as an guide for your own dbt project.



