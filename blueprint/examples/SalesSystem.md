> This is a tutorial of SpecAlive UI specification.
>
> The purpose of this document is to demonstrate how to write UI system specification
> so that it is properly processed by SpecAlive.
>
> The quoted text contains instructions on how to write the specification.
>
> The un-quoted text is an example of a specification of a hypothetical sales system
> that demonstrates the features described.

# Sales System

> Use `heading level 1` to name the **system** being described by the specification.

#### Functional specification

> Heading 2 and 3 are reserved (see below), but headings 4 and higher can be safely used in the text.

The Sales System lets users keep records of their products, customers and orders.

This document specifies the functionality of the Sales System.
It does so by describing the interactions of a user with the system.
The system is described from the outside (as a black box) as the user will see it.

This documentation is in itself interactive and lets the reader interact
with it by opening screens and following links in between them.
This in effect gives the reader an opportunity to better visualize
how the users will work with the system
and hopefully also better understand its functionality.

**This document is NOT, by any means, complete.**
It is a working draft, there are system functions yet to be added 
and all the wording may still be changed.

This document does NOT specify the layout of the screens (how the elements will be arranged).
It does NOT specify the graphical look of the screens either.
Both of these will be defined by a graphical designer in a process separate from this document.
The aim of this documentation is to specify the functionality of the system
and the screens presented here only illustrate the functionality,
they do not attempt to match the target look and feel of the system.

This document is maintained by Andy Thor,
you can reach me at a.u.thor@theco.com should you have any questions, comments or suggestions.
I'd be happy to help you.


## Products

> Use `heading level 2` to specify **entry points** into the system.
> An entry point will typically correspond to a main menu or a menu item.
> All system entry points are typically accessible from anywhere within the system.
> 
> The products entry point specifies the system functionality related to maintaining products.

The Products domain lets users maintain product database within the system.

> An entry point consists of screens.

### List products [/products]

> Use `heading level 3` to specify a system **screen**.
>
> Use square brackets after the name of the screen to specify its **code**.
> The code is then used to link to the screen from buttons (see below).
>
> General screen structure:
>
> - A screen consists of **forms** and **tables**.
> - Both forms and tables can be either **editable** or **read-only**.
> - Forms and tables are specified as `list items` with leading keywords
> `EditForm`, `ReadOnlyForm`, `EditTable` and `ReadOnlyTable`.
> - Forms and tables can be nested as required.
> Composition of forms and tables is expressed by embedding `lists`.
> - Forms / tables contain **fields** / **columns** and **buttons**.
> These are specified as plain `list items` (with no leading keyword)
> within the form's / table's `list`.

The List products screen allows users to search products
and select a product to work with.

- EditForm Product criteria

	> A `list item` starting with keyword `EditForm` specifies a **form** with **editable** fields.
	>
	> The _Product criteria_ editable form specifies the criteria for
	> finding products.
	
	User enters criteria to find a product.

	> Use `embedded list items` to specify **fields** of the form.

	- name (text)

	> A field specification starts with the **code** of the field.
	>
	> Use parentheses to specify the **type** of the field. The supported types are:
	>
	> - `text`: plain text field
	> - `password`: text field with the value hidden
	> - `number`: a text field allowing numerical input
	> - `date`: a text field allowing date input
	> - `time`: a text field allowing time input
	> - `checkbox`: a checkbox field, boolean value
	> - `select`: a dropdown / combobox field that lets the user select a single value from a list of available values
	> - `radios`: list of radio buttons to select a single value from a list of fixed values
	> - `multi-select`: a dropdown / combobox field that lets the user select multiple values from a list of available values
	> - `checkboxes`: list of checkboxes to select multiple values from a list of fixed values
	>
	> The `text` type is default, so it can actually be omitted in the _name_ field specification above.

	- ean - EAN
	
		> By default, the **field label** is derived from its code automatically.
		> You can however specify a custom label after dash.
	
	- status: Active, Disabled (select)

		> Specify the value of the field after a colon.
		> Multiple values can be specified by separating them with a comma.

