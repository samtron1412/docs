[TOC]

# 1. Angular Overview

- AngularJS is a JavaScript framework. It can be added to an HTML page with a `<script>` tag.

- AngularJS extends HTML attributes with **Directives**, and binds data to HTML with **Expressions**.

- AngularJS is distributed as a JavaScript file, and can be added to a web page with a script tag:

```html
<script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js"></script>
```

- It is used in Single Page Application (SPA) projects.

## 1.1 Philosophy
- Is built around the belief that **declarative programming** should be used for building **user interfaces and connecting software components**, while **imperative programming** is better suited to defining an **application's business logic**.

# 2. AngularJS Explain Work Flow

Angular's HTML compiler allows the developer to teach the browser **new HTML syntax**. The compiler allows you to attach behavior to any HTML element or attribute and even create new HTML elements or attributes with custom behavior. Angular calls these behavior extensions **directives**.

## 2.1 Initialization
Angular initializes automatically upon DOMContentLoaded event or when the angular.js script is evaluated if at that time document.readyState is set to 'complete'. At this point Angular looks for the ng-app directive which designates your application root. If the ng-app directive is found then Angular will:

 - load the module associated with the directive.
 - create the application injector
 - compile the DOM treating the ng-app directive as the root of the compilation. This allows you to tell it to treat only a portion of the DOM as an Angular application.

**Note:**  You can use data-ng-, instead of ng-, if you want to make your page HTML valid.

# 3. AngularJS Expressions
AngularJS binds data to HTML using Expressions.

AngularJS expressions are written inside double braces: `{{ expression }}`.

AngularJS expressions bind AngularJS data to HTML the same way as the **ng-bind directive**.

**AngularJS expressions** are much like **JavaScript expressions**: They can contain literals, operators, and variables.

Example:

