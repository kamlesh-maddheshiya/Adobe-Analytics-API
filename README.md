<!-- Output copied to clipboard! -->

<!-- You have some errors, warnings, or alerts. If you are using reckless mode, turn it off to see inline alerts.
* ERRORs: 0
* WARNINGs: 0
* ALERTS: 28 -->

**Table of Contents**


[TOC]


<h1>**What is Adobe Analytics API **</h1>


Adobe Analytics APIs allow you to directly call Adobe's servers to perform almost any action that you can perform in the user interface. You can create reports to explore, get insights, or answer important questions about your data. You can also manage components of Adobe Analytics, such as the creation of segments or calculated metrics. 

<h2>**Getting started with the Analytics API**</h2>


There are several steps to take before using the Analytics APIs.



1. **Permissions: **

    Configure permissions for the developer in the Adobe Admin Console ([https://adminconsole.adobe.com](https://adminconsole.adobe.com/9FA32981641059C00A495FE1@AdobeOrg/overview)).

2. **API Client**: 

    Create an API client in the Adobe Developer Console ([https://developer.adobe.com/console/](https://developer.adobe.com/console/)).

3. **Authentication**: 

    Obtain the necessary credentials to send data to Adobe. Adobe offers two primary methods to authenticate:

1. **OAuth**: Use your own account to authenticate with the API. 
2. **JWT**: Use a service account to authenticate with the API. 
3. What’s needed
1. **<code>api_key</code> </strong>– this is a key that is available once you create an Adobe I/O OAuth client in the Adobe I/O console. For details, see [https://experienceleague.adobe.com/docs/analytics-learn/tutorials/apis/using-postman-to-make-adobe-analytics-2-0-api-requests.html?lang=en](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/apis/using-postman-to-make-adobe-analytics-2-0-api-requests.html?lang=en) .
2. <strong><code>company_id</code> </strong>– you can get this from the [Swagger interface](https://adobedocs.github.io/analytics-2.0-apis/) ([https://adobedocs.github.io/analytics-2.0-apis/](https://adobedocs.github.io/analytics-2.0-apis/)) for the Adobe Analytics API. Jen explains how to do that starting at the 1:37 mark in [the same video referenced above](https://helpx.adobe.com/analytics/kt/using/postman-analytics-api2-requests-technical-video-use.html).
3. <strong><code>aa_rsid</code> </strong>– this is just the report suite ID. You can grab this from your website or the plain ol’ Adobe Analytics Admin Console (no fancy Adobe I/O stuff needed for this).
4. <strong><code>aa_token</code></strong> – this comes from the Analysis Workspace debugger tool. Details on how to enable that are available in [Adobe’s documentation](https://github.com/AdobeDocs/analytics-2.0-apis/blob/master/reporting-tricks.md) ([https://github.com/AdobeDocs/analytics-2.0-apis/blob/master/reporting-tricks.md](https://github.com/AdobeDocs/analytics-2.0-apis/blob/master/reporting-tricks.md)). Follow steps 1 through 6 and then grab the <em>Authorization:</em> value from the <em>CURL REQUEST</em> section of any request you inspect with the little bug icon. This token will expire periodically and will have to be updated in the code. 

<h1><strong>Steps to create Adobe Analytics API</strong></h1>


<h2>**1**: Login  to Adobe I/O.</h2>


([https://developer.adobe.com/console/home](https://developer.adobe.com/console/home)) make sure you have Admin and Developer Access with Web Services. If not, get the access from your administrator.

<h2>**2:** Click, ‘Create a new Project’ under Home Quick Start.</h2>



![alt_text](images/image1.png "image_tooltip")


<h2>**3:** Click ‘Add API’** **on the Project Screen 1.</h2>



![alt_text](images/image2.png "image_tooltip")


<h2>**4:** Select Adobe Analytics from the list.</h2>



![alt_text](images/image3.png "image_tooltip")


<h2>**5:** Select User Authentication **OAuth **on ‘Configure API’ Screen. </h2>


Service Account (JWT) is also a method to integrate, but this post covers **OAuth** only.


![alt_text](images/image4.png "image_tooltip")


<h2>**6:** Select Web Auth2.0** **on ‘OAuth 2.0 authentication</h2>


And authorization’ screen. Input the Default Redirect URL, Redirect URL pattern and save the configuration.



* Default Redirect URL : [https://www.adobe.com](https://www.adobe.com/)
* Redirect URL Pattern : [https://www\.adobe\.com](https://www/.adobe/.com)


![alt_text](images/image5.png "image_tooltip")


<h2>**7:** Edit the Project</h2>


Once saved, you should see the project under ‘Projects’ Tab. Edit the project and give a Proper Name for your identification (Screen grab 01). Copy _Client ID_ and_ Client Secret _from the OAuth Web (Screen grab 02). The two values (_Client ID_ & _Client Secret_) will be used in the upcoming steps.


![alt_text](images/image6.png "image_tooltip")



![alt_text](images/image7.png "image_tooltip")


<h2>**8: **Open one more tab and login to [Swagger UI](https://adobedocs.github.io/analytics-2.0-apis/). </h2>


([https://adobedocs.github.io/analytics-2.0-apis/](https://adobedocs.github.io/analytics-2.0-apis/))

<h2>**9:** Navigate to ‘Users Tab’ and click on **GET** /users/me.</h2>



![alt_text](images/image8.png "image_tooltip")


<h2>**10:** Click **Try Out** and **Execute**. </h2>


Copy the _Company ID** **_from the Request URL (See below screen grab for reference – Yellow Highlighted). The value (_Company ID_) will be used in the upcoming steps.


![alt_text](images/image9.png "image_tooltip")


<h2>**11: **Open Postman and Login </h2>


(If Postman is outdated, please update and then login).

<h2>**12: **Create a new ‘Request (GET)’ and add the Request Name. </h2>


For this exercise, have added the Request Name as ‘Adobe Analytics Blog’.


![alt_text](images/image10.png "image_tooltip")


<h2>**13:** Click on the Request created</h2>


And change the method to ‘**POST**‘ and add the URL to the ‘POST’.

POST URL : https://analytics.adobe.io/api/_Company ID_/reports

The _Company ID_ in the above URL is from Step 11.


![alt_text](images/image11.png "image_tooltip")


<h2>**14: **Click on ‘Authorization Tab’ under the ‘POST’ URL</h2>


and select OAuth2.0 from the drop down Type. Click ‘Get New Access Token’.


![alt_text](images/image12.png "image_tooltip")


<h2>**15:** Input the below values to the ‘Get New Access Token’ pop-up</h2>


and request for a token.



* Token Name : Adobe Analytics 2.0
* Grant Type : Authorization Code
* Callback URL : [https://www.adobe.com](https://www.adobe.com/) (Don’t enable Authorize using browser)
* Auth URL: [https://ims-na1.adobelogin.com/ims/authorize/v1](https://ims-na1.adobelogin.com/ims/authorize/v1)
* Access Token URL : [https://ims-na1.adobelogin.com/ims/token/v1](https://ims-na1.adobelogin.com/ims/token/v1)
* Client ID : _Copied from Step 08._
* Client Secret: _Retrieved and copied from Step 08._
* Scope: openid,AdobeID,read_organizations,additional_info.projectedProductContext,additional_info.job_function
* State : _Your State_
* Client Authentication : Send as Basic Auth Header


![alt_text](images/image13.png "image_tooltip")


<h2>**16: **Authenticate </h2>


Once you click ‘Request Token’, you need to authenticate using your Experience Cloud ID credentials. Once token is generated, click on ‘Use Token’ at the top right.


![alt_text](images/image14.png "image_tooltip")


<h2>**17:** Click on the ‘Headers Tab’ </h2>


and add the below Key Value pairs.

x-proxy-global-company-id : _Company ID_ copied from Step 11.

x-api-key : _Client ID_ copied from Step 08.

Content-Type : application/json


![alt_text](images/image15.png "image_tooltip")


<h2>**18: **Click on ‘Body Tab’ and select ‘raw’. </h2>


Here is where we need to add the request.


![alt_text](images/image16.png "image_tooltip")


<h2>**19:** Go to Workspace and open a new Project. </h2>


Click the ‘Help’ section inside the Workspace section (Not the Analytics section at the top) and ‘Enable Debugger’.


![alt_text](images/image17.png "image_tooltip")


<h2>**20:** click on the Free Form Table under the Oberon Icon.</h2>


The browser will force reload after the pop-up confirmation on enabling debugger. 

After reload, you should see the below ‘Oberon Icon’ on your Free Form Table. Build your Free Form and click on the Free Form Table under the Oberon Icon.


![alt_text](images/image18.png "image_tooltip")


<h2>**21:** Copy the JSON Request from the ‘Oberon XML Tab’ once opened.</h2>



![alt_text](images/image19.png "image_tooltip")


<h2>**22:** Paste the request to the Postman ‘Body Tab</h2>


’ i.e. raw (Step 19) and send the request.

<h2>**23:** You should now be able to see the response</h2>


 that should match the data you have seen in the Workspace.


![alt_text](images/image20.png "image_tooltip")


Now our Adobe Analytics API is working and also it can bring data from Adobe analytics so let's use this data into a dashboard using a business intelligence tool like Google Looker studio.

<h2>**24:** Go to Looker studio and create a new report. </h2>


[https://lookerstudio.google.com/navigation/reporting](https://lookerstudio.google.com/navigation/reporting) 


![alt_text](images/image21.png "image_tooltip")


<h2>**25:** Lets use Adobe Analytics 2.0 as a data source . </h2>


Click on Adobe Analytics 2.0


![alt_text](images/image22.png "image_tooltip")


<h2>**26:** Click on Authorise </h2>



![alt_text](images/image23.png "image_tooltip")


<h2>**27:** Click on Start to connect to Adobe Analytics 2.0</h2>



![alt_text](images/image24.png "image_tooltip")


<h2>**28:** Click on Connect with oAuth (Valid for 2 weeks only) and login</h2>



![alt_text](images/image25.png "image_tooltip")


<h2>**29:** Fill the parameter and click on ADD.</h2>



![alt_text](images/image26.png "image_tooltip")


<h2>**30:** Click on Add to report</h2>



![alt_text](images/image27.png "image_tooltip")


<h2>**31:** Select date range and dimension as a page</h2>


and occurrences as one metric.


![alt_text](images/image28.jpg "image_tooltip")


Hurray, I have now successfully created my first Adobe Analytics API 2.0 Request.
