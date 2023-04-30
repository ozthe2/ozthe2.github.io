---
layout: post
title:  "ConfigMgr: How to create a collection to include only active or inactive computers"
date:   2013-10-03 22:00:00 +0000
categories: ConfigMgr
tags: [configmgr, query, collection]
---

If you would like to create a SCCM computer collection that includes only active, or only inactive computers then you will want to read this step-by-step guide.

I couldn’t find anywhere on the Internet that showed how to do this, so here’s how I created a collection of all of our ‘Active’  computers:

### 1.
Under Assets and Compliance -> Device Collections, create a new device collection.

![1-4](/assets/images/1-4.PNG)

### 2.
On the ‘General’ tab, fill in the name of the collection, a comment if you are feeling funky and set the limiting collection that you want this query to be, well, limited to.  In this example,  I limited the query to the ‘All Systems’ collection.

![2-3](/assets/images/2-3.PNG)

### 3.
On the membership rules I chose to use incremental updates so that I had a more accurate collection.  The best practice is to limit your use of incremental updates but it can be implemented on something like 200 collections.

See this link here for more details on best practices for collections: [http://technet.microsoft.com/en-us/library/gg699372.aspx](http://technet.microsoft.com/en-us/library/gg699372.aspx)

Click the ‘Add Rule’ button and select ‘Query Rule’ from the drop-down menu.

![3-3](/assets/images/3-3.PNG)

### 4.
Give the query rule a meaningful name and then click on the ‘Edit Query Statement’ button.

![4-3](/assets/images/4-3.PNG)

### 5.
Select the ‘Criteria’ tab and click on the little goldy-yellowy-starry sun type button.

![5-3](/assets/images/5-3.PNG)

### 6.
On the ‘Criterion Properties’ box, leave the criterion type as ‘Simple Value’ and click the ‘Select’ button.

![6-2](/assets/images/6-2.PNG)

### 7.
On the ‘Select Attribute’ box, select ‘Client Status’ for the Attribute class and then select, ‘Client Activity’ for the Attribute.

![7-2](/assets/images/7-2.PNG)

### 8.
**To query Active computers:**
On the ‘Criterion Properties’ box, ensure that the ‘Operator’ is set to: ‘*is equal to*’ and the value is set to: *1*  

**To query Inactive computers:**
On the ‘Criterion Properties’ box, ensure that the ‘Operator’ is set to: ‘*is equal to*’ and the value is set to: *1*  

In this example, I am creating a query for active computers, so I will use the value of 1 as per my screenshot below:

![8-2](/assets/images/8-2.PNG)

### 9.
Click the OK buttons (three times) and you will be back at the ”Create Device Collection Wizard’ box with your newly created query proudly on display.

![9-2](/assets/images/9-2.PNG)

### 10.
Click the Next button, then click Next again at the Summary screen and you should be presented with a successful outcome.

![10-2](/assets/images/10-2.PNG)

### 11.
Click the close button and you’re done!

---

**Get my books:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)