- ReadOnlyTable Product list

	> This `list item` specifies a **read-only** UI **table** that presents multiple records.
	> The records are typically displayed as rows in a table.

	The system displays products matching the criteria entered.
	For text fields, system performs case-insensitive, starts-by match.

	> The `embedded list items` of a table specify the data **columns** in the UI table.

	- name: T-shirt Orange, T-shirt Tutti Frutti, T-shirt Free, T-shirt Hipster, Cookies Chocolate Ecuador, Cookies Chocolate Venezuela, Cookies Orange
	- ean: 70107773572, 70115256941, 70112074810, 70112074810, 70114765149, 70108874916, 70108669294
	- status: Active, Active, Active, Active, Disabled
	- recommendedRetailPrice: 9.99, 9.99, 9.99, 9.99, 2.89, 2.89, 2.89
	- [View](/products/detail "View product detail")

		> Use a `link` to represent a **button**.
		>
		> A button can either navigate to another screen,
		> perform some functionality, or do both of these.
		>
		> A button **refers** to another screen 
		> by using the screen's code as the `target` of the `link`.

- ReadOnlyForm

	> This anonymous read-only form wraps the following button
	> at the bottom of the _List customers_ screen.

	- [Create](/products/new "Create new product")

### Create product [/products/new]

Create products screen lets the user create a new product record.

> Use an `EditForm` to specify an editable form 
> and then use `list items` within the form to specify the fields of the form.

- EditForm New product

	- name (text, required)
		
		> Use the `required` keyword after the field type to specify a **required** field.
		>
		> The type can also be omitted, in which case it defaults to `text` as in the following field.

	- ean (required) - EAN
	- cogs (number, required) - COGS
	
		Cost of goods sold, the buying price.
			
		> Use an embedded paragraph to further specify the field.
	
	- retailPrice (number, required)
	- vatRate (number, required) - VAT rate

	- [Save](/products/detail)
	
		> Specify the system functionality on the _Save_ button.

		1. If a product with the EAN code already exists: system displays **error**.
		
		2. System creates new product.

	- [Cancel](/products "Return back to Product list")

### Product detail [/products/detail]

- ReadOnlyForm Product

	- name: T-shirt Orange
	- status: Active
	- ean: 70107773572 - EAN
	- cogs: 3.54 - COGS
	- retailPrice: 9.99
	- vatRate: 15 % - VAT rate

	- [Edit](/products/detail/edit "Edit the product")
	- [Disable]()
	
		Enabled for status active.
		
		System sets status disabled.

	- [Activate]()
	
		Enabled for status disabled.
		
		System sets status active.

	- [Cancel](/products "Return back to Product list")

### Edit product [/products/detail/edit]

- EditForm Edit product

	- name: T-shirt Orange (text, required)
	- ean: 70107773572 (required) - EAN
	- cogs: 3.54 (number, required) - COGS
	- retailPrice: 9.99 (number, required)
	- vatRate: 15 (number, required) - VAT rate

	- [Save](/products/detail)

		1. If other product with the EAN code already exists: system displays **error**.
		
		2. System updates the product.

	- [Cancel](/products/detail "Return back to Product detail")


## Customers

The Customers domain lets users work with customers.

### List customers [/customers]

The List customers screen allows users to search customers
and select a customer to work with.

- EditForm Customer criteria

	User enters criteria to find a customer.

	- name - Find customer by name.

- ReadOnlyTable Customer list

	The system displays customers matching the criteria entered by the user.

	- name - Customer name
	- taxNo - Tax number
	- [View](/customers/detail "View customer detail")

- ReadOnlyForm

	- [Create](/customers/new "Create new customer")

### Create customer [/customers/new]

- EditForm Create customer

	> The create customer form has 3 sections: customer, address and contact.

	- EditForm Customer
	
		Customer data.

		- taxNo - Tax number
	
			Format: 2 upper-case letters (A-Z), 
			2-12 upper-case letters or numbers (A-Z, 0-9).
	
		- [Load](. "Verify tax number and load customer data")
		
			> Use dot `.` as the target of a `link` that does not navigate to other screen.
			>
			> Specify the system functionality of the _Load_ button:

			1. System verifies the tax number is valid and pre-fills the following fields (if empty):
	
				- `name`
				- `country`
				- `city`
				- `street`
				- `postalCode`
			
			2. If tax number is **invalid**, system displays **error** 
			but lets the user **continue** with the invalid tax number.
			
			3. If tax number **could not be verified**, system displays **warning**.
	
		- name (text, required) - The name of the customer
		
		- invoiceMaturity: 30, 60, 90 (select, required) - Invoice maturity
		
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

		1. If a customer with the `taxNo` already exists: system displays **error**.
		
		2. System creates new customer.

	- [Cancel](/customers "Return back to Customer list")
