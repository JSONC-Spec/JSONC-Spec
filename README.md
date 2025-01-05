
<!-- For license of this file, see LICENSE.md in the base dir. -->

Common JSONC Specification
==========================

*(The original version of this document can be found [here](
https://codeberg.org/JSONC-Spec/JSONC-Spec#common-jsonc-specification).)*

This is a specification of the *common JSON with Comments (JSONC) config
format* that is often seen with a `.jsonc` file extension, or sometimes
simply with a `.json` file extension. The main focus of this document
is to capture what seems to be **the most common variant that seems
most commonly implemented**, while listing some of the various spin-offs
for your information.

**What is JSONC?** JSONC is based on [JSON](
https://www.json.org/json-en.html). JSON is a format often used for
basic data exchange, and JSONC has various small additions to
make it more suitable for configuration files written by human
users. JSONC is a superset of JSON, which means all JSON is also
valid JSONC, but not the other way around.

**How can I use JSONC?** The perhaps most used implementation
of the most common JSONC dialect described in this specification
is provded by [node-jsonc-parser](
https://github.com/Microsoft/node-jsonc-parser). This variant is
also provided by [Horse64](
https://codeberg.org/Horse64/core.horse64.org). Different
variants with various changes are provided by [glaze](
https://github.com/stephenberry/glaze) and [HexDocs's JSONC
parser](https://hexdocs.pm/jsonc/JSONC.html).

> **JSONC example:**
> ```json
> {
>     // This is a JSONC example.
>     "title": "This is a test!",
>     "type": "Example document",
>     "author": "JSONC Spec writers",
> }
> ```

> **Warning**
> There are multiple differing implementations of JSONC, so not all
> features might be available in all of them. If you have implemented
> JSONC, you are encouraged to link the exact specification you
> are implementing.


Introduction to JSON
--------------------

The base of this specification is the **JSON** format.
JSON is a text format that commonly requires a **so-called
Unicode text encoding**, although some parsers might accept
other encodings.

The original JSON specification is [here](https://json.org),
although a short overview will be provided in the following.

JSON has the following elements that can be used in a nested
tree, whereas the root commonly is the **object** element type
or the **array** element type:

| **List of JSON elements:** |                                            |
|-------------|-----------------------------------------------------------|
| element     | May be any of the available elements below.               |
| object      | `{` assignments `}` **OR:** `{` `}`                       |
| array       | `[` items `]` **OR:** `[` `]`                             |
| assignments | name `:` element **OR:** assignments `,` name `:` element |
| items       | element **OR:** items `,` element                         |
| name        | string                                                    |
| boolean     | `true` **OR:** `false`                                    |
| null        | `null`                                                    |
| number      | A term matching this regex: `-?[0-9]+(\.[0-9]+)+`.        |
| string      | `"` *(inside, characters excluding newlines and `"`)* `"` |

> **Note**
> Strings may contain backslash escapes, see below.

> **Note**
> Whitespace characters in between the elements are ignored.

The **object** type is in many languages mapped to an equivalent
that may have the alternate name "dictionary" (Python) or "map" (C++).

The **array** type is in many languages mapped to an equivalent
that may have the alternate name "list" (Python) or "vector" (C++).


### JSON backslash escapes

Since JSON strings cannot contain literal newlines or literal `"` quotes,
you can insert those characters with backslash escapes that start
with a `\` character.
The commonly implemented JSON backslash escapes are escaped forward
slash `\/`, escaped backward slash `\\`, escaped quotes `\"`, escapes for
newlines `\r` (ascii 13) and `\n` (ascii 10), escapes for horizontal tabs
`\t` (ascii 9), special escape `\b` (ascii 8), special escape `\f`
(ascii 12), and unicode escapes `\u` followed by 4 (or in some
implementations up to 8) hexidecimal digits for the codepoint.


JSONC extensions
----------------

The following extensions to the JSON format are provided by the common
JSONC variant:

### Line comments with `//`

Additionally to regular JSON, a literal `//` outside of a string may start
a line comment. The line comment continues until a literal newline
character, and will be ignored by the JSONC parser:

```json
{
    // This is a line comment example.
    // { this will be ignored and be part of the line comment }
    "number": 4.0
}
```

### Block comments starting with `/*` and ending with `*/`

Additionally to regular JSON, a literal `/*` outside of a string may start
a block comment. The block comment continues until a literal `*/` is
found. Please note this means nesting doesn't work, since the first `*/`
terminates the block comment no matter how many `/*` preceded it.
Any block comment will be ignored by the JSONC parser:

```json
{
    /* This is a block comment example.
       The number after this will be picked up by the
       parser again since the block comment ended: */ "number": 4.0
}
```

### Trailing commas in **object** and **array** elements

Additionally to regular JSON, a single trailing `,` may be used
after non-empty **object** and **array** elements after their
assignments or items inside:

```json
{
    "abc": "def",
    "test": 5,  // <- This comma found here is valid JSONC.
}
```

```json
[
    1, 2, 3, 4,
    5, 6, 7, 8,  // <- This comma at the end of the line is valid JSONC.
]
```

> **Warning**
> Keep in mind that regular JSON doesn't allow such a trailing comma.
> Additionally, some of the diverging different JSONC
> specifications don't support a trailing comma either.

### Other additions found in JSONC variations

> **Warning**
> These additions aren't found in what seems to be the most common
> JSONC variant, so check with your JSONC library if these are
> available.

**Single quotes:** Some JSONC spin-offs allow using single quotes
for strings, e.g. `'This is a spin-off JSONC string variant'`, instead
of the usual `"` double quotes.

**No trailing comma:** Some JSONC spin-offs won't allow a trailing
comma.

**Strings without quotes:** Some JSONC spin-offs allow strings
without special characters and without whitespace to be put into
objects without requiring any quotes: `{some_value: 5}`

Contribute
----------

If you find errors or omissions, [please report them here](
https://codeberg.org/JSONC-Spec/JSONC-Spec/issues). You can
find the [authors of this document here](/AUTHORS.md).


