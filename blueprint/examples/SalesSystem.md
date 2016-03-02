# Sales System

This is a demo of SpecAlive.com UI specification.

The purpose of this document is to demonstrate how to write UI system specification
so that it is properly processed by SpecAlive.com.

Use `heading level 1` to name the system being described by the specification.

## Customers

Use `heading level 2` to specify entry points into the system.
An entry point will typically correspond to a main menu or a menu item.

All system entry points are typically accessible from anywhere within the system,
or at least from the system home (landing) page.

The customers entry point specifies the system functionality related to maintaining customers.

### List customers

Use `heading level 3` to specify a page.
Page represents all the UI elements displayed by the system at once.

On general page structure:

- Page consists of editable forms, read-only forms, editable lists and read-only lists.
- Forms (both editable and read-only) may contain other forms and lists.
- The forms and lists are specified as `list items` with leading keywords
`EditForm`, `ReadOnlyForm`, `EditList` and `ReadOnlyList`.
- Composition of forms and lists within other forms is expressed by embedding
HTML `lists`.
- Forms contain fields and buttons / links. Lists contain data columns.
- A page may contain fields directly (without embedding them within a form)
in which case an implicit editable form is assumed.

The List customers page allows users to find and list customers
and select a customer to work with.

- EditForm Customer criteria

	A `list item` starting with keyword `EditForm` specifies a form with editable fields.

	The Customer criteria editable form specifies the criteria for
	finding customers.

	Use `embedded list items` to specify fields of the form.

	- name (text) - Find customer by name. Case-insensitive, starts-by match.

	- ReadOnlyList Customer list
	
		This `embedded list` specifies a read-only UI list widget that presents multiple records.
		The records are typically displayed as rows.
		It may be a table with explicitly separate and labelled columns,
		or it may also be a simple list of rows where each row presents the data
		of the records in such a way as to make the meaning of each piece of data obvious.
		
		The `embedded list items` of a list specify the data columns (pieces) of each row in the UI list.

		The Customer list displays customers matching the criteria specified by the user.
		
		- name - Customer name
		- taxNo - Tax number

	- [Create](#create-customer)
	
		Use `links` to represent buttons or HTML links.
		A `link` refers to a page.

### Create customer

Create customer page lets the user create a new customer record.

Use list items to specify 

- taxNo (text) - Tax number
- name (text, required) - The name of the customer
