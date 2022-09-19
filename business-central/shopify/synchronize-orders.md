---
title: Synchronize and Fulfill Sales Orders
description: Set up and run import and processing of sales order from Shopify.
ms.date: 05/27/2022
ms.topic: article
ms.service: dynamics365-business-central
ms.search.form: 30110, 30111, 30112, 30113, 30114, 30115, 30121, 30122, 30123, 30124, 30125, 30128, 30129, 30130, 30131, 30132, 30133, 30134, 
author: edupont04
ms.author: andreipa
ms.reviewer: solsen
---

# Synchronize and Fulfill Sales Orders

This article describes the necessary settings and steps that you must complete to synchronize and fulfill sales orders with Shopify in [!INCLUDE[prod_short](../includes/prod_short.md)].

## Set the import of orders on the Shopify Shop Card

A regular Shopify order can include costs in addtion to the subtotal, such as shipping charges or, if enabled, tips. These amounts are posted directly to the G/L account you want used for specific transaction types:

- **Shipping Cost Account**
- **Sold Gift Card Account**; learn more at [Gift Card](synchronize-orders.md#gift-cards)
- **Tip account**  

Enable **Auto Create Orders** to automatically create sales documents in [!INCLUDE[prod_short](../includes/prod_short.md)] once the Shopify order is imported.
The sales document in [!INCLUDE[prod_short](../includes/prod_short.md)] contains a link to the Shopify order. If you select the **Shopify Order No. on Doc. Line** field, this information is repeated in the sales lines of type *Comment*.

In the **Tax area source** field, you can set the priority on how to select tax area code or VAT business posting group based on address. This step is relevant for countries with sales tax as well as those with VAT. Learn more at [Tax remarks](synchronize-orders.md#tax-remarks).

### Shipment method mapping

The **Shipment method code** for sales documents imported from Shopify can be filled in automatically. You need to configure the **Shipment Method Mapping**.

1. Choose the ![Lightbulb that opens the Tell Me feature 1.](../media/ui-search/search_small.png "Tell me what you want to do") icon, enter **Shopify Shops**, and then choose the related link.
2. Select the shop for which you want to define mapping to open the **Shopify Shop Card** page.
3. Choose the **Shipment Method Mapping** action. This automatically creates records for shipping methods defined in the [**Shipping**](https://www.shopify.com/admin/settings/payments) settings in your **Shopify admin**.
4. In the **Name** field, you can see the name of the shipping method from Shopify.
5. Enter the **Shipment Method Code** with the corresponding shipping method in [!INCLUDE[prod_short](../includes/prod_short.md)].

> [!NOTE]  
> If multiple shipping charges are associated with a sales order, only one will be selected as the shipping method and assigned to the sales document.

### Payment method mapping

To fill in the **Payment method code** for sales documents imported from Shopify automatically, you need to configure **Payment method mapping**.

1. Choose the ![Lightbulb that opens the Tell Me feature 1.](../media/ui-search/search_small.png "Tell me what you want to do") icon, enter **Shopify Shops**, and then choose the related link.
2. Select the shop for which you want to define mapping to open the **Shopify Shop Card** page.
3. Choose the **Payment Method Mapping** action.
4. In the **Gateway** and **Credit Card Company** fields, enter the name of the payment method from Shopify. The record gets created automatically when you import Shopify orders.
5. Enter the **Payment Method Code** with the corresponding payment method in [!INCLUDE[prod_short](../includes/prod_short.md)].
6. Set the **Priority** for cases when the customer uses multiple means of payment. The payment method with the highest priority gets selected in the sales document. If both payment methods have the same priority, the payment method with the highest amount is used.

> [!NOTE]  
> If corresponding payment method in [!INCLUDE[prod_short](../includes/prod_short.md)] has **Bal. Account Type** and **Bal. Account No.** populated, then during posting the invoice system will create a balancing entry of the *Payment* type and apply it to the *Invoice* type in the customer ledger entry.

### Location mapping

To fill in the **Location Code** for sales documents imported from Shopify automatically, you need to configure the **Shopify Shop Locations**.

1. Choose the ![Lightbulb that opens the Tell Me feature 1.](../media/ui-search/search_small.png "Tell me what you want to do") icon, enter **Shopify Shops**, and then choose the related link.
2. Select the shop for which you want to configure the mapping of locations to open the **Shopify Shop Card** page.
3. Choose the **Locations** action to open the **Shopify Shop Locations**.
4. Choose the **Get Shopify Locations** action to import all the locations defined in Shopify. You can find them in the [**Locations**](https://www.shopify.com/admin/settings/locations) settings in your **Shopify admin** panel. Note that the location marked as *Default* will be used when importing unfulfilled Shopify orders.
5. Enter the **Default Location Code** with the corresponding location in [!INCLUDE[prod_short](../includes/prod_short.md)].

> [!NOTE]  
> You must configure the location mapping if the **Location Mandatory** toggle is enabled on the **Inventory Setup** card or you won't be able to create sales documents.

## Run the order synchronization

The following procedure describes how to import and update the sales orders.

> [!NOTE]  
> Archived orders in Shopify can't be imported. Deactivate the **Automatically archive the order** option in the **Order Processing** section of the **Checkout** settings in your **Shopify Admin** panel to make sure that all orders are imported to [!INCLUDE[prod_short](../includes/prod_short.md)]. If you need to import archived orders, use the **Unarchive Orders** action in the [Orders](https://www.shopify.com/admin/orders) page of the **Shopify admin** panel.

1. Choose the ![Lightbulb that opens the Tell Me feature 1.](../media/ui-search/search_small.png "Tell me what you want to do") icon, enter **Shopify Shops**, and then choose the related link.
2. Select the shop for which you want to import orders to open the **Shopify Shop Card** page.
3. Choose the **Orders** action.
4. Choose the **Sync Orders From Shopify** action.
5. Define filters on orders as necessary. For example, you can import fully paid orders or the ones with a low risk level.
6. Choose the **OK** button.

Alternatively, you can search for the **Sync Orders From Shopify** batch job.

You can schedule the task to be performed in an automated manner. Learn more at [Schedule recurring tasks](background.md#to-schedule-recurring-tasks).

## Review imported orders

Once the import is completed, you can explore the Shopify order and find all related information, such as the payment transactions, shipping costs, risk level, or fulfillments, if the order was already fulfilled in Shopify. You can also see any order confirmation that has been sent to the customer by choosing the **Shopify Status Page** action.

> [!NOTE]  
> You can navigate to the **Shopify Orders** window directly and you'll see orders with the *open* status from all shops. To review completed orders, you need to open the **Shopify Orders** page from the specific **Shopify Shop Card** window.

## Create sales documents in Business Central

If the **Auto Create Orders** toggle is enabled on the **Shopify Shop Card**, [!INCLUDE[prod_short](../includes/prod_short.md)] tries to create a sales document once the order is imported. If issues such as a missing customer or product occur, you'll need to fix the problems then create the sales order again.

### To create sales documents

1. Choose the ![Lightbulb that opens the Tell Me feature 1.](../media/ui-search/search_small.png "Tell me what you want to do") icon, enter **Shopify Shops**, and then choose the related link.
2. Select the shop for which you want to synchronize orders to open the **Shopify Shop Card** page.
3. Choose the **Orders** action.
4. Select the order for which you want to create a sales document and choose the **Create Sales Documents** action.
5. Choose **Yes**.

If the Shopify order requires fulfillment, a **Sales Order** is created. For fulfilled Shopify orders, such as those orders that contain only a gift card or which are already handled in Shopify, a **Sales Invoice** gets created.

A sales document is now created and can be managed by using standard [!INCLUDE[prod_short](../includes/prod_short.md)] functionality.

### Manage missing customers

If your settings prevent creating a customer automatically and a proper existing customer can't be found, you'll need to assign a customer to the Shopify order manually. There are a few ways to do this:

- You can assign the **Sell-to Customer No.** directly on the **Shopify Orders** page by choosing a customer from the list of existing customers.
- You can select a customer template code, then create, and assign the customer via the **Create new customer** action on the **Shopify Orders** page.
- You can map an existing customer to the related **Shopify Customer** in the **Shopify Customers** window and then choose the **Find Mapping** action in the **Shopify Orders** page.

### Tax remarks

The imported Shopify order contains information about taxes, but the taxes get recalculated when you create the sales document so it's important that the VAT/tax settings are correct in [!INCLUDE[prod_short](../includes/prod_short.md)].

- Multiple product VAT/tax rates. For example, some product categories are liable for reduced tax rates. Those items must exist in [!INCLUDE[prod_short](../includes/prod_short.md)] and be mapped to Shopify products. Otherwise, with automatic creation of missing items, the VAT product posting group is used.

- Address-dependent tax rates. Use the **Tax area priority** field together with the **Customer Templates** table to overwrite standard logic that fills in the **Tax Area Code** in the sales document. The **Tax area priority** field specifies the priority used to determine the information about the country/region and state/province. Then the corresponding record in the Shopify customer templates is found and the **Tax Area Code**, **Tax Liable**, and **VAT Bus. Posting Group** are used when a sales document is created.

- Price including Tax. The **Prices including Tax**/**Prices including VAT** field in the created sales document doesn't depend on the customer, but on the **Customer Template** from the **Shopify Shop Card** page or Customer template per country.

### Impact of order editing

In Shopify:

|Edit|Impact|
|------|-----------|
|Change the fulfillment location | Original location will be synched to [!INCLUDE[prod_short](../includes/prod_short.md)]. |
|Edit an order and change quantity| Order header and supplementary tables will be updated in [!INCLUDE[prod_short](../includes/prod_short.md)], lines won't. |
|Edit an order and add new item | Order header will be updated, lines won't. |

In [!INCLUDE[prod_short](../includes/prod_short.md)]:

|Edit|Impact|
|------|-----------|
|Change the location to another location, mapped to the Shopify Locations. Post shipment. | After synchronizing the fulfillment, location will be updated in Shopify. |
|Change the location to another location, not mapped to the Shopify Locations. Post shipment. | The fulfillment won't be synchronized with Shopify. |
|Change decrease quantity. Post shipment. | The Shopify order will be marked as partially fulfilled. |
|Add a new item. Post shipment. | The Shopify order will be marked as fulfilled. Lines won't be updated. |

## Synchronize shipments to Shopify

When a sales order created from a Shopify order is shipped, you can synchronize the shipments with Shopify.

1. Choose the ![Lightbulb that opens the Tell Me feature 1.](../media/ui-search/search_small.png "Tell me what you want to do") icon, enter **Sync Shipments to Shopify**, and then choose the related link.
2. Define the filters on shipments as necessary. For example, you can update a shipment posted on a specific date.
3. Choose the **OK** button.

The order in Shopify will be marked as fulfilled. The customer automatically receives a shipment notice email or text message (SMS). If a shipping agent and a tracking code are specified on the shipment, the tracking information is included in the email.

> [!NOTE]  
> Remember to run **Synchronize Orders from Shopify** to update the fulfillment status of an order in [!INCLUDE[prod_short](../includes/prod_short.md)]. The connector functionality also archives completely paid and fulfilled orders in both Shopify and in [!INCLUDE[prod_short](../includes/prod_short.md)] provided the conditions are met.

### Shipping agents and tracking URL

If the **Posted Sales Shipment** document contains the **Shipping Agent Code** and/or **Package Tracking No.**, this information will be sent to Shopify and to the customer in the shipping confirmation email.

The tracking company is populated in the following order (from highest to lowest) based on the shipping agent record:

- **Shopify Tracking Company**
- **Name**
- **Code**

If the **Package Tracking URL** field is filled in for the shipping agent record, then the shipping confirmation will contain a tracking URL as well.

## Gift cards

In the Shopify shop you can sell gift cards, which can be used to pay for real products.

When dealing with gift cards, it's important to enter a value in the **Sold Gift Card Account** field in the **Shopify Shop Card** window. The sold gift card will be synchronized together with orders in line. An applied gift card will also be imported with the order, but now as a transaction. Notice that the gift card doesn't reduce the amount to invoice.

To review the issued and applied gift cards, choose the ![Lightbulb that opens the Tell Me feature.](../media/ui-search/search_small.png "Tell me what you want to do") icon, enter **Gift Cards**, and then choose the related link.

## Transactions and payouts

When a customer completes their checkout in the online store, the information about payments is saved as a **Transaction**. There might be multiple transactions linked to the order, such as when a customer uses a gift card to pay some of the cost and then uses a credit card or PayPal for the remaining amount. 

If you use Shopify Payment as a payment provider, then in addition to information about money received from the customer by the payment provider, you can also see payouts from Shopify to your bank account. 

### Transactions

The payment transactions that take place in Shopify are synchronized with the orders and can be viewed on the *Shopify Orders* page.

To review all transactions, choose the ![Lightbulb that opens the Tell Me feature 1.](../media/ui-search/search_small.png "Tell me what you want to do") icon, enter **Transactions**, and select the related link.

If you configured payment method mapping then the created sales document will have a Payment Method Code assigned. Learn more at [Payment Method Mapping](#payment-method-mapping).

### Payouts

If your store uses Shopify Payment, you'll receive payments through *Shopify Payouts* when a customer pays using Shopify Payments and accelerated checkouts.

1. Choose the ![Lightbulb that opens the Tell Me feature 1.](../media/ui-search/search_small.png "Tell me what you want to do") icon, enter **Shopify Shops**, and then choose the related link.
2. Select the shop for which you want to synchronize payouts to open the **Shopify Shop Card** page.
3. Choose the **Sync Payouts** action.

To review all payouts, choose the ![Lightbulb that opens the Tell Me feature.](../media/ui-search/search_small.png "Tell me what you want to do") icon, enter **Payouts**, and select the related link.

**Payouts** are for information purposes only and don't impact the General Ledger or Bank Ledger, though they can be helpful when you process your bank account statement.

## See also

[Get Started with the Connector for Shopify](get-started.md)  