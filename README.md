# SBOM - Simple Bill of Materials

**SBOM** is a really simple *BOM* generation system for *OpenSCAD*.

**SBOM** is completely driven the OpenSCAD design and generates
*reStructuredText* documents that can trivially be converted into PDF or HTML
files. **SBOM** aggregates all of the parts found in the design into a simple
tabular form.

While **SBOM** is intended for use with OpenSCAD it does not depend on this in
any way and can be used with other applications.


## SBOM Syntax

**SBOM** parses the input file for lines of the following form:

    BOM:namespace..:part:key=value,..

*   *BOM*
    *   Tell SBOM to consider this line.
*   *namespace*
    *   Categorise part in a hierarchal namespace separated by colons
        (optional).
*   *part*
    *   Name of the part type.
*   *key=value*
    *   Parameters of this part.

For example an M6 bolt may be represented by:

    BOM:hardware:bolt:size=M6,length=12

If out input file contained the above line four times then we would get a table
like this:

| #   | size | length | qty |
| --- | ---- | ------ | --- |
| A   | M6   | 12     | 4   |

The way these can be used is pretty flexible but it comes down to:

*   A BOM will contain a table for each part.
*   These tables will be organised by namespace.
*   The columns of the tables will contain the keys and aggregates values.

Every time a part is used in the design the line should be output again. We let
SBOM do the counting for us.


## Using SBOM with OpenSCAD

In OpenSCAD we can.. variables...

    echo(str("BOM:hardware:bolt:size=M", size, ",length=", length));