With expression:


	   <div ng-app="" ng-init="person={firstName:'John',lastName:'Doe'}">
	   	   
	   	   	<p>The name is {{ person.lastName }}</p>`
	   	   
	   	</div>


With ng-bind:

	
	    <div ng-app="" ng-init="person={firstName:'John',lastName:'Doe'}">
	
			<p>The name is <span ng-bind="person.lastName"></span></p>
	
		</div>

An AngularJS expression must be inside a scope.

# 4. AngularJS Applications

AngularJS **modules** define AngularJS applications.

AngularJS **controllers** control AngularJS applications.

The **ng-app directive** defines the application.The ng-app directive defines the root element of an AngularJS application.

The **ng-controller directive** defines the controller.

			<div ng-app="myApp" ng-controller="myCtrl">
		
				First Name: <input type="text" ng-model="firstName"><br>
				Last Name: <input type="text" ng-model="lastName"><br>
				<br>
				Full Name: {{firstName + " " + lastName}}
		
			</div>
		
			<script>
				var app = angular.module('myApp', []);
				app.controller('myCtrl', function($scope) {
				    $scope.firstName= "John";
				    $scope.lastName= "Doe";
				});
			</script>

# 5. AngularJS Directives
## 5.1 ng-app Directive
The **ng-app directive** defines the root element of an AngularJS application.
The ng-app directive will **auto-bootstrap (automatically initialize)** the application when a **web page is loaded**.
ng-app can have a value (like ng-app="myModule"), to connect code modules.

	<div ng-app="" ng-init="firstName='John'">

		<p>Name: <input type="text" ng-model="firstName"></p>
		<p>You wrote: {{ firstName }}</p>

	</div>

The ng-app directive also tells AngularJS that the <div> element is the "owner" of the AngularJS application.


## 5.2 ng-model Directive
The ng-model directive binds the value of HTML controls (input, select, textarea) to application data.

The ng-model directive can also:
	- Provide type validation for application data (number, email, required).
	- Provide status for application data (invalid, dirty, touched, error).
	- Provide CSS classes for HTML elements.
	- Bind HTML elements to HTML forms.
	- 
## 5.3 ng-controller Directive
### 5.3.1 Not module
The ng-controller directive defines a controller.

	<div ng-app="myApp" ng-controller="myCtrl">

		First Name: <input type="text" ng-model="firstName"><br>
		Last Name: <input type="text" ng-model="lastName"><br>
		<br>
		Full Name: {{firstName + " " + lastName}}

	</div>

	<script>
		var app = angular.module('myApp', []);
		app.controller('myCtrl', function($scope) {
	    	$scope.firstName = "John";
	    	$scope.lastName = "Doe";
	    	$scope.fullName = function() {
        		return $scope.firstName + " " + $scope.lastName;
    		}
		});
	</script>

Example explained:

The AngularJS application is defined by **ng-app**. The application runs inside a div.

The **ng-controller** directive defines a controller.

The myCtrl function is a JavaScript function.

AngularJS will invoke the controller with a $scope object.

In AngularJS, $scope is the application object (the owner of application variables and functions).

The controller creates two properties (variables) in the scope (firstName and lastName).A controller can also have methods (fullname)

The **ng-model directives** bind the input fields to the controller properties (firstName and lastName).

### 5.3.2 Module
In larger applications, it is common to store controllers in external files.

	angular.module('myApp', []).controller('personCtrl', function($scope) {
	    $scope.firstName = "John",
	    $scope.lastName = "Doe",
	    $scope.fullName = function() {
	        return $scope.firstName + " " + $scope.lastName;
	    }
	})

Define name with personController.js after that include in html with script tag.

	<script src="personController.js"></script>

Or you can slipt the module and the controllers in JavaScript files.

`myApp.js`

	var app = angular.module('myApp', []);

**Note:** The [] parameter in the module definition can be used to define dependent modules.

`personCtrl.js`

	app.controller('personCtrl', function($scope) {
	    $scope.firstName = "John",
	    $scope.lastName = "Doe",
	    $scope.fullName = function() {
	        return $scope.firstName + " " + $scope.lastName;
	    }
	});

And include to html file

	<!DOCTYPE html>
	<html>

	<head>
	<script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js"></script>
	</head>

	<body>

	<div ng-app="myApp" ng-controller="personCtrl">
	{{ firstName + " " + lastName }}
	</div>

	<script src="myApp.js"></script>
	<script src="personCtrl.js"></script>

	</body>
	</html>

So define many controller as you can, and include to myApp module.
It is common in AngularJS applications.

## 5.4 ng-repeat Directive
The ng-repeat directive repeats an HTML element:

	<div ng-app="" ng-init="names=['Jani','Hege','Kai']">
	  <ul>
	    <li ng-repeat="x in names">
	      {{ x }}
	    </li>
	  </ul>
	</div>

The ng-repeat directive clones HTML elements once for each item in a collection (in an array).

## 5.5 ng-disabled Directive
The ng-disabled directive binds AngularJS application data to the disabled attribute of HTML elements.

	<div ng-app="">

	<p>
	<button ng-disabled="mySwitch">Click Me!</button>
	</p>

	<p>
	<input type="checkbox" ng-model="mySwitch">Button
	</p>

	</div>

Application explained:

The ng-disabled directive binds the application data mySwitch to the HTML button's disabled attribute.

The ng-model directive binds the value of the HTML checkbox element to the value of mySwitch.

If the value of mySwitch evaluates to true, the button will be disabled.

If the value of mySwitch evaluates to false, the button will not be disabled.

## 5.6 ng-show Directive
The ng-show directive shows or hides an HTML element.

	<div ng-app="">

	<p ng-show="true">I am visible.</p>

	<p ng-show="false">I am not visible.</p>

	</div>

The ng-show directive shows (or hides) an HTML element based on the value of ng-show.

You can use any expression that evaluates to true or false:

	<div ng-app="">

	<p ng-show="hour > 12">I am visible.</p>

	</div>

## 5.7 ng-hide Directive
The ng-hide directive hides or shows an HTML element.

## 5.8 ng-include Directive
With AngularJS, you can include HTML content, using the ng-include directive

	<body>

	<div class="container">
	  <div ng-include="'myUsers_List.htm'"></div>
	  <div ng-include="'myUsers_Form.htm'"></div>
	</div>

	</body>

**Note** Becareful with angular scope when using include.

## 5.9 Custom Directive.
Here's an simple custom directive declared with a Directive Definition Object:


		var myModule = angular.module(...);

		myModule.directive('directiveName', function factory(injectables) {
		  var directiveDefinitionObject = {
		    priority: 0,
		    template: '<div></div>', // or // function(tElement, tAttrs) { ... },
		    // or
		    // templateUrl: 'directive.html', // or // function(tElement, tAttrs) { ... },
		    transclude: false,
		    restrict: 'AEC',
		    scope: false,
		    require: 'siblingDirectiveName', // or // ['^parentDirectiveName', '?optionalDirectiveName', '?^optionalParent'],
		    compile: function compile(tElement, tAttrs, transclude) {
		      return {
		        pre: function preLink(scope, iElement, iAttrs, controller) { ... },
		        post: function postLink(scope, iElement, iAttrs, controller) { ... }
		      }
		      // or
		      // return function postLink( ... ) { ... }
		    }
		  };
		  return directiveDefinitionObject;
		});

To knowledged about option please visit this link: https://docs.angularjs.org/guide/directive
In this document, we will only explain how a custom directive was loaded.

First when a browser renders a page, it essentially reads the HTML markup, creates a DOM and broadcasts an event when the DOM is ready.

When you include your AngularJS application code on a page using a <script></script> tag, AngularJS listens for that event and as soon as it hears it, it starts traversing the DOM, looking for an ng-app attribute on one of the elements.

When such an element is found, AngularJS starts processing the DOM using that specific element as the starting point. So if the ng-app attribute is set on the html element, AngularJS will start processing the DOM starting at the html element.

From that starting point, AngularJS recursively investigates all child elements, looking for patterns that correspond to directives that have been defined in your AngularJS application.

How AngularJS processes the element depends on the actual directive definition object. You can define a compile function, a link function or both. Or instead of a link function you can opt to define a pre-link function and a post-link function.

So what is difference between all those functions and why or when should you use them?

Consider the following HTML markup:

	<level-one>  
    	<level-two>
        	<level-three>
            	Hello {{name}}         
        	</level-three>
    	</level-two>
	</level-one>

and the following JavaScript:

	var app = angular.module('plunker', []);

	function createDirective(name){  
	  return function(){
	    return {
	      restrict: 'E',
	      compile: function(tElem, tAttrs){
	        console.log(name + ': compile');
	        return {
	          pre: function(scope, iElem, iAttrs){
	            console.log(name + ': pre link');
	          },
	          post: function(scope, iElem, iAttrs){
	            console.log(name + ': post link');
	          }
	        }
	      }
	    }
	  }
	}

	app.directive('levelOne', createDirective('levelOne'));  
	app.directive('levelTwo', createDirective('levelTwo'));  
	app.directive('levelThree', createDirective('levelThree'));  


Go to this link and see on console to see the output
http://plnkr.co/edit/5rbeFfKO7QUM2PGkK3Qy?p=preview

**Let's analyze**

	// COMPILE PHASE
	// levelOne:    compile function is called
	// levelTwo:    compile function is called
	// levelThree:  compile function is called

	// PRE-LINK PHASE
	// levelOne:    pre link function is called
	// levelTwo:    pre link function is called
	// levelThree:  pre link function is called

	// POST-LINK PHASE (Notice the reverse order)
	// levelThree:  post link function is called
	// levelTwo:    post link function is called
	// levelOne:    post link function is called

Notice how the order of the compile and pre-link functions calls is identical but the order of the post-link function calls is reversed.

So at this point we can already clearly identify the different phases, but what is the difference between the compile and pre-link function?

To dig a bit deeper, let's update our JavaScript so it also outputs the element's DOM during each function call:

	var app = angular.module('plunker', []);

	function createDirective(name){  
	  return function(){
	    return {
	      restrict: 'E',
	      compile: function(tElem, tAttrs){
	        console.log(name + ': compile => ' + tElem.html());
	        return {
	          pre: function(scope, iElem, iAttrs){
	            console.log(name + ': pre link => ' + iElem.html());
	          },
	          post: function(scope, iElem, iAttrs){
	            console.log(name + ': post link => ' + iElem.html());
	          }
	        }
	      }
	    }
	  }
	}

	app.directive('levelOne', createDirective('levelOne'));  
	app.directive('levelTwo', createDirective('levelTwo'));  
	app.directive('levelThree', createDirective('levelThree'));

Ok Refresh browser and see console again.

Link for see demo
http://plnkr.co/edit/KtMs0H1pBsrOmXrFh9nf

Printing the DOM reveals something very interesting: the **DOM is different** during the **compile** and **pre-link** function.

OK, we will see what is happening here?
So when AngularJS starts traversing the DOM, it bumps into the <level-one> element and knows from its directive definition that some action needs to be performed.

Because a compile function is defined in the levelOne directive definition object, it is called and the element's DOM is passed as an argument to the function.

If you look closely you can see that, at this point, the DOM of the element is still the DOM that is initially created by the browser using the original HTML markup.

Once the compile function of the levelOne directive has run, AngularJS **recursively** traverses deeper into the DOM and repeats the same compilation step for the <level-two> and <level-three> elements.

Before digging into the pre-link functions, let's first have a look at the post-link functions.

After AngularJS travels down the DOM and has run all the compile functions, it traverses back up again and runs all associated post-link functions.

The DOM is now traversed in the opposite direction and thus the post-link functions are called in reverse order. So while the reversed order looked strange a few minutes ago, it is now starting to make perfect sense.

This reverse order guarantees that the post-link functions of all **child elements** have run by the time the post-link function of the **parent element** is run.

So when the post-link function of <level-one> is executed, we are guaranteed that the post-link function of <level-two> and the post-link function of <level-three> have already run.

This is the exact reason why it is considered the safest and default place to add your directive logic.

The pre-link function is guaranteed to run on an element instance before any post-link function of its **child elements** has run.

# 6. AngularJS Filters
AngularJS filters can be used to transform data.
Filters can be added to expressions and directives using a pipe character.

- Some basic angular filter:

| Filter    | Description                             |
| -         | -                                       |
| currency  | Format a number to a currency format.   |
| filter    | Select a subset of items from an array. |
| lowercase | Format a string to lower case.          |
| orderBy   | Orders an array by an expression.       |
| uppercase | Format a string to upper case.          |

## 6.1 Adding Filters to Expressions
A filter can be added to an expression with a pipe character (|) and a filter.

		<div ng-app="" ng-controller="personCtrl">

			<p>The name is {{ lastName | uppercase }}</p>

		</div>
		
## 6.2 Adding Filters to Directives
A filter can be added to a directive with a pipe character (|) and a filter.

	<div ng-app="" ng-controller="namesCtrl">

		<p><input type="text" ng-model="test"></p>

		<ul>
		  <li ng-repeat="x in names | filter:test | orderBy:'country'">
		    {{ (x.name | uppercase) + ', ' + x.country }}
		  </li>
		</ul>

	</div>
The filter above filter selects a subset of an array

#7. AngularJS XMLHttpRequest
## 7.1 $http
$http is an AngularJS service for reading data from remote servers.

$http.get(url) is the function to use for reading server data.


	<div ng-app="myApp" ng-controller="customersCtrl"> 

	<ul>
	  <li ng-repeat="x in names">
	    {{ x.Name + ', ' + x.Country }}
	  </li>
	</ul>

	</div>

	<script>
	var app = angular.module('myApp', []);
	app.controller('customersCtrl', function($scope, $http) {
	    $http.get("http://www.w3schools.com/website/Customers_JSON.php")
	    .success(function(response) {$scope.names = response;});
	});
	</script>

**Application explained:**

The AngularJS application is defined by **ng-app**. The application runs inside a <div>.

The **ng-controller** directive names the **controller object**.

The **customersCtrl** function is a standard JavaScript **object constructor.**

AngularJS will invoke customersCtrl with a **$scope** and **$http** object.

$scope is the **application object** (the owner of application variables and functions).

$http is an **XMLHttpRequest object** for requesting external data.

**$http.get()** reads static **JSON data** from http://www.w3schools.com/website/Customers_JSON.php.

If success, the controller creates a property **names** in the scope, with JSON data from the server.

## 7.2 Cross-Site HTTP Requests
Requests for data from a different server (than the requesting page), are called cross-site HTTP requests.

Cross-site requests are common on the web. Many pages load CSS, images, and scripts from different servers.

In modern browsers, cross-site HTTP requests from scripts are restricted to same site for security reasons.

The following line, in our PHP examples, has been added to allow cross-site access.

	header("Access-Control-Allow-Origin: *");

# 8. AngularJS Events
AngularJS has its own HTML events directives.

## 8.1 ng-click Directive

	<div ng-app="myApp" ng-controller="personCtrl">

	<button ng-click="toggle()">Toggle</button>

	<p ng-hide="myVar">
	First Name: <input type="text" ng-model="firstName"><br>
	Last Name: <input type="text" ng-model="lastName"><br>
	<br>
	Full Name: {{firstName + " " + lastName}}
	</p>

	</div>

	<script>
	var app = angular.module('myApp', []);
	app.controller('personCtrl', function($scope) {
	    $scope.firstName = "John",
	    $scope.lastName = "Doe"
	    $scope.myVar = false;
	    $scope.toggle = function() {
	        $scope.myVar = !$scope.myVar;
	    };
	});
	</script>

Application explained:

The first part of the personController is the same as in the chapter about controllers.

The application has a default property (a variable): $scope.myVar = false;

The ng-hide directive sets the visibility, of a <p> element with two input fields, according to the value (true or false) of myVar.

The function toggle() toggles myVar between true and false.

The value ng-hide="true" makes the element invisible.

# 9. Module Loading & Dependencies

A module is a collection of configuration and run blocks which get applied to the application during the bootstrap process. In its simplest form the module consist of a collection of two kinds of blocks:

##9.1 Configuration blocks
- Get executed during the provider registrations and configuration phase. Only providers and constants can be injected into configuration blocks. This is to prevent accidental instantiation of services before they have been fully configured.

##9.2 Run blocks 
- Get executed after the injector is created and are used to kickstart the application. Only instances and constants can be injected into run blocks. This is to prevent further system configuration during application run time.


		angular.module('myModule', []).
		config(function(injectables) { // provider-injector
		  // This is an example of config block.
		  // You can have as many of these as you want.
		  // You can only inject Providers (not instances)
		  // into config blocks.
		}).
		run(function(injectables) { // instance-injector
		  // This is an example of a run block.
		  // You can have as many of these as you want.
		  // You can only inject instances (not Providers)
		  // into run blocks
		});

## 9.3 Creation versus Retrieval
Beware that using angular.module('myModule', []) will create the module myModule and overwrite any existing module named myModule. Use angular.module('myModule') to retrieve an existing module.

	var myModule = angular.module('myModule', []);

	// add some directives and services
	myModule.service('myService', ...);
	myModule.directive('myDirective', ...);

	// overwrites both myService and myDirective by creating a new module
	var myModule = angular.module('myModule', []);

	// throws an error because myOtherModule has yet to be defined
	var myModule = angular.module('myOtherModule');