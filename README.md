
<!-- For license of this file, see LICENSE.md in the base dir. -->

# JSONC Specification

*(The original version of this document can be found
[here](https://codeberg.org/JSONC-Spec/JSONC-Spec).)*

This is a specification of the JSON with Comments (JSONC) config format
that is often seen with a `.jsonc` file extension. The main focus of
this document is to capture **the most commonly implemented** variant,
while listing some of the various spin-off for your information.

**What is JSONC?** JSONC is based on [JSON](
https://www.json.org/json-en.html). JSON is a format often used for
basic data exchange, and JSONC has various small additions to
make it more suitable for configuration files written by human
users.

**How can I use JSONC?** There are various implementations
available, the most common one likely being [node-jsonc-parser](
https://github.com/Microsoft/node-jsonc-parser).

> **JSONC example:**
> ```
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

## 

