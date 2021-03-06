symphonize tests
===
Description: This is a simple markdown file for describing what tests are in which files and which file is setup to test what. All files that aren't listed are part of the set of *tests* that are being deprecated.

**Test Files:**

 * *_testing.js* - Simple library to ensure that *mocha* and *should* are included. If these fail then likely an **npm install** needs run to pull in the libraries.
 * *_orchestrate_key.js* - Simple object constructor test and verification of object constructors.
 * *_dispenser.js* - Simple object constructor test and verification of object constructors.
 	 * *_dispenser_orchestrate.js* - Functional integration tests for reading and writing verification to Orchestrate.io.
 	 * *_dispenser_console.js* - Functional integration tests for writing verification to the console.
 * *_symphonize.js* - Simple object constructor test and verification of object constructors.
  	 * *_symphonize_configuration.js* - Tests to verify configuration read from constructor or from file.
  	 * *_symphonize_configuration_parameters.js* - Tests to verify if the configuration passed in has defaults set and is read correctly.
  	 * *_symphonize_data_generation.js* - Tests to verify the data is returned for generated data based on the parameters passed in from configuration.
