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

### Future Work ###

This is very much an early stage library. Some additional features have been considered but most currently have workarounds with the above support. We will look to add to this in the future though.

* Timestamp comparisons (Workaround: Convert to numbers and use native passIfEquals.vi or Pass If Equal 1D array).
* 2D/nD Array. This is very hard to make expandable so currently I recommend just looping over 1D array comparison. Could consider 2D array in the future.
* Waveform comparison. (Workaround: Split parts and use other comparison VIs.)
* Error Comparions for codes and displayable text. (Workaround: Split the error and use Pass If Matches Regular Expression on the source string)

### Contribution guidelines ###

Feel free to fork this project to fix any bugs. If you have ideas that you want to contribute then create an issue in the issue log and we can work together to get it into the library.

### Who do I talk to? ###

This project was setup by James McNally at Wiresmith Technology. You can get in contact on here as JamesMc86, NI forums as JamesMcN or twitter @jamesmc86
