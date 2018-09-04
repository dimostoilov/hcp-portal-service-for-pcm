
# Welcome to SAP Cloud Platform, Portal Service - Partner Channel Management Configuration Guide


The SAP Cloud Platform, portal service for Partner Channel Management configuration guide provides all you need to deploy a PCM solution on your SCP account and connect it to your SAP Cloud for Customer (C4C) tenant and Identity Authentication tenant.

## How to Deploy the Partner Channel Management Solution
This guide will show you how to download the partner channel management solution from the SAP SCP, portal service GitHub repository and deploy it to your account.

The Partner Channel Management solution includes several components:

*  pcmapps - an HTML5 application containing UI5 Components corresponding to C4C Business Objects such as Lead, Opportunity, Task etc. There are 3 types of applications: List, Object Details, and Create New Object.
*  pcmcpapps - an HTML5 application containing the following UI5 Applications: Self-Registration, Invitation, Registration and Status.
*  pcmsitetemplate - an HTML5 application containing a Site Template for creating a new Partner Channel Management site.
*  SAPID Mail Templates.zip -  a sample mail template for emails that will be sent after Self-Registration and Invitation.

##  1. Prerequisites

*	SAP Cloud Platform (SCP) productive account (the solution does not work with a trial account)
*	Portal Service enabled from the SCP account cockpit, Services tab
*	Identity Authentication tenant
*	SAP Cloud for Customer (C4C) tenant
*	In C4C, Partner Program Management project scope is enabled. For more information [read this blog](https://blogs.sap.com/2015/09/26/cloud-for-customer-specific-configurations-for-partner-channel-management/)
*	In C4C, Deal Registration is also selected if needed.
*	In C4C,	maintain the Business Roles in the Business Configuration
*	Users:
     -  Admin access to an SCP account
	 -  TENANT_ADMIN user for Portal Service
     -  C4C admin user
     -  Identity Authentication admin user

## 2. Configure Your Account

### 2.1 	Deploy PCM artifacts
 1. Navigate to	[ https://github.com/SAP/hcp-portal-service-for-pcm/releases](https://github.com/SAP/hcp-portal-service-for-pcm/releases)
 2. Prepare content for deployment. There are two options:  
     a. Download ZIP files from the Releases folder.  
     b. Clone and Create a Zip file:  
         1.  	Clone the repository to your computer, or download it as a ZIP file by clicking the Clone or download button and selecting Download ZIP, and extract its contents.  
         2. 	Archive every folder content to ZIP files (pcmapps, pcmcpapps, pcmsitetemplate).

 3. Import the following ZIP files to your SCP account:
    * pcmapps.zip	(Business applications)
    * pcmcpapps.zip	(Invitation application)
    * pcmsitetemplate.zip	(Site template).

   You can import the files to SAP Web IDE and then deploy them to SCP, or you can directly deploy them to SCP through the SCP cockpit (Applications >>HTML5 Applications >> Import from File.  
   If the applications were deployed through SCP cockpit, they should be activated by clicking the link in the app's name, clicking on 'Versioning' in the left menu, 'Versions' under History section, and then on the activation icon in the 'Actions' column.  
 4. (Optional, if you imported the pcm applications via SAP Web IDE)
 	Preview your site template in SAP WEB-IDE:
	a. Open SAP Web IDE and right click on the 'pcmsitetemplates project'.  
	b. Choose Run -> Run as -> Preview Site Template.  


### 2.2 Create PCM roles
   1. Open the SAP SCP account cockpit and navigate to Services >> Portal Service >> Configure Portal Service >> Roles.
   2. Create the following new roles:
       * PartnerManager
       * PartnerContact
       * Applicant
       * Candidate


###  2.3 Create an email template in the Identity Authentication Service (IAS)
   The email template for the PCM invitation flow includes a SAP logo as well as pre-defined text. You may update the email template used by the IAS to send invitations to users according to your needs.
   
   1.	Download SAPID Mail Templates.zip from [ https://github.com/SAP/hcp-portal-service-for-pcm/releases](https://github.com/SAP/hcp-portal-service-for-pcm/releases)
   2.	Adjust the template according to your needs.
   3.  Add the template to the Identity Authentication IDP account. For more details:  https://help.sap.com/viewer/6d6d63354d1242d185ab4830fc04feb1/Cloud/en-US/3c4f39763f3c4d659a43e1c33c94b95e.html
   4.	Define the uploaded mail template to your application. For more details:       https://help.sap.com/viewer/6d6d63354d1242d185ab4830fc04feb1/Cloud/en-US/bb2c79b71f8d47ec877882d78e0ceb39.html

#### 2.3.1 Set up Privacy policy in IAS
To adhere to the EU General Data Protection Regulation (GDPR), after an 
invitee has accepted the mail invitation (by pressing the account activation button), as part of the activation process users should read a privacy policy document and consent to it.
For this purpose you as the Partner Manager should configure the privacy policy document in IAS as follows:
   1. Create a privacy policy document and add it to IAS. For more details:
 https://help.sap.com/viewer/6d6d63354d1242d185ab4830fc04feb1/Cloud/en-US/e73cf2dc28fa40c09dd4ad294c23ee5f.html
   2. Define the privacy policy for your application. For more details:
 https://help.sap.com/viewer/6d6d63354d1242d185ab4830fc04feb1/Cloud/en-US/96111183bf734776bfbec21f3d5f5a5a.html 

Please note that if you have defined a new privacy policy document for your application, all users that have already consented to the old privacy policy will now have to consent to the new updated policy on login to the application.


### 2.4	Trigger an Automated Integration Between SAP Cloud for Customer and SAP Cloud Platform

Follow the [Onboarding Guide](https://uacp2.hana.ondemand.com/viewer/462e41a242984577acc28eae130855ad/Cloud/en-US) and make sure you triggered [automated integration between SAP Cloud for Customer and SAP Cloud Platform](https://help.sap.com/viewer/462e41a242984577acc28eae130855ad/Cloud/en-US/9dcbeda8fcbf436e956496721d4f0efe.html). It will set up a trust between the customer account and IAS (for log-on scenario).

  In Cloud Platform, portal, under Roles, assign the user to the TENANT_ADMIN role.
  You should now be able to log on to the portal service’s Admin Space with the user ID
  (email) that was assigned to it when the customer account was provisioned to the portal service.
  If the user cannot log in, make sure that the user was added to the Identity Authentication account (go to the Identity Authentication admin page and create the user via the User Management page or upload the user with his/her full details in a CSV file format. To see the required details, you can export a user to a CSV file and edit the file).
  

#### 2.5	Set up trust between the customer account and IAS API (for SAP ID invitation flow)
   1. Open the admin page of your Identity Authentication IDP account.
   2. Click Applications.
   3. Choose your application (created in step 3 in section 2.4.2)
   4. Go to 'HTTP Basic Authentication' under 'API Authentication' section
   5. Enter a password and confirm it (save it for future use)
   6. Click on 'Save' button
   7. Enter the page and copy the user ID that was generated by IAS (save it as well for future use)

#### 2.6	Set up trust between the customer account and SAP C4C backend (for C4C invitation flow)

As part of the [onboarding guide](https://uacp2.hana.ondemand.com/viewer/462e41a242984577acc28eae130855ad/Cloud/en-US) make sure you [configured OAuth Client for OData Access](https://help.sap.com/viewer/462e41a242984577acc28eae130855ad/Cloud/en-US/0ac0dc9b3f3e4a07ba64cbac74a23327.html) 

#### 2.7	Upload destinations to customer SCP account

As part of the [onboarding guide](https://uacp2.hana.ondemand.com/viewer/462e41a242984577acc28eae130855ad/Cloud/en-US) make sure you [created OAuth2SAMLBearerAssertion destination](https://help.sap.com/viewer/462e41a242984577acc28eae130855ad/Cloud/en-US/929294823bc44614ba2034662f043793.html). Set its "Name" property to "C4C". This is an OAuth C4C destination used for connecting to the SAP C4C backend during partner flow.

Additionally create the following destinations:

##### 2.7.1	SAPID Destination  
Destination used for the invitation flow with IAS.  
  + Name = sapid
  + Type = HTTP
  + Description = (enter a description)
  + URL = (enter the URL to your IAS, https://<your Identity Authentication account name>.<accounts>.ondemand.com/)
  + ProxyType = Internet
  +	Authentication = BasicAuthentication
  + User = (enter the user ID from section 2.5 above)
  + Password = (enter the password from section 2.5 above)
  
  Additional property:
  Properties are added by clicking on "New Property" button  
  +	TrustAll = true (add this manually. Note that 'TrustAll' is the key and 'true' is its value.)


##### 2.7.3	C4C__Public Destination  
Public C4C destination (used for connecting to the C4C backend during a guest registration scenario) with the parameters in the next section.  
+ Name = C4C__public (double underscore)
+ Type = HTTP
+ Description = (enter description)
+ URL = …/sap/byd/odata/v1/pcmportal (this relative path should come after the full URL to C4C tenant, E.g. https://myXXXXXX.crm.ondemand.com/sap/byd/odata/v1/pcmportal)
+ ProxyType=Internet
+ Authentication = BasicAuthentication
+ User = (admin user of the C4C tenant)
+ Password=<admin user password> (admin password of the C4C tenant)  
Additional properties:  
+ authnContextClassRef = urn:oasis:names:tc:SAML:2.0:ac:classes:PreviousSession (add this manually)
+ nameIdFormat = urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress (add this manually)
+ scope = UIWC:CC_HOME (add this manually)

#### 2.8	Configure SAP C4C Backend

##### 2.8.1	Purpose
This section describes how to create a Callback from the CRM that is used in the PCM scenario, to the Portal Service account.

The configuration is mandatory for enabling the entire self-registration scenario, including the transition between roles: Applicant -> Candidate -> Partner Manager.

Note that the Callback is configured on the CRM per SCP system, which means that only one SCP account can be configured.


##### 2.8.2	Instructions
   1.	Enter the C4C PCM CRM, for example: https://my312033.crm.ondemand.com, as an administrator.
   2.	Click the Administration tab and choose General Settings.
   3.	Click on Communication Systems under the 'Integration' section.
   4.	Create a new system with the following details:
            1. ID = PCM_PORTAL
            2. Host Name = [portal java application's name: cloudnwcportal or cloudsandboxportal]-[SCP account name].[data center, E.g. eu1, us1].hana.ondemand.com/, E.g. cloudnwcportal-aab4aef77.eu1.hana.ondemand.com/
            3. System Access Type = Internet
   5. Save the settings.
   6. Set Actions to Active.
   7. Click on Communication Arrangement.
   8. Click on New, and then do the following:
      1. Select Scenario: Choose the Channel Partner Registration Portal Callback option and click Next.
      2. Define Business Data: Choose the communication system you created in step 4, and click Next.
      3. Define Technical Data:
         1. Communication Method = Direct Connection.
         2. Application Protocol = Http.
         3. Authentication Method = User ID and Password.
         4. Click the Edit Credentials button and set the details (email address) of the TENANT_ADMIN user you have on SCP for the User ID (the user can be found in SCP - Services - Portal Service - Configure Portal Service - Roles). Please note that if, for some reason, the TENANT_ADMIN user is locked, the callback will fail.
      4. Review: Review and verify the accuracy of the data you filled in, then click on Finish and then Confirm
   9.	In the Communication Arrangement, click the entry of the new arrangement, then click Edit.
   10.	Switch to the Technical Data tab.
   11.	Click the Edit Advanced Settings button.
   12.	Make sure that the port is 443 and in the Path field add: portal/v1/services/invitations/continue_flow/
   13.	Click Save.

## 3. Create & Configure the PCM Site
1.	In the SCP cockpit, go to Services – Portal Service, and from there click on Go to Service. This opens the Site Directory of your portal service.
2.	Go to 'Site Directory' from the left menu and click on “+” to create a new site. Select the Partner Portal site template and click Create.
3.	(Optional) Set site alias:
    + Go to site settings.
    + Click Edit and set site alias.
    + Click Save.
4. Data Retention Policy:
The personal contact details of all invitees who ignore the invitation, or do not accept the privacy terms in the registration form, will be deleted from the contacts table after the number of retention days that are specified in the site’s settings.

 **How to specify the number of retention days?**
   + Go to Site Settings.
   + Click Edit.
   + Under Custom Site Properties, set the key "data_retention_days" with an integer value that represents the number of days.
   + Click Save.

**Note:** If the number of retention days is not specified, all personal contact details of pending invitees will be deleted after 90 days (default).

5.	Publish the site by clicking on the Publish button in the site header. This makes the site available for all users.
6.	The URL of the published site will be used later on for the registration of new applicants and future actions. 
7.	There are two URLs related to your site:  
 **I.** Public URL to start the registration flow:
https://flpnwc-[account name].dispatcher.[data center].hana.ondemand.com/sites/[site alias]#Home-show
**II.** Authenticated URL. Data from C4C is available for Partner Managers:
https://flpnwc-[account name].dispatcher.[data center].hana.ondemand.com/sites/[site alias]?hc_login#Shell-home
  
**Note:** Please do not assign users directly to Partner Manager role in SCP . The assignment to this role is done automatically by the callback batch job in C4C, which runs every night in the background, after the user's application form is approved.

### Rebranding

| Question | More Information |
| -------- | ---------------- |
| **How do I change the company logo or background of the support site?** | 1.	Go to the Home page. <br>2.	On the left, click ![services](/resources/ss3.png) to open Services and Tools. <br>3.	In the UI Theme Designer, click Configure.<br>4.	In order to change a logo, create a new theme as follows: <ul><li>a.	Click Create a New Theme.</li><li>b.	Follow the steps of the wizard and click Create Theme.</li><li>c.	On the right of the screen, select ![edit](/resources/ss4.png)  (quick editing mode) and upload the company logo.</li><li>d.	From the Theme tab at the top left, select Export to create a zip file containing the new theme you created with the logo. For more information, see Exporting Themes.</li></ul>5.	Now go to the Theme Manager (also in Services and Tools) and click Configure. <br>6.	Browse for and upload the zip file with the updated theme that includes your logo. <br>7.	Click Assign to Site.|


## 4.	SAP C4C Documentation


[https://cp.hana.ondemand.com/dps/d/preview/0cec219614e94fd3bdd0f0561e9b70e0/1511/en-US/frameset.htm?b7027a7e846f4cbf9391d6a475c24ce5.html ](https://cp.hana.ondemand.com/dps/d/preview/0cec219614e94fd3bdd0f0561e9b70e0/1511/en-US/frameset.htm?b7027a7e846f4cbf9391d6a475c24ce5.html )


## Disclaimer
Any software coding and/or code snippets are examples. They are not for productive use. The example code is only intended to better explain and visualize the syntax and phrasing rules. SAP does not warrant the correctness and completeness of the example code. SAP shall not be liable for errors or damages caused by the use of example code unless damages have been caused by SAP's gross negligence or wilful misconduct.
