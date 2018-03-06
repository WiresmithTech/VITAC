# VITAC README #


### What is VITAC? ###

VI Tester Advanced Comparisons (VITAC) provides some more advanced comparison VIs to support use of VI tester in unit testing.

If you are already using VI tester you can substitute some of the test VIs for these to get:

* Comparisons not supported e.g. 1D arrays.
* Better reporting e.g. where in a string is a failure.


### How do I get set up? ###

A VIPC file is provided in the releases section of this repository. Install this using VI package manager 2014 or later to use.

The project supports LabVIEW 2015 and later.

### Available Functions ###

#### Pass If Equal 1D Array ####

![pass if equal conn pane](docs/images/passifequal1darrayconpane.png?raw=true)

Compares two 1D numeric arrays and returns a pass/fail if any elements exceed the provided delta value (default = 0)

The results string will identify the numbers that don't match as well as the array index.

The VI takes EXT but has been tested to work with coerced SGL, DBL and integers.

#### Pass If Equal String ####

![pass if equal string conn pane](docs/images/passifequalstring.png?raw=true)

Compares two strings and passes if they match.

The results string will tell you which characters don't match (with slash code display) and provide an excerpt around this point for context.

#### Pass If Matches Regular Expression ####

![pass if matches conn pane](docs/images/passifmatchesstring.png?raw=true)

Compares a string to a regular expression and passes if it matches. This VI uses the same PCRL regular expressions as the matches pattern VI.

The results string will include the full string and regex if it fails.

### Available Templates ###

In addition to the comparison VIs we have included some templates that we use at Wiresmith Technology to produce better tests.

#### Given, When, Then ####

Given, When, Then drops a flat sequence structure with four frames designed to make tests much easier to read and understand. They are:

* Given: The test preconditions.
* When: The VI/procedure being tested.
* Then: Where you perform your comparisons and check your results.
* Clean Up: A convenient place to close references etc. without interfering with the VI Tester error chain.

Learn more at [https://devs.wiresmithtech.com/blog/given-when-then/](https://devs.wiresmithtech.com/blog/given-when-then/)

![given when then complex example](docs/images/givenwhenthencomplexexample.png?raw=true)

#### Test Event Response ####

This is a template for testing that an event has fired. You should drop it into the "then" case for comparisons. Either remove the dynamic registration functions or move the event registration to the Given case.

![dynamic event test template](docs/images/dynamiceventtestvitester.png?raw=true)

Learn more at [https://devs.wiresmithtech.com/blog/testing-events-vi-tester/]( https://devs.wiresmithtech.com/blog/testing-events-vi-tester/)

### Usage Examples ###

A project is installed into the LabVIEW example finder showing usage of each component as individual tests. To run them:

1. Search the example finder for VITAC and load the project.
2. Open VI tester and run the tests.

You can open each test and play with the values to try different scenarios.

### Future Work ###

This is very much an early stage library. Some additional features have been considered but most currently have workarounds with the above support. We will look to add to this in the future though.

* Timestamp comparisons (Workaround: Convert to numbers and use native passIfEquals.vi or Pass If Equal 1D array).
* 2D/nD Array. This is very hard to make expandable so currently I recommend just looping over 1D array comparison. Could consider 2D array in the future.
* Waveform comparison. (Workaround: Split parts and use other comparison VIs.)
* Error Comparions for codes and displayable text. (Workaround: Split the error and use Pass If Matches Regular Expression on the source string)

### Contribution guidelines ###

Feel free to fork this project to fix any bugs. If you have ideas that you want to contribute then create an issue in the issue log and we can work together to get it into the library.

The project source is in LabVIEW 2015 SP1, please use this version for edits.

### Who do I talk to? ###

For support, please create an issue on this page so we can work through the problem.

This project was setup by James McNally at Wiresmith Technology. You can get in contact on here as JamesMc86, NI forums as JamesMcN or twitter @jamesmc86
