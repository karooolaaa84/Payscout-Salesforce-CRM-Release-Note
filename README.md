# Payscout-Salesforce-CRM-Release-Note
Payscout Salesforce CRM Release Note April 2019

Payscout PS Approval Request Changes
A process to validate opportunity before attempting to create a PS Approval Request has been added.  For example, previously there was an issue if the sales agent field was not filled in the system would crash due to the workflow requiring this field to continue.  Users will access the Approval Request in the same dropdown from the opportunity record

When a user attempts to create a PS Approval Request from the opportunity record.
If a sales agent has not been selected, an error will appear

If a sales agent has been selected, the PS Approval Request create form will appear

Once a PS Approval Request has been created
The related Merchant Account is no longer editable
The related Merchant Account Boarding Stage is changed to “Pending - Approval Request”.
Once a PS Approval Request has been approved. 
The PS Approval Request is no longer editable.
The related merchant account becomes editable again.
The related merchant account boarding stage becomes “Ready for Boarding”
When a Merchant Account of a PS Approval Request that has been approved is edited, the updated information is copied to the related PS Approval Request.

Changes to accommodate object data type mismatching
There was a mismatch in data type between the Approval Request and the Merchant account object that caused crashes. Since there’s data in both of these, simply changing the datatype to fix this issue was not an option. Work has been done to accommodate for this data transfer need in the workflow:

Merchant Account
PS Approval Request

Review Cycle
Text-Field
 

Review Cycle
Pick-List



Settlement Delay
Text-Field
 

Settlement Delay
Pick-List



This is causing problems when a value is entered into the text field that does not exist in the Pick-List. Since there is data in the tables, simply changing the data-type is not an option. The approach for fixing this issue will be:
Promoting the object pick-list to a global pick-list.
Creating a new field on the object with the text-field (Merchant Account). This is field will reference the global pick-list created above.
Creating a process to copy the data selected in the new field and into the old text field

Logical Delete Changes - a new Account record type has been added to identify if an account has been logically deleted. Please find the changes to accommodate this below:
Page Layout - a new page layout will be created for the Deleted record type. A logically deleted record should no longer be editable, but there should be an option to “activate” the merchant.

Activate - when a merchant account is “Activated” the “ - Deleted” is removed from the name and the merchant is valid to have opportunity again
List view -  current list view will be modified to exclude deleted account and a new view will be created to show only deleted account
Merchant Account name 
A workflow will be created to append “Deleted” to the merchant account name when an account is assigned to the deleted record type
A workflow will be created to remove “Deleted” from the merchant account name when an account is reactivated

Marking an account as Deleted - an account with related opportunities cannot be marked as deleted. The opportunities must be reassigned to another merchant account before a merchant account can be logically deleted.
When a user tries to delete a merchant account, if there’s opportunity record(s) tie to that account, a modal will appear with a dropdown list of active account that the user can select to reassign the opportunity record(s) to.

Once all records have been reassigned, the merchant account will be marked as deleted
Primary Identifier for Merchant Account - a new custom field “IsPrimary” has been created on the Merchant Account.
The new checkbox has been added to the Merchant Account layout

New Identifier to Differentiate Prospects and Clients - The new field called “Type” has been added to the Lead, Account, Contact, and Opportunity  object. All of the fields are reference the same global pick list which includes Merchant, ISO, Agent, ISV. I have also added mapping for this field so that went a lead is converted, the field will be passed along to the newly created object. 
