**Background**

Customers want to be up to date with the latest products while companies want inform their customers about new entries in their product database. To avoid "SPAMMING", companies need to identify their customers' interests. Once the interests such as product category have been identified, then a process will need to be created so that every time a product enters the database, customers who are interested in that product category will be informed.

**Solution**

Ideally an entry of a new product would trigger the communication process to the right customer segment automatically with no human intervention. To achieve the latter, this solution uses Amazon Step Function and Pinpoint APIs to:
1) Receive the payload from the Products' DB
2) Create a dynamic segment based on the customers' interests stored in the User Attributes
3) Send an Email campaign immediately
4) Delete both segment and campaign once they have been both completed

This process is fully automated and the only input required is the product Category of the new product, the product name and product link. Note that these fields can be changed but code changes will be required.

Incoming payload example from the Products' Database:

{
  "interest": "festivals",
  "product_name": "Coachella",
  "product_link": "https://www.coachella.com/"
}

**Considerations**

1)	You will need to amend the email HTML body template on the "Create Campaign Lambda"
2)	The solution is currently configured to send email campaigns immediately

## StateMachine Definition
![alt text](https://github.com/Pioank/pinpoint-AutoSegmentCampaign/blob/main/StateMachine-FlowChart.JPG)
