****
WORK IN PROGRESS

TO DO:

- DDD
- TDD

****

# fauxpas

Handle embarrassingly awkward errors with ease.

## Overview

Often when developing complex applications error handling is often overlooked or at best only partially considered. With Fauxpas you can manage, monitor and handle custom errors with ease. 

## Where to use it

Fauxpas was developed to work in either the browser or node.js.

### node.js

```
> npm install fauxpas
```
```
var fauxpas = require('fauxpas');
```

### require.js

```
require.config({
    paths: {
        "fauxpas": "path/to/fauxpas",
    }
});

define(["fauxpas"], function (fauxpas) {

	// do something

});

```

### browser

```	
	<script src="path/to/fauxpas.js" />
	
```

## Usage

### fauxpas

#### on

#### list

#### once

#### remove

#### removeAll

#### trigger

#### define

Creates a fauxpas error definition which essentially groups together a collection of errors and describes how errors should be identified and processed by fauxpas. 


```
// Based on https://dev.twitter.com/docs/error-codes-responses

fauxpas.define({

	// name:
	// Used as an internal reference by fauxpax and 
	// allows filtering

	name: 'twitter',
	
	// description:
	// User friendly description of error definition 
	
	description: 'Error definition for github errors ',
	
	// throw:
	// Should a custom JavaScript error be thrown. By default this is always set to true
	// but can be overriden on a per error basis.

	throw: true,
	
	// evidence:
	// Custom function to process current error and determine 
	// the current error code
	
	evidence: function () {
	
		// must always return result in the format
		// below
	
		return {
		
			code: '',
			reason: '',
			message
		
		};
	
	},
	
	// listener:
	// Custom listener to call whenever there is an error for this
	// definition
	
	listener: function (/* Array */ errors) {
		
		// Example of errors array passed by fauxpas
		// 
		// [{
		// 		code: '32',
		//		reason: 'Could not authenticate you',
		// 		message: 'Your call could not be completed as dialed',
		//		origin: {} // Original error
		// }]
		//
	
	}
	
	// errors:
	// Provides mappings for each possible error which needs
	// to be processed
	
	errors: {
		
		'32': {
		
			reason:  'Could not authenticate you',
			message: 'Your call could not be completed as dialed.',
			
			thows: false,
			
			// listener:
			// Triggered when ever fauxpas detects this error
			
			error <object> fauxpas error object
			
			listener: function (/* Object */ error) {
				
				// Example of error object passed by fauxpas
				// 
				// {
				// 		code: '32',
				//		reason: 'Could not authenticate you',
				// 		message: 'Your call could not be completed as dialed',
				//		origin: {} // Original error
				// }
				//
			
			}
		
		}
		
	}

});

```
> Example fauxpas error definition


## Change Log

0.1.0