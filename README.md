# Welcome to Simplify
## How to integrate & test


[Hosted Checkout](#Hosted-checkout)

[Direct API](#Direct-API)

[Plugins](#Plugins)

[SDKs](#Available-SDKs)

## Testing Modes

The i-bank my Store API can be accessed in Sandbox or Live modes. In Sandbox mode, all payments are simulated. In Live mode, payments are real. The API key specified in API requests determines which mode is accessed. When logged into the i-bank my Store web portal, you can switch between viewing Sandbox and Live data using the toggle switch in the header.


## Live
When used for live payments (e.g. when configured with a live API key), the hosted payment button will only work on the website that is registered in your live i-bank my Store account. 

## SandBox
Sandbox environment is comprised of virtual servers for software testing in an isolated environment that developers use to test new features. Using sandbox you cannot use 3Ds enrolled cards and plugins. Additionally, the redirect url is disabled when using a sandbox key for testing.

## Hosted Checkout 

There are two easy ways in which you can start to use hosted payments on your website. You have the option of presenting the hosted payment form as either a modal or embedding it directly on your page.

The checkout is fully hosted, compliant with updated PCI standards and requires no server-side scripting. Your first option is to add a modal with a button on your web site by adding the code given below and following the instructions.

**Simple example html file for live and sandbox enviroment (modal)**


```
<!DOCTYPE html>
<html>
<head>
    <title></title>
</head>
<body>
<script type="text/javascript"                  
src="https://uat.simplify.com/commerce/simplify.pay.js"></script>                   
<button data-sc-key="<put your Api public hosted key>"                 
data-name="Jasmine Green Tea"                   
data-description="Smooth tea with a rich jasmine bouquet"                   
data-reference="99999"                  
data-amount="3000"                  
data-color="#12B830">                   
Buy Now                 
</button>
</body>
</html>
```
Your second option is to put an embedded form in your web page by adding the second code given.

**Simple example html file for live and sandbox enviroment (embedded form)**
```
	<script type="text/javascript"
	        src="https://www.uat.simplify.com/commerce/simplify.pay.js"></script>
	<iframe name="my-hosted-form"
	        data-sc-key="<put here your Api public hosted api key>"
	        data-name="Jasmine Green Tea"
	        data-description="Smooth tea with a rich jasmine bouquet"
	        data-reference="99999"
	        data-amount="3000"
	        data-color="#12B830">
	</iframe>
```

The only difference is the "iframe" instead of "button" in a modal (in html file). In the same way, follow the instructions below.

- Copy and paste the code snippet below directly into your web page, in the location where you want the button to display (in your html file).
- Change the value of the &#39;&#39;data-sc-key&#39;&#39; attribute to your own hosted public key (live or sandbox). This public key exists on the platform Account Settings / API keys / [your hosted public key](https://ibanknbg.uat.simplify.com/commerce/docs/tools/hosted-payments#keys)(only for live mode). [(Test api keys)](https://nbgfilestorage.blob.core.windows.net/ecommerce/docs/i-Bank%20e-Simplify%20Sandbox%20Credentials.docx)
- Change the value of the &quot;data-reference&quot; attribute to your reference number for the payment.

In **sandbox** enviroment you can put the sandbox hosted public key that was provided through the developers portal and use these [test Cards](https://ibanknbg.uat.simplify.com/commerce/docs/testing/test-card-numbers).

## Troubleshooting
If hosted payments doesn't work straight away, below is a checklist that may help you get up and running.

- Use a Hosted Payment Enabled API Key: If you plan on using the form to make payments, then you need to use the right key.
- Use the Public Key: So you enabled an API Key Pair for hosted payments, but it still doesn't work. There are 2 keys, so make sure it is the public key that is used. Public keys start with sbpb_ (sandbox/test key) or lvpb_ (live key). For **sandbox** testing the [keys](https://nbgfilestorage.blob.core.windows.net/ecommerce/docs/i-Bank%20e-Simplify%20Sandbox%20Credentials.docx) are provided through the developers portal.
- Use the Correct Website: You have successfully tested your hosted payments locally and now have switched to a live key. As a security measure, hosted payments will only work on the website you registered with Simplify.com when you onboarded. See [Domain Restrictions](https://ibanknbg.uat.simplify.com/commerce/docs/tools/hosted-payments#domain).

### Handling responses

**Modal Redirect URL** (only for live mode)

Use the redirect URL to return your customers back to your website with the response parameters returned in the query string. So If set, this will be the URL your customers will be returned to once the payment transaction is complete. In live mode the domain of the redirect URL must be on the same domain as the website you registered when onboarding with i-bank my Store.
This option is ideal for websites that do not use HTTPS.

```
<script type="text/javascript" src="https://www.uat.simplify.com/commerce/simplify.pay.js"></script>
<button data-sc-key="<put here your live public hosted api key>"
        data-name="Jasmine Green Tea"
        data-description="Smooth tea with a rich jasmine bouquet"
        data-reference="99999"
        data-amount="3000"
        data-color="#12B830"
        data-redirect-url="https://www.example.com/checkout.html">
        Buy Now
</button>
```
More about modal redirect url [here](https://ibanknbg.uat.simplify.com/commerce/docs/tools/hosted-payments#redirect-url) .

You can find more information about handling responses [here](https://ibanknbg.uat.simplify.com/commerce/docs/tools/hosted-payments#js).




### Test Results (live mode only)

If you are in live mode, choose one option and follow the instructions for 5 scenarios with the example number card below. It&#39;s important for each transaction you fill in the data reference in the table below. 

! Note: For each transaction you have to change the &quot;data-reference&quot; and then you try to do the payment. After payment add the data-reference in the table. [Download the table](https://nbgfilestorage.blob.core.windows.net/ecommerce/docs/Test%20Results.docx).

For more information about Hosted Checkout please visit this [documentation](https://ibanknbg.uat.simplify.com/commerce/docs/tools/hosted-payments).

**Example number card**

Correct Card Details:

Number_card: 5123450000000008  , 3Ds: yes , CVC: 100  , Exp. Date: 05/21


| Transaction | Card Number | ACS Simulator | Expected Result | Input Data | Test Case | Data  Reference |  ID  |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Authorization/Pay| 5123450000000008 |  Authenticated | ACCEPTED | Correct Data | 3D-Secure Authenticated |   |   |
| Authorization/Pay | 5123450000000008 |  NotAuthenticated | DECLINED | Correct Data | Not 3D-Secure Authenticated |   |   |
| Authorization/Pay | 5123450000000008 |   Attempted | ACCEPTED | Correct Data | 3D-Secure Attempted |   |   |
| Authorization/Pay | 5123450000000008 |   Unavailable | ACCEPTED | Correct Data | 3D-Secure Unavailable |   |   |
| Authorization/Pay | 5123450000000008 |  Authenticated | DECLINED | Wrong CVV (example 102) | 3D-Secure Authenticated |   |   |

Then try to make a payment with example number card. This card has ACS Simulator so, you can choose different option (different test cases). 

**Scenario 1:** Successful transaction with 3DS authentication successful.

Enter the card details and all other required details for the transaction. In the following 3DS emulator choose &quot;Authentication successful&quot; and press &quot;Submit&quot;. The payment should be completed successfully.

**Scenario 2:** _Transaction with 3DS authentication failure._

Enter all required details as before. In the following 3DS emulator choose &quot;Authentication failed&quot; and press &quot;Submit&quot;.The payment should be declined.

**Scenario 3:** _Successful transaction with 3DS authentication attempted._

Enter all required details as before. In the following 3DS emulator choose &quot;Authentication Attempted&quot; and press &quot;Submit&quot;. The payment should be completed successfully.

**Scenario 4:** _Successful transaction with 3DS authentication unavailable_

Enter all required details as before. In the following 3DS emulator choose &quot;Authentication Not Available&quot; and press &quot;Submit&quot;. The payment should be successful.

**Scenario 5:** Failed _transaction using a wrong CVC number with 3DS authentication successful._

Enter all required details as before, but with an invalid CVC number, 102 instead of 100 in this test case. In the following 3DS emulator choose &quot;Authentication Successful&quot; and press &quot;Submit&quot;.The payment should be declined.

After all these scenarios, you can confirm the result from the merchant administrator page using the &quot;data-reference&quot; into the Simplify platform / Transaction / Payments / filter by reference.

 ![img1](images/img1.png)

After finding the transaction you can see the details payments. When you find the payment with your &quot;data reference&quot; you can note the &quot;ID&quot; value in the table, too.

 ![SimplifyPlatform](images/SimplifyPlatform.PNG)

After filling in the data reference and the ID for each scenario, you have to send us the updated table.

### Direct API 

Another option to integrate is direct API. The Direct API Integration enables merchants to process credit card and check transactions in real time directly through ecommerce solution. To use direct API calls you have to download first the SDK from [here](https://ibanknbg.uat.simplify.com/commerce/docs/sdk/index). Also, in this case you have to use the (default) public API key (Live or SandBox). In below link you can find the API calls that you can use with instructions. Each section of our API includes detailed information about methods & parameters as well as example code.

[Direct API Calls instructions](https://ibanknbg.uat.simplify.com/commerce/docs/api/index?api=payments)

### Plugins (not appliccable in sandbox enviroment) 

You have the option to use popular e-commerce plugins. A software plug-in is an add-on for a program that adds functionality to it. It is mentioned that plugins are enabled for Live mode only. Below is a link of plugins and extensions with which you can integrate. 

[Plugins instructions](https://ibanknbg.uat.simplify.com/commerce/docs/plugins/index)

### Available SDKs
SDK (software development kit) is a set of software tools and programs used by developers to create applications for specific platforms. Below is a list of programming languages we provide support to develop with.  
Java, php, Ruby, Python Pelr, .net, node.js, ios, android

[SDKs instructions](https://ibanknbg.uat.simplify.com/commerce/docs/sdk/index)
