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

**The UI of the REAL application will look different.**
This document does NOT specify the layout of the screens (how the elements will be arranged).
It does NOT specify the graphical look of the screens either.
Both of these will be defined by a graphical designer in a process separate from this document.
The aim of this documentation is to specify the functionality of the system
and the screens presented here only illustrate the functionality,
they do not attempt to match the target look and feel of the system.

This functional specification is maintained by Andy Thor,
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
> - Forms and tables can be nested within other form.
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

	- Name (text)

	> A field specification starts with the **label** of the field.
	>
	> Use parentheses to specify the **type** of the field. The supported types are:
	>
	> - `text`: plain text field
	> - `password`: text field with the value hidden
	> - `date`: a text field aiding the user to enter a date value (possibly using a date-picker)
	> - `time`: a text field aiding the user to enter a time value (possibly using a time-picker)
	> - `multiLine`: multi-line text field
	> - `checkbox`: a checkbox field, boolean value
	> - `select`: a dropdown / combobox field that lets the user select a single value from a list of available values
	> - `radios`: list of radio buttons to select a single value from a list of fixed values
	> - `multiSelect`: a dropdown / combobox field that lets the user select multiple values from a list of available values
	> - `checkboxes`: list of checkboxes to select multiple values from a list of fixed values
	>
	> The `text` type is default, so it can actually be omitted in the _Name_ field specification above.

	- EAN
	- Status (select: Active, Disabled)

		> Specify the values of a `select` field after a colon.
		> Multiple values are separated with a comma.

- ReadOnlyTable Product list

	> This `list item` specifies a **read-only** UI **table** that presents multiple records.
	> The records are typically displayed as rows in a table.

	The system displays products matching the criteria entered.
	For text fields, system performs case-insensitive, starts-by match.
	System starts by displaying first page of matching criteria.

	> The `embedded list items` of a table specify the **columns** in the UI table.

	- Name

		> Line items embedded within a column specify the values for the rows in the table:

		- T-shirt Orange
		- T-shirt Tutti Frutti
		- T-shirt Free
		- T-shirt Hipster
		- Cookies Chocolate Ecuador
		- Cookies Chocolate Venezuela
		- Cookies Orange
	- EAN
		- 70107773572
		- 70115256941
		- 70112074810
		- 70112074810
		- 70114765149
		- 70108874916
		- 70108669294
	- Status
		- Active
		- Active
		- Active
		- Active
		- Disabled
		- Active
		- Active
	- Retail price
		- 9.99
		- 9.99
		- 9.99
		- 9.99
		- 2.89
		- 2.89
		- 2.89
	- [View](/products/detail "View product detail")

		> Use a `link` to represent a **button**.
		>
		> A button can either navigate to another screen,
		> perform some functionality, or do both of these.
		>
		> A button **refers** to another screen 
		> by using the screen's code as the `target` of the `link`.

- ReadOnlyForm

	> This anonymous read-only form wraps the following buttons
	> on the _List products_ screen.

	- [Next]()

		> Specify the system functionality on the _Next_ button.
		
		System loads next page of matching records and adds them to the table.

	- [Create](/products/new "Create new product")

### Create product [/products/new]

Create products screen lets the user create a new product record.

> Use an `EditForm` to specify an editable form 
> and then use `list items` within the form to specify the fields of the form.

- EditForm New product

	- Name (required text)
		
		> Specify the **status** of the field before its type.
		> The supported status values are:
		>
		> - `readOnly`
		> - `optional`
		> - `required` = `*`
		>
		> On read-only forms and tables, the `readOnly` status is the default.
		> On editable forms and tables, the `optional` status is the default.
		>
		> A star is equivalent to required.
		>
		> The status can also be specified without the type as in the following field.

	- EAN (*)
	- COGS (*) - Cost of goods sold, the buying price.
			
		> Specify the **hint** of the field after a dash.
		> A hint is displayed on the form to the user as an explanation related to the field.
	
	- Retail price (*)
	- VAT rate (*)

	- [Save](/products/detail)
		1. If a product with the EAN code already exists: system displays **error**.
		2. System sets status = Active.
		3. System creates new product.

	- [Cancel](/products "Return back to Product list")

### Product detail [/products/detail]

- ReadOnlyForm Product

	- Name: T-shirt Orange

		> Specify the value of the field after a colon.

	- Status: Active
	- EAN: 70107773572
	- COGS: 3.54
	- Retail price: 9.99
	- VAT rate: 15 %

	- [Edit](/products/detail/edit "Edit the product")
	- [Disable]()
	
		Enabled for status active.
		
		1. System sets status disabled.

	- [Activate]()
	
		Enabled for status disabled.
		
		1. System sets status active.

	- [Cancel](/products "Return back to Product list")

### Edit product [/products/detail/edit]

- EditForm Edit product

	- Name (*): T-shirt Orange
	- EAN (*): 70107773572
	- COGS (*): 3.54
	- Retail price (*): 9.99
	- VAT rate (*): 15

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

	- Name

- ReadOnlyTable Customer list

	The system displays customers matching the criteria entered by the user,
	sorted by number of orders they have in descending order.

	- Name
		- Gauss GmbH.
		- Poisson Denis
		- Newton Inc.
		- Fibonacci srl.
	- Tax number
		- DE56874646
		- FR2776987643
		- GB02264641
		- IT33656477
	- [View](/customers/detail "View customer detail")
	
		> Button specified in place of a table column will be replicated into each table row.

