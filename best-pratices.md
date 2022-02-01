# Best Practices

After few months of using our own product and with the help of all of you we have found a set of practices that help to keep the Naas working your use cases!

Use Mainly Naas as ETL :

{% embed url="https://en.wikipedia.org/wiki/Extract,_transform,_load" %}

Not a crypto miner or any other Fancy idea, it will work as his best when :

Create a folder in your Naas by project, ideally, in this project, you should find:

* **Input** folder where you put every file you use as dependency to your notebook.
* **Output** folder **** where you save all results of your notebook, intermediary or final
* **Script** folder where you put your notebooks, all with a clear name of what they do.
* **deploy.ipynb** who is there to list and send all your sandbox files in production, it will prevent you to send your work in production by restarting a kernel!

Use **real Database** for storing purposes, CSVs are great but please use it as debug, not for storing every move from excel loses all its meaning!&#x20;

To do so, use our Mongo connector and a **free instance** from Mongo Atlas, you have **512MB** a good point to start  :

{% embed url="https://www.mongodb.com/pricing" %}





* Don't use emoji, space, or weird characters this will lead to errors just for a name, do you really what to find that the name \`$t0️⃣ck of W/-\ll $street.csv\` was causing your bug after 10 hours?
* Don't create your own scheduler within the scheduler, like schedule every minute a script to choose which action to do. It will create a ton of output file, max you file storage very fast and debug with be a crazy hell!
* Don't put password or sensitive information in your notebook, for many reason this is not the rigth place to store them,  use our secret system instead, it store them encoded on your machine, not perfect but much better ! &#x20;
