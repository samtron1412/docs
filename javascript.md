[TOC]

# Overview



# Code pattern
## Prototype
Use to code plugin javascript

## OOP Coding
### The module
First we declare an javascript object

```javascript
var s, loginApp = {

};
```

### Settings
The settings function contains all significant elements (DOM nodes), static variables and things need for global.

```javascript
$(document).ready(function(){
	var setting = {
		loginForm: $('#loginForm'),
		userId: $('input[name=userId]'),
		password: $('input[name=password'),
		errorMessage: $('span.errorMessage')
	};
});
```

### Init function
To "kick things off" we'll have just only one function be called. This will be consistent across all modules, so you know exactly where to look when you start reading the code and figuring out what happens when.

We will pass setting variables to initial funciton for get all DOM nodes:

```javascript
var s, loginApp = {
	init: function(param){
		s = param;
	};
};
```

### Binding UI action
We would have a function just for binding the UI events. You never write any code that "does stuff" when you bind, you just do the binding and then call another appropriately named sub-function.

BindingUIAction will be called in initial function for "kick things off"

```javascript
var s, loginApp = {
	init: function(){
		s = this.setting;
		this.bindUIActions();
	},

	bindUIActions: function(){
		s.loginForm.validate();
	}
};
```

### Validation
#### I. Need add jquery plugin validate on page
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>Login Page</title>
    <link rel="stylesheet" type="text/css" href="{{urlResource('assets/css/lib/bootstraps/bootstrap.css')}}">

    <!--[if lt IE 9]>
    <script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
    <script src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js"></script>
    <![endif]-->
    <script src="{{urlResource('assets/js/lib/jquery/jquery-1.11.2.js')}}"></script>
    <script src="{{urlResource('assets/js/lib/bootstraps/bootstrap.js')}}"></script>

    <script src="{{urlResource('assets/js/lib/jquery/jquery.validate.js')}}"></script>

</head>
```

#### II. Call validate function on form element need to validate.
```javascript
s.loginForm.validate({
	onfocusout: function(element){ $(element).valid(); }
});
```

The onfocusout function help to execute validate element on blur event.

#### III. Validate Properties
##### 1. `rules`: Read, add and remove rules for an form's child element.
Example:

```javascript
s.userId.rules("add", {
	required: true,
	maxlength: 20
});
```

**Rules properties**
- Makes the element required: `required: (true or false)`
- Request a remote resource to check the element for validity: `remote: {...}`
Example: Makes the email field required, is an email and does a remote request to check if the given email address is available or not.

```javascript
$( "#myform" ).validate({
  rules: {
    email: {
      required: true,
      email: true,
      remote: {
        url: "check-email.php",
        type: "post",
        data: {
          username: function() {
            return $( "#username" ).val();
          }
        }
      }
    }
  }
});
```
- Min length: `minlength: (number)`
- Max length: `maxlength: (number)`
- Range length: `rangelength: (array of range)`
- Valid email: `email: (true or false)`
- Valid url: `url: (true or false)`
- Date: `date: (true or false)`
- Decimal number: `number: (true or false)`
- Digits only: `digits: (true or false)`
- Credit card number: `creditcard: (true or false)`

#### Some Helper function
1. errorClass: "class name"
2. wrapper: "html element"
3. highlight: function(element, errorClass, validClass)
4. unhighlight: function(element, errorClass, validClass)

Example

```javascript
var validator = s.loginForm.validate({
	onfocusout: function(element) { $(element).valid(); },
	wrapper: "span",
	errorClass: "text-danger",
	highlight: function(element, errorClass, validClass) {
		$(element).closest('div').addClass('has-error');
	},
	unhighlight: function(element, errorClass, validClass){
		$(element).closest('div').removeClass('has-error');
	}
});
```

#### About Datatablles plugin
Use datatables: `$('#employeeTable').DataTable();`

Setting

```javascript
$('#employeeTable').DataTable({
	scrollY: 300,
	paging: false
});
```

Please visit here for full options: https://datatables.net/reference/option/

# [JavaScript engine](https://en.wikipedia.org/wiki/JavaScript_engine)
A JavaScript engine is a virtual machine which interprets and executes JavaScript. Although there are several uses for a JavaScript engine, it is most commonly used in web browsers