- ReadOnlyForm
	- [Next]()

		System loads next page of matching records and adds them to the table.

	- [Create](/customers/new "Create new customer")

### Create customer [/customers/new]

- EditForm Create customer

	The create customer form has 3 sections: customer, address and contact.
	This guarantees that a new customer will have at least one address and contact defined.
	More addresses and contacts can be then added to the customer.

	- EditForm Customer
	
		Customer data.

		- Tax number - Including country prefix, without spaces.
	
			Format: 2 upper-case letters (A-Z), 
			2-12 upper-case letters or numbers (A-Z, 0-9).

			> Use an embedded paragraph to further specify the field.
	
		- [Load](. "Verify tax number and load customer data")
		
			> Use dot `.` as the target of a `link` that does not navigate to other screen.
			>
			> Specify the system functionality of the _Load_ button:

			1. If tax number is **valid**, system pre-fills the following fields (if empty):
	
				- Name
				- Country
				- City
				- Street
				- Postal code
			
			2. If tax number is **invalid**, system displays **error** 
			but lets the user **continue** with the invalid tax number.
			
			3. If tax number **could not be verified**, system displays **warning**.
	
		- Name (*)
		- Invoice maturity (* select: 30, 60, 90)
		- Web - URL of the customer's web site

	- EditForm Address
	
		Customer address data.

		- Country (*)
		- City (*)
		- Street
		- Postal code

	- EditForm Contact
	
		Customer contact data.
		
		- Salutation (select: Mr, Ms)
		- Last name (*)
		- First name
		- Work phone
		- Mobile phone
		- Email
		
		One of Work phone, Mobile phone, Email is required.

	- [Save](/customers/detail)

		1. If a customer with the Tax number already exists: system displays **error**.
		
		2. System creates new customer.

	- [Cancel](/customers "Return back to Customer list")

### Customer detail [/customers/detail]

- ReadOnlyForm Customer
	- Name: Gauss Friedrich
	- Tax number: DE56874646
	- Invoice maturity: 60
	- Web
	- [Edit](/customers/detail/edit "Edit the customer")
	- [Cancel](/customers)

- ReadOnlyList Addresses
	- Country
		- Germany
		- Germany
	- City
		- Oberbach
		- Unterhofen
	- Street
		- Kirchgasse 5
		- Rathausplatz 3
	- Postal code
		- 23478
		- 65421
	- [Edit]()

		The screen to edit customer address needs to be specified.

- ReadOnlyForm
	- [Create address]()

		The screen to create new customer address needs to be specified.

- ReadOnlyList Contacts
	- Salutation
		- Mr
	- Last name
		- Gauss
		- Redel
	- First name
		- Friedrich
	- Work phone
		- 
		- 777333111
	- Mobile phone
		- 333555777
	- Email
	- [Edit]()

		The screen to edit customer contact needs to be specified.

- ReadOnlyForm
	- [Create contact]()

		The screen to create new customer contact needs to be specified.

### Edit customer [/customers/detail/edit]

- ReadOnlyForm Customer

	- Name (*): Gauss Friedrich
	- Tax number: DE56874646
	- Invoice maturity (* select: 30, 60, 90): 60
	- Web - URL of the customer's web site
	- [Save](/customers/detail "Edit the customer")
	- [Cancel](/customers/detail)


## Orders

Maintain customer orders.

### List orders [/orders]

Orders are sorted by time created in descending order.

- EditForm Order criteria
	- Order number
	- Status (select: Created, Confirmed, Closed, Invoiced)
	- Customer
- ReadOnlyTable Order list
	- Order number
		- 1236 0116
		- 1224 1215
		- 1215 1115
		- 1213 1015
		- 1201 1015
	- Status
		- Created
		- Confirmed
		- Closed
		- Invoiced
		- Invoiced
	- Customer
		- [Gauss GmbH.](/customers/detail)
		- [Gauss GmbH.](/customers/detail)
		- [Poisson Denis](/customers/detail)
		- [Newton Inc.](/customers/detail)
		- [Fibonacci srl.](/customers/detail)
	- [View](/orders/detail)
- ReadOnlyForm
	- [Next]()

		System loads next page of matching records and adds them to the table.

	- [Create](/orders/new)

### Create order [orders/new]
- EditForm
	- Customer (* select: Gauss GmbH., Poisson Denis, Newton Inc., Fibonacci srl.)
	- Date received (* date): 12/31/2015

		System pre-fills with current date.

	- Comment (multiLine)
	- [Save](/orders/detail)
		1. System sets status = Created.
		2. System creates new order.

### Order detail [/orders/detail]
- ReadOnlyForm Order
	- Order number: 1236 0116
	- Status: Created
	- Customer: [Gauss GmbH.](/customers/detail)
	- Date received: 12/31/2015
	- Comment
- ReadOnlyTable Line items
	- Product
		- T-shirt Orange
		- T-shirt Hipster
		- Cookies Orange
	- Unit price
		- 9.99
		- 9.99
		- 2.89
	- Quantity
		- 1
		- 2
		- 5
	- Price
		- 9.99
		- 19.98
		- 14.45
	- VAT
		- 1.5
		- 3
		- 2.17
	- Item total
		- 11.49
		- 22.98
		- 16.62
- ReadOnlyForm Order totals
	- Total price: 44.42
	- Total VAT: 6.67
	- Order total: 51.09
