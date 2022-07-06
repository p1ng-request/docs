---
description: What you need to know to keep your Naas experience clean and safe.
---

# Best Practices

As we "eat our own dog food" using Naas for our personal and business use cases, we have found a set of practices that help to keep the Naas working on any kind of your use cases!

It prevents the "bad habits" people have in their notebook usage and emphasis a human-centric approach, where everything is as detailed as possible in written language, and as abstracted as possible.

### The Naas template framework.

**→ Common  metadata on the notebook**

* Title: "Tool - Action of the notebook"
* Description: a one-liner explaining the benefits of the notebooks for the user
* Tags: hashtags of the topics the notebook is about

**→ A repeatable structure. And if the functions can be packaged then create** [**a python wrapper on top.**](../drivers/)****

* Input: list of all the variables, credentials, that needs to be setup
* Model: list the functions applied to the data
* Output: list the assets to be used by the user and its distribution channels if any.\


### Storage&#x20;

When it's necessary (big amount of structured data to handle) we use are using parquet file + [https://duckdb.org/](https://duckdb.org/) to query the dataset used in our data products.

What's nice with that solution is that if at any time your dataset is becoming too big, then you can switch to storing everything in AWS S3 and then querying your parquets files with AWS Athena for example.

This project from AWS makes it easy to deal with S3 + Parquet + SQL query [https://github.com/awslabs/aws-data-wrangler](https://github.com/awslabs/aws-data-wrangler)



### Others

* Don't use emoji, space, or weird characters this will lead to errors just for a name, do you really what to find that the name \`$t0️⃣ck of W/-\ll $street.csv\` was causing your bug after 10 hours?
* Don't create your own scheduler within the scheduler, like schedule every minute a script to choose which action to do. It will create a ton of output file, max you file storage very fast and debug with be a crazy hell!
* Don't put password or sensitive information in your notebook, for many reason this is not the rigth place to store them,  use our secret system instead, it store them encoded on your machine, not perfect but much better ! &#x20;
