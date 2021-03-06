[![Dependencies](https://david-dm.org/Adron/symphonize.png)](http://david-dm.org/Adron/symphonize)

![Symphonize.js](http://photos.adron.me/Software/Software-Development/Symphonize/i-kzTdM4Q/0/S/Symphonize-S.png "Symphonize.js")

symphonize.js
===
NOTE: This project is still a few steps away from being deployed for use via npm. However all of these instructions are written as if it is complete. Please verify that we're in a released v0.1.0 state before using the project via npm. Currently the project on npm is on v0.0.4
 
**Description:** This project is a data generation library that makes the data available as generated for display via the console or for external services like Orchestrate.io. It can be used locally or as a tool to create random data based on configuration for testing, experimentation or however or whatever you may need data for.

***How to use this project in one of your projects.***

	npm install symphonize

***How to setup this project for development.***

First fork the repository located at [https://github.com/Adron/symphonize](https://github.com/Adron/symphonize).

	git clone git@github.com:YourUserName/symphonize.git
	cd symphonize
	npm install

Using The Library
---

The intended usage is to invocate the JavaScript object and then call generate. That's it, a super simple process. The code would look like this:

	var Symphonize = require('../bin/symphonize');
	var symphonize = new Symphonize();

The basic constructor invocation like this utilizes the generate.json file to generate data from. To inject the json configuration programmatically just inject the json configuration information via the constructor.

	var configJson = {"schema":"keyvalue"};

	var Symphonize = require('../bin/symphonize');
	var symphonize = new Symphonize();

Once the Symphonize data generator has been created call the generate() method as shown.

	symphonize.generate();

That's basically it. But you say, it's supposed to do X, Y or Z. Well that's where the json configuration data comes into play. In the configuration data you can set the data fields and what they'll generate, what type of data will be generated, the specific schema, how many records to create and more.

generate.json
---
The library comes with the generate.json file already setup with a working example. Currently the generation file looks like this:

	{
	    "schema": "keyvalue", /* keyvalue, graph, event, geo */
	    "count": 20, /* X values to generate. */
	    "write_source": "console", /* console, orchestrateio and whatever other data sources that might come up. */

	    "fields": {
	        /* generates a random name. */
	        "fieldName": "name",

	        /* generates a random dice roll of a d20. */
	        "fieldTwo": "d20",

	        /* A single lorum ipsum random statement is genereated. */
	        "fieldSentence": "sentence",

	        /* A random guid is generated. */
	        "fieldGuid": "guid"
	    }
	}

**Configuration File Definitions**

Each of the configuration options that are available have a default in the configuration file. The default is listed in italics with each definition of the configuration option listed below.

 * "schema" : This is used to select what type of data structure type is going to be generated. The default is *keyvalue* for this option.
 * "count" : This provides the total records that are to be generated by the library. The default is *1* for this option.
 * "write_source" : This provides the location to output the generated data to. The default is *console* for this option.
 * "fields" : This is a JSON field within the JSON configuration file that provides configuration options around the fields, number of fields and their respective data to generate. The default is *one field*, with a default data type of *guid*. Each of the respective entries in this JSON option is a self contained JSON name and value pair. This then looks simply like this (which is also shown above in part):
	
		{
			"someBoolean": "boolean",
			"someChar": "character",
			"aFloat": "float",
			"GetAnInt": "integer",
	        "fieldTwo": "d20",
	        "diceRollD10": "d10",
	        "_string": {
	        	"fieldName": "NameOfFieldForString",
	        	"length": 5,
	        	"pool": "abcdefgh"
	        },
 		    "_name": {
	        	"fieldName": "nameFieldName",
	        	"middle": true,
	        	"middle_initial": true,
	        	"prefix": true
	        },
	        "_hash": {
	        	"fieldName": "HashFieldName",
	        	"length": 25,
	        	"casing": 'upper'
	        },
	        "fieldGuid": "guid"
	    }
 * **Fields Configuration**: For each of the fields you can either set the field to a particular data type or leave it empty. If the field name and value pair is left empty then the field defaults to *guid*. The types of data to generate for fields are listed below. These listed are all simple field and data generation types. More complex nested generation types are listed below under *Complex Field Configuration* below the simple section.
	 * "boolean": This generates a boolean value of true or false.
	 * "character": This generates a single character, such as '1', 'g' or 'N'.
	 * "float": This generates a float value, similar to something like -211920142886.5024.
	 * "integer": This generates an integer value, similar to something like 1, 14 or 24032.
	 * "d4": This generates a random integer value based on a dice roll of one four sided dice. The integer range being 1-10.
	 * "d6": This generates a random integer value based on a dice roll of one six sided dice. The integer range being 1-10.
	 * "d8": This generates a random integer value based on a dice roll of one eight sided dice. The integer range being 1-10.
	 * "d10": This generates a random integer value based on a dice roll of one ten sided dice. The integer range being 1-10.
	 * "d12": This generates a random integer value based on a dice roll of one twelve sided dice. The integer range being 1-10.
	 * "d20": This generates a random integer value based on a dice roll of one twenty sided dice. The integer range being 1-20.
	 * "d30": This generates a random integer value based on a dice roll of one thirty sided dice. The integer range being 1-10.
	 * "d100": This generates a random integer value based on a dice roll of one hundred sided dice. The integer range being 1-10.
	 * "guid": This generates a random globally unique identifier. This value would be similar to 'F0D8368D-85E2-54FB-73C4-2D60374295E3', 'e0aa6c0d-0af3-485d-b31a-21db00922517' or '1627f683-efeb-4db8-8174-a5f2e3378c87'.

 * **Complex Field Configuration**: Some fields require more complex configuration for data generation, simply because the data needs some baseline of what the range or length of the values need to be. The following list details each of these. It is also important to note that these complex field configurations do not have defaults, each value must be set in the JSON configuration or an error will be thrown detailing that a complex field type wasn't designated. Each of these complex field types is a JSON name and value parameter. The name is the passed in data type with a preceding underscore '_' to generate with the value having the configuration parameters for that particular data type.
 	
 	* "_string": This generates string data based on a *length* and *pool* parameters. Required fields for this include *fieldName*, *length* and *pool*. The JSON would look like this:
 	
 		     "_string": {
	        	"fieldName": "NameOfFieldForString",
	        	"length": 5,
	        	"pool": "abcdefgh"
	        }
	        
	    Samples of the result would look like this for the field; 'abdef', 'hgcde' or 'ahdfg'.
	* "_hash": This generates a hash based on the *length* and *upper* parameters. Required fields for this included *fieldName*, *length* and *upper*. The JSON would look like this:
	
 		     "_hash": {
	        	"fieldName": "HashFieldName",
	        	"length": 25,
	        	"casing": 'upper'
	        }
	        
	    Samples of the result would look like this for the field: 'e5162f27da96ed8e1ae51def1ba643b91d2581d8' or '3F2EB3FB85D88984C1EC4F46A3DBE740B5E0E56E'.
	* "_name": This generates a name based on the *middle*, *middle_initial* and *prefix* parameters. Required fields for this included *fieldName*, *middle*, *middle_initial* and *prefix*. The JSON would look like this:
	
 		     "_name": {
	        	"fieldName": "nameFieldName",
	        	"middle": true,
	        	"middle_initial": true,
	        	"prefix": true
	        }
	        
	    Samples of the result would look like this for the field: 'Dafi Vatemi', 'Nelgatwu Powuku Heup', 'Ezme I Iza', 'Doctor Suosat Am', 'Mrs. Suosat Am' or 'Mr. Suosat Am'.
	
**Dependencies**

In this project we've used several other libraries, all available via NPM. These projects include: [orchestrate.js](https://npmjs.org/package/orchestrate) and [chance.js](https://npmjs.org/package/chance). They'll be pulled in automatically when running npm install or when the symphonize library is included in your project. In other words this dependency list is just an FYI.

For more information on the library ping me [@adron](https://github.com/adron) or on Twitter [@Adron](http://twitter.com/adron).
Join In, Pull Requests and Getting Involved
---

 * [Issues List](https://github.com/Adron/symphonize/issues?state=open)
 * [Huboard Kanban](https://huboard.com/Adron/symphonize)
 * [Public Gihub Pages Site](http://adron.github.io/symphonize/)

[Adron](https://github.com/Adron) || [@Adron](http://twitter.com/adron) || [![Signature Logo](http://photos.adron.me/Software/Misc-Images/Logo/i-5zk96td/0/O/AH---Logo-32x32.png)](http://adron.me)
