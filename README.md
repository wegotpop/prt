# PRT

PRT (POP Rich Text) is a safe, small and strict rich text serialisation protocol
which can be used in server - client communication. The protocol is JSON
compatible.

### Table of Content

- [PRTv2.0](#prtv20)
    - [Protocol](#protocol)
    - [Example](#example)
    - [Reference Implementations](#reference-implementations)
    - [The pop-dialect](#the-pop-dialect)
        - [Dialect](#dialect)
        - [Identifiers](#identifiers)
        - [Attributes](#attributes)
            - [Generic](#generic)
            - [Specific to 0x00](#specific-to-0x00)
            - [Specific to 0x0B](#specific-to-0x0b)

- [PRTv1.0](#prtv10)
- [Lincese](#license)


## PRTv2.0

### Protocol

<pre><code><b><i>document</i></b>         ::=   { <b><i>type_pair</i></b>, <b><i>version_pair</i></b>, <b><i>dialect_pair</i></b>, <b><i>elements_pair</i></b> }
<b><i>type_pair</i></b>        ::=   '<b>type</b>' : '<b>PRTDocument</b>'
<b><i>version_pair</i></b>     ::=   '<b>version</b>' : <b><i>version_string</i></b>
<b><i>version_string</i></b>   ::=   '<i>unsigned integer</i>.<i>unsigned integer</i>'
<b><i>dialect_pair</i></b>     ::=   &lt;<i>optional</i> '<b>dialect</b>' : <i>string</i>&gt;
<b><i>elements_pair</i></b>    ::=   '<b>elements</b>' : <b><i>elements</i></b>
<b><i>elements</i></b>         ::=   <i>null</i> | <b><i>text</i></b> | &lt;<i>sequence of</i> <b><i>element</i></b>&gt;
<b><i>element</i></b>          ::=   <i>null</i> | <b><i>text</i></b> | [ <b><i>identifier</i></b>, <b><i>attributes</i></b>, <b><i>elements</i></b> ]
<b><i>attributes</i></b>       ::=   <i>null</i> | { &lt;<i>sequence of</i> <b><i>attribute_pair</i></b>&gt; }
<b><i>attribute_pair</i></b>   ::=   <b><i>attribute_name</i></b> : <b><i>attribute_value</i></b> ,
<b><i>attribute_name</i></b>   ::=   <i>string</i>
<b><i>attribute_value</i></b>  ::=   <i>string</i>
<b><i>text</i></b>             ::=   <i>string</i>
<b><i>identifier</i></b>       ::=   <i>unsigned integer</i></code></pre>


### Example

The following examples are all in `JSON`.

1. This example is the smallest possible PRT document:

    ```json
    {
        "type": "PRTDocument",
        "version": "2.0",
        "elements": null
    }
    ```

2. The *classic* hello-world example:

    ```json
    {
        "type": "PRTDocument",
        "version": "2.0",
        "dialect": "pop",
        "elements":
        [
            [2, {"id": "source"}, [13, null, ["hello, ", [1, null, "world"], "!"]]]
        ]
    }
    ```

    And this can be translated to:

    ```html
    <code id="source"><pre>hello, <b>world</b>!</pre></code>
    ```


### Reference Implementations

- [Server side (python)][1]
- [Client side (javascript)][2] *(Reactified implementation)*
- [GUI binding (javascript)][3] *([Draft.js](https://draftjs.org) binding)*


### The pop-dialect

#### Dialect

- **`'dialect'`**: `'pop'`


#### Identifiers

- **`0x00`**: `'a'`
- **`0x01`**: `'b'`
- **`0x02`**: `'code'`
- **`0x03`**: `'h1'`
- **`0x04`**: `'h2'`
- **`0x05`**: `'h3'`
- **`0x06`**: `'h4'`
- **`0x07`**: `'h5'`
- **`0x08`**: `'h6'`
- **`0x09`**: `'h7'`
- **`0x0A`**: `'i'`
- **`0x0B`**: `'img'`
- **`0x0C`**: `'p'`
- **`0x0D`**: `'pre'`
- **`0x0E`**: `'s'`
- **`0x0F`**: `'u'`


#### Attributes

##### Generic

- **`'id'`**
- **`'class'`**

##### Specific to `0x00`

- **`'href'`**

##### Specific to `0x0B`

- **`'alt'`**
- **`'src'`**



## PRTv1.0

The initial version was used internally and has never been released to the
public.



## License

Copyright &copy;2017 [**We Got POP Ltd.**][4]

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

<!-- anchors -->
[1]: https://github.com/wegotpop/prt-server
[2]: https://github.com/wegotpop/prt-client
[3]: https://github.com/wegotpop/prt-web
[4]: https://www.wegotpop.com
