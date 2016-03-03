> This is a demo of SpecAlive.com UI specification.
>
> The purpose of this document is to demonstrate how to write UI system specification
> so that it is properly processed by SpecAlive.com.
>
> The quoted text contains instructions on how to write the specification.
>
> The un-quoted text is an example of a specification of a hypothetical sales system
> that demonstrates the features described.

# Sales System

> Use `heading level 1` to name the **system** being described by the specification.

Welcome to the specification of the Sales System.

The Sales System lets users keep records of their customers.

## Customers

> Use `heading level 2` to specify **entry points** into the system.
> An entry point will typically correspond to a main menu or a menu item.
> All system entry points are typically accessible from anywhere within the system,
> or at least from the system home (landing) page.
> 
> The customers entry point specifies the system functionality related to maintaining customers.

The Customers domain lets users work with customers.

> An entry point consists of pages.

### List customers [/customers]

> Use `heading level 3` to specify a **page**.
> Page represents all the UI elements displayed by the system to the user at once.
>
> Use square brackets after the name of the page to specify its **code**.
> (In a web application this may coincide with the URL or URL fragment of the page.)
> The code is then used to link to the page from buttons and table rows (see below).
>
> General page structure:
>
> - A page consists of **forms** and **tables**.
> - Both forms and tables can be either **editable** or **read-only**.
> - Forms and tables are specified as `list items` with leading keywords
> `EditForm`, `ReadOnlyForm`, `EditTable` and `ReadOnlyTable`.
> - Forms may contain other forms and tables.
> Composition of forms and tables within other forms is expressed by embedding `lists`.
> - Forms and tables contain **fields** (or **columns** in tables)
> and **buttons** / **links**.
> These are specified as plain `list items` (with no leading keyword)
> within the form's / table's `list`.

The List customers page allows users to search customers
and select a customer to work with.

- EditForm Customer criteria

	> A `list item` starting with keyword `EditForm` specifies a **form** with **editable** fields.
	>
	> The _Customer criteria_ editable form specifies the criteria for
	> finding customers.

	User enters criteria to find a customer.

	> Use `embedded list items` to specify **fields** of the form.

	- name (text) - Find customer by name. Case-insensitive, starts-by match.
	
	> Use parentheses to specify the **type** of the field. The supported types are:
	>
	> - `text`: plain text field
	> - `password`: text field with the value hidden
	> - `number`: a text field allowing numerical input
	> - `date`: a text field allowing date input
	> - `date-range`: a text field to enter a range of dates (date from, date to)
	> - `time`: a text field allowing time input
	> - `checkbox`: a checkbox field, boolean value
	> - `select`: a dropdown / combobox field that lets the user select a single value from a list of available values
	> - `radios`: list of radio buttons to select a single value from a list of fixed values
	> - `multi-select`: a dropdown / combobox field that lets the user select multiple values from a list of available values
	> - `checkboxes`: list of checkboxes to select multiple values from a list of fixed values
	>
	> The text type is default.

- ReadOnlyTable Customer list

	> This `list item` specifies a **read-only** UI **table** that presents multiple records.
	> The records are typically displayed as rows in a table.
	>
	> (It may be a table with explicitly separate and labelled columns,
	> or it may also be a simple list of rows where each row presents the data
	> of the record in such a way as to make the meaning of each piece of data obvious.)

	The Customer list displays customers matching the criteria entered by the user.

	> The `embedded list items` of a table specify the data **columns** in the UI table.

	- name - Customer name
	- taxNo - Tax number

- ReadOnlyForm

	> This anonymous read-only form wraps the following button
	> at the bottom of the _List customers_ page.
	>
	> A button (or a link) may optionally **refer to a page** 
	> by using its code as the `target` of the `link`.

	- [Create](/customers/new "Create new customer")

		> Use a `link` to represent a **button**.

### Create customer [/customers/new]

Create customer page lets the user create a new customer record.

> Use an `EditForm` to specify an editable form 
> and then use `list items` within the form to specify the fields of the form.

- EditForm Create customer

	- EditForm Customer
	
		Customer data.

		- taxNo - Tax number
	
			Format: 2 upper-case letters (A-Z), 
			2-12 upper-case letters or numbers (A-Z, 0-9).
			
			> Use an embedded paragraph to further specify the field.
	
		- [Load](# "Verify tax number and load customer data")
		
			> Use `#` as the target of a `link` that does not navigate to other page.
			>
			> Specify the system functionality on the _Load_ button.

			1. System verifies the tax number is valid and pre-fills the following fields (if empty):
	
				- `name`
				- `country`
				- `city`
				- `street`
				- `postalCode`
			
			2. When tax number is **invalid**, system displays **error** 
			but lets the user **continue** with the invalid tax number.
			
			3. When tax number **could not be verified**, system displays **warning**.
	
		- name (text, required) - The name of the customer
		
			> Use the `required` keyword after the field type to specify a **required** field.
		
		- invoiceMaturity: 30, 60, 90 (select, required) - Invoice maturity
		
			> Specify the available values after the name of the field and a colon 
			> (for field types that select from a list of values,
			> i.e. `select`, `radios`, `multi-select`, `checkboxes`).
		
		- web - URL of the customer's web site

	- EditForm Address
	
		Customer address data.

		- country (text, required)
		- city (text, required)
		- street
		- postalCode

	- EditForm Contact
	
		Customer contact data.
		
		- salutation: Mr, Ms (select)
		- lastName (text, required)
		- firstName
		- workPhone
		- mobilePhone
		- email
		
		One of `workPhone`, `mobilePhone`, `email` is required.
	
	- [Save](/customers/detail)
	
		> Specify the system functionality on the _Save_ button.
	
		1. When a customer with the `taxNo` **already exists**, system displays **error**.
		
		2. System creates new customer.

	- [_Cancel_](/customers "Return back to Customer list")

		> Use a `link` with `emphasized` text (wrapped in underscores) to represent plain HTML links.
