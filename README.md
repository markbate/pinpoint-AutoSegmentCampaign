**UseCases**

1) Product drops
2) Out of stock
3) New product launches for which customer has registered interest

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
3)	Pinpoint users must have a User Attribute named "interest" and that should match with the product DB payload variable "interest" if that user wants to receive an email

**Implementation**
1) Download the Amazon CloudFormation template in this Repository - https://github.com/Pioank/pinpoint-AutoSegmentCampaign/blob/main/AutoSegmentEmailCampaign.yaml
2) Navigate to the CLoudFormation part of the AWS console and create new Stack with Existing Resources
3) Upload the yaml template from step 1
4) You will need your Pinpoint App ID and the email that you would like to send the emails from (that email address needs to be verified via the Pinpoint console first)

## StateMachine Definition
![alt text](https://github.com/Pioank/pinpoint-AutoSegmentCampaign/blob/main/StateMachine-FlowChart.JPG)
