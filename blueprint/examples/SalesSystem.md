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

	> A `list item` starting with keyword `EditForm` specifies a form with editable fields.
	>
	> The _Customer criteria_ editable form specifies the criteria for
	> finding customers.

	User enters criteria to find a customer.

	> Use `embedded list items` to specify **fields** of the form.

	- name (text) - Find customer by name. Case-insensitive, starts-by match.

- ReadOnlyTable Customer list

	> This `list item` specifies a read-only UI table that presents multiple records.
	> The records are typically displayed as rows in a table.
	>
	> (It may be a table with explicitly separate and labelled columns,
	> or it may also be a simple list of rows where each row presents the data
	> of the record in such a way as to make the meaning of each piece of data obvious.)

	The Customer list displays customers matching the criteria entered by the user.

	> The `embedded list items` of a table specify the data columns in the UI table.

	- name - Customer name
	- taxNo - Tax number

- ReadOnlyForm

	> This anonymous read-only form wraps the following button.

	- [Create](/customers/new "Create new customer")
	
		Use `links` to represent buttons or HTML links.
		A `link` refers to a page by its code.

### Create customer [/customers/new]

Create customer page lets the user create a new customer record.

> Use an `EditForm` to specify an editable form 
> and then use `list items` within the form to specify the fields of the form.

- EditForm Create customer

	- taxNo (text) - Tax number
	- name (text, required) - The name of the customer
