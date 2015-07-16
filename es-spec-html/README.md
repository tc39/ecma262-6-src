# es-spec - Convert the ECMAScript Language Specification to HTML

This directory contains the artifacts use to convert the .docx source of an ECMA-262 spec. to html.  It’s original author was Jason Ordendorff.

To convert a .docx file, first copy into this directly using the name `es6-draft` or `es6-final`.  


To run the program:

    ./es-spec.py es6-draft.docx
or
    ./es-spec.py es6-final.docx

Note: Python 3 is required.

The directory `6.0-template` is a model for how the html version is distributed. First copying the model directory to create a distribution directory. Then copy the `es6-final.html` or `es6-draft.html` file produced using spec.py into the distribution directory as `index.html`.  When producing the final distribution for the Ecma web site, the Google Analytics script in `ecma-analytics` need to be manually copied as the last sub-element of the `<head>` element.


## About this program

**Architecture:** The program is in four parts:

  * Load the Word document (`docx.py`)
  * Convert it to extremely rough HTML+CSS (`transform.py`)
  * Apply a series of transformations, ranging from minor tweaks to
    very fancy algorithms, to the HTML (`fixups.py`)
  * Dump the resulting HTML document (`htmodel.py`)

Most of the interesting work, and most of the bugs, are in `fixups.py`.

**Fragility:** The script is quite sensitive to the input document and
will throw an exception and give up if the document isn't exactly as
expected.  It's been hard to balance (a) being "liberal in what you
accept" with (b) making sure fixups do not break silently, but rather
get the user's attention, when the input document changes in unexpected
ways.

**Debugging:** If a directory named `_fixup_log` exists under the
current directory, the script dumps the whole halfway-transformed
document to a file in that directory after each fixup.
