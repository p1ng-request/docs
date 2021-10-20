# FAQ

### The basics​ <a href="the-basics" id="the-basics"></a>

#### **What is Naas?** <a href="what-is-naas" id="what-is-naas"></a>

\
Naas stands for "Notebook as automated service" is an open-source product developed by CashStory SAS. It allows anybody to write and execute arbitrary Python code through the browser, and is especially well suited to machine learning, data science and automation projects.\
​\
Naas is a hosted Jupyter notebook service that requires no setup to use and it is an alternative to Google Colab.

#### **What is the difference between Colab and Naas?** <a href="what-is-the-difference-between-colab-and-naas" id="what-is-the-difference-between-colab-and-naas"></a>

The main difference between Naas compared to Google Colab is the notebooks scheduling.

Then comes the computing power you can access (dedicated vCPU + GPU on demand in Naas vs mutualized GPU on Colab)

Naas also enables the users to follow closely their consumption of computing power and cloud resources throught detailed reports.\
\


### Using Naas <a href="using-naas" id="using-naas"></a>

#### **What is the difference between Jupyter and Naas?** <a href="what-is-the-difference-between-jupyter-and-naas" id="what-is-the-difference-between-jupyter-and-naas"></a>

​\
[Jupyter](https://jupyter.org) is the open-source project on which Naas is based. Naas allows you to use and share Jupyter notebooks with others without having to download, install or run anything.

Naas adds micro-services (features) to Jupyter notebooks/Lab instances such as :

* Scheduling
* Assets sharing
* Webhooks
* Notifications
* Secrets keys

​\
Naas facilitates Python scripting with low-code drivers. A Python library called [Naas drivers](https://pypi.org/project/naas-drivers/) is accessible on Pypi.org

Naas enables anyone with no or little knowledge of Python to start data projects with templates. The templates library is called [Naas awesome-notebooks](https://github.com/jupyter-naas/awesome-notebooks), fully open-source and accessible on Github.\
\


### Resource limits <a href="resource-limits" id="resource-limits"></a>

#### **Is it really free to use?** <a href="is-it-really-free-to-use" id="is-it-really-free-to-use"></a>

Yes. Naas Free Plan gives to all users 100 credits per month (equivalent to 3h20 of notebooks uptime).

#### **How does the credit system works?** <a href="how-does-the-credit-system-works" id="how-does-the-credit-system-works"></a>

Naas resources are not unlimited. It is important for Naas core team to provide resources for free to try the product or give access to hobbyists willing to use the service.

Nevertheless, when the computing power required goes above 3h20 per month Naas offers [credit plans](https://www.naas.ai/pricing).\
​

#### **How I can use my credits ?** <a href="how-i-can-use-my-credits" id="how-i-can-use-my-credits"></a>

Naas gives you access to services divided in 3 categories : ​

* **Notebook uptime**: time spent on "open" Notebooks (notebooks connected to a kernel)
* **Scheduler runtime**: time a scheduler spends to run your notebook when you are not around.
* **Asset sharing**: when you expose an asset to the public, a credit is debited every time some calls/hits it.
* **Webhook/API calls**: when you plug a webhook to third-party service that will then be updating your Naas notebooks.
* **Notifications**: number of messages sent by recipient.

To estimate your Naas credit consumption go to our [🥤 Naas Credits estimator](https://docs.google.com/spreadsheets/d/1k3a6J4ECUQuwRmNgKbGKBdmzb0hx4t2GuL3qQ1CICXE/edit#gid=0) spreadsheet.

#### **If I let my Notebook open, will I use my credits?** <a href="if-i-let-my-notebook-open-will-i-use-my-credits" id="if-i-let-my-notebook-open-will-i-use-my-credits"></a>

​\
No, if your Notebook is inactive for more than **15 minutes**, we will shut it down for you and you will not use more credits.

#### **How can I check how many credits I have?** <a href="how-can-i-check-how-many-credits-i-have" id="how-can-i-check-how-many-credits-i-have"></a>

​\
If you have been using Naas during the current month, you will receive every day an email that sums up your actions, your credit consumption, and your remaining balance.

You will also access files in an attachment that will go into the details.\
​\
​

#### **What will happen when I will be out of credits ?** <a href="what-will-happen-when-i-will-be-out-of-credits" id="what-will-happen-when-i-will-be-out-of-credits"></a>

We will warm you when you will reach 80% of your credits. Then, when out of credits, your actions will be saved but frozen.\
​\
To launch them, you will have to get more credits.\
​

#### **How I can get more credits ?** <a href="how-i-can-get-more-credits" id="how-i-can-get-more-credits"></a>

Go on [https://www.naas.ai/pricing](https://www.naas.ai/pricing) and choose the plan that better fits you. Do not hesitate to contact us if you need assistance :\
​

* Email: [hello@naas.ai](mailto:hello@naas.ai)
* Call :+ 33 7 67 64 05 68

​

### Additional questions <a href="additional-questions" id="additional-questions"></a>

#### **What browsers are supported?** <a href="what-browsers-are-supported" id="what-browsers-are-supported"></a>

Naas works with most major browsers, and is most thoroughly tested with the latest versions of Chrome, Firefox and Safari.

#### **What about other programming languages?** <a href="what-about-other-programming-languages" id="what-about-other-programming-languages"></a>

Naas focuses on supporting Python and its ecosystem of third-party tools. We're aware that users are interested in support for other Jupyter kernels (e.g. R or Scala). We would like to support these in the future. Please send us an email to [hello@naas.ai](mailto:hello@naas.ai) if you have such needs.

#### **I found a bug or have a question; who do I contact?** <a href="i-found-a-bug-or-have-a-question-who-do-i-contact" id="i-found-a-bug-or-have-a-question-who-do-i-contact"></a>

Open any Naas notebook. Then open a notebook and run a cell with 'naas.open\_help()'.

#### **I am interested in Naas but I don't know how to use Notebooks !** <a href="i-am-interested-in-naas-but-i-dont-know-how-to-use-notebooks" id="i-am-interested-in-naas-but-i-dont-know-how-to-use-notebooks"></a>

​\
No problem! We created a training program adapted to your level and your goals. We will tackle your data project, you can book a time slot to talk about it just [book a meeting](https://calendly.com/valentin-piquard/rendez-vous-15-minutes-en)\
​

#### **Can Naas be used in a company ?** <a href="can-naas-be-used-in-a-company" id="can-naas-be-used-in-a-company"></a>

​\
Of course! Notebooks can become your best ally to start AI or launch an ambitious data-driven strategy.\
​\
Netflix is using Notebooks for their analytics check out our video on [Netflix scheduling Jupyter notebooks](https://www.youtube.com/watch?v=JF10Ey-O1HU\&t=2102s)
