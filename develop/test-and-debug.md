---
title: Test and debug
description: To test your code, you should use your integration sandbox account in Partner Center (and the corresponding tokens) so that you don't accidentally incur new charges that your company is responsible for paying.
Author: Xansky
ms.assetid: 0A84F92F-CE66-42DF-B686-4D9E6FFECB16
ms.date: 09/11/2018
ms.localizationpriority: medium
---

# Test and debug


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

To test your code, you should use your integration sandbox account in Partner Center (and the corresponding tokens) so that you don't accidentally incur new charges that your company is responsible for paying. For more information about this test-in-production (TiP) environment, see [Set up API access in Partner Center](set-up-api-access-in-partner-center.md).

## <span id="Integration_sandbox_constraints"></span><span id="integration_sandbox_constraints"></span><span id="INTEGRATION_SANDBOX_CONSTRAINTS"></span>Integration sandbox constraints

If you run automated build verification tests, conduct testing in production, or perform manual testing in the integration sandbox, you may reach the maximum limits for the integration sandbox. These limits are 75 customers, 5 subscriptions per customer, and 25 seats per subscription. 

This means you cannot acquire an offer in the sandbox that has a minimum seat requirement that exceeds 25 seats. This includes trials. 

### Cloud Solution Provider (CSP) Azure subscription offers 
CSP Azure subscription offers are no longer available by default to sandbox accounts. These include MS-AZR-0146P, MS-AZR-DE-0146P and MS-AZR-USGOV-0146P for CSP Azure subscriptions in Microsoft Public Cloud, German Cloud and Government Cloud respectively. Partners who need access to these offers with their sandbox account must apply for access. To apply for access, reach out to your Microsoft account manager or business contact. 

For partners whose sandbox accounts have been approved for CSP Azure subscription offers, the following limits apply:  

 - You can have up to a maximum of 375 active subscriptions (75 customers x 5 subscriptions per customer). However, only 10 of which can be CSP Azure subscriptions.  
 - When a CSP Azure subscription reaches $200 of Azure usage, its resources are temporarily disabled until its next billing cycle. It is still considered an active subscription and is counted towards the 10 active Azure subscriptions limit.  
 - Each CSP Azure subscription under your sandbox account is limited to 4 virtual machine (VM) cores per data center. Therefore, you cannot provision VM SKUs that require more than 4 VM cores. Certain specialized VM SKUs such as GPU cores are also excluded.  

> [!Important]  
> All existing CSP Azure subscriptions provisioned with sandbox accounts prior to August 1, 2018 are no longer supported and will be deprovisioned by Microsoft between October 16 – October 31, 2018. After the subscriptions have been deprovisioned, they cannot be re-enabled, and associated data are no longer accessible. Partners who have valuable data stored under these subscriptions must back up the data before October 16, 2018.

### Azure Reserved VM instance  

If you are [purchasing an Azure Reserved VM instance](purchase-azure-reservations.md) with your sandbox account, you are limited to 2 VM instances per customer. You are also limited to selecting only from the following Azure Reserved VM instance product SKUs: 

| Product Title  | Effective Date  | Sku Title                                               | Region [ArmRegionName] | Instance Key [ArmSkuName] | Duration | Consumption Meter Id       |
|----------------|-----------------|---------------------------------------------------------|------------------------|--------------|----------|----------------------------|
| B Series       | 12/1/2017 0:00  | Reserved VM instance, Standard_B1s, KR South, 1 year    | KoreaSouth             | Standard_B1s | 1Year    | 3f913071-0dd7-4258-8ec4-6fad05bd976d |
| B Series       | 12/1/2017 0:00  | Reserved VM instance, Standard_B1s, US East, 1 year     | eastus                 | Standard_B1s | 1Year    | f4d7a5a5-1b67-45ea-b1a0-282fbdd34b05 |
| B Series       | 12/1/2017 0:00  | Reserved VM instance, Standard_B1s, US West 2, 1 year   | westus2                | Standard_B1s | 1Year    | 222e39f5-e99f-4fa3-a323-f46402977888 |
| B Series       | 12/1/2017 0:00  | Reserved VM instance, Standard_B1s, US North Central, 1 year    | northcentralus | Standard_B1s | 1Year    | 4e1716fc-4842-43f1-aa96-7c1b1b1395a7 |
| B Series       | 12/1/2017 0:00  | Reserved VM instance, Standard_B1s, CA East, 1 year     | CanadaEast             | Standard_B1s | 1Year    | ab8a5993-5db7-47c8-b3b1-2e1365b353fb |
     

To clean up at the end of your test run so there's space for the next round of testing, see the following topics:

-   [Delete a customer account from the integration sandbox](delete-a-customer-account-from-the-integration-sandbox.md)

-   [Decrease the quantity of a subscription](change-the-quantity-of-a-subscription.md)

-   [Suspend a subscription](suspend-a-subscription.md) so that you can remove it.

## <span id="Best_practices_for_REST_development"></span><span id="best_practices_for_rest_development"></span><span id="BEST_PRACTICES_FOR_REST_DEVELOPMENT"></span>Best practices for REST development


-   Use a network trace tool so that you can see your request, the response, and if there were any errors in the HTTP status code in the response. For more information about error handling, see [Partner Center REST error codes](error-codes.md).

-   Use a new Correlation ID for each call made to the Partner Center REST API. This ensures better logging and will help during debugging. For more information, see [Partner Center REST headers](headers.md).

## <span id="Troubleshooting_tips_for_common_REST_problems"></span><span id="troubleshooting_tips_for_common_rest_problems"></span><span id="TROUBLESHOOTING_TIPS_FOR_COMMON_REST_PROBLEMS"></span>Troubleshooting tips for common REST problems


-   Review all header properties, including the URL and API version.

-   Ensure properties are included if required, and correctly formatted.

-   Incorrect array formatting is a common error.

-   **ETags** are temporary and therefore should not be stored. When a function call requires an **ETags**, use the latest **ETags** value by getting the resource again. **ETags** values should be included in double quotation marks, like a string:

    ```
    If-Match : "eyJpZCI6IjUwMWE4NjBjLTE2OTgtNDQyYi04MDhjLTRiNjEyY2NmMzVmMiIsInZlcnNpb24iOjF9"
    ```

 

 




