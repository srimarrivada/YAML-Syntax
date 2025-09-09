# YAML Basic & Advanced Syntax

**YAML** which stands for **YAML Ain't Markup Language** is a human-readable data serialization language primarily used for configuration files and data exchange in modern applications. It emphasizes clean, indentation-based syntax makes it easy to read, write, and maintain, particularly for developers and system administrators. YAML builds upon the structures and concepts found in XML, HTML, Perl, Python, C and other programming languages.

YAML was first proposed by **Clark Evans** in 2001 and designed it together with **Brian Ingerson**, and **Oren Ben-Kiki** and was originally abbreviated as **Yet Another Markup Language** but it was later backronymed (recursive acronym) to **YAML Ain't Markup Language** to emphasize that YAML is data-oriented but not really a markup language.

**YAML** is a more human-readable and concise data serialization language compared to **XML** _(eXtensible Markup Language)_ and **JSON** _(Java Script Object Notation)_. While XML is a markup language developed in early 1990s, JSON and YAML are both modern data formats, with YAML being a superset of JSON. This means any valid JSON file can also be read by a YAML parser, giving it additional features for readability and complexity.

<br/>

## YAML Syntax Rules
YAML's syntax primarily uses indentation to define data structures like key-value pairs and lists, and follows other syntax rules.

* YAML uses Python-style indentation to determine the structure and indicate nesting. <ins>YAML does not allow tab characters for indentation</ins> to maintain portability across systems, so one or more whitespaces (literal space characters) must be used instead of tabs. The number of whitespaces to use for indentation is not fixed but it should be consistent across the YAML file to avoid cross platform issues _(ideally, 2 white spaces are used for indentation)_.
* Each key-value pair which is the primary structure for organizing data in YAML, must be properly separated by a colon (`:`) followed by a space to avoid misconfigurations. Any trailing spaces at the end of key-value pair should be avoided as they can cause issues while parsing the YAML file.
* YAML is case sensitive which applies to all of its elements, particularly the keys in key-value pairs. For example, YAML identifies `data:` and `Data:` as two separate keys, hence consistent casing must be used throughout the YAML file to avoid errors.
* Each list item must be defined on a new line, prefixing with a hyphen and a space (`- `), and at the same level of indentation.
* Strings need not be quoted in general but quotes (single quote or double quote) are required for strings containing special characters such as `[`, `]`, `,`, `@`, etc. or reserved words to avoid misinterpretation.
* YAML allows multi-line strings in folded style (using `>` character) to preserve all new lines or literal style (using `|` character) to replace new lines with spaces.
* Comments in YAML can be defined with a pound or hash symbol (`#`). It is always a best practice to use comments for describing the code, making it easy to understand.
* YAML allows to store multiple documents (each document has its own YAML structure) in a single file with each document separated by three hyphens (`---`) on a new line.
* YAML files can optionally begin with 3 hyphens (`---`) to indicate the start of the document and optionally end with 3 dots (`...`) to indicate the end of the document.
* Each YAML file must use either `.yml` or `.yaml` extension.
<br/>

## YAML Basic Syntax
YAML data type structures are similar to that of Perl and Python. In YAML, there are three fundamental structures (also termed as **nodes** in YAML) which are **Scalars** (data types), **Mappings** (key-value pairs) and **Sequences** (lists). 

YAML follows some key formatting principles to define its data structure.

### Comments
YAML is a superset of JSON but unlike JSON, YAML supports comments which will be helpful to explain the document code. YAML supports only single line comment that can be represented using hash or pound character (`#`) but multi-line or block comments are not supported. However, multi-line comments can be represented using `#` at the beginning of each line. YAML allows to specify comments as a single line or after a value (inline). 

The below YAML code describes a single line comment and inline comment
```
# This is a single line comment
person:
  name: John # this is an inline comment
  age: 30
```

### Indentation
YAML heavily relies on whitespace and indentation to indicate nesting which makes easy to read and understand by humans. YAML follows the Python-like indentation style for defining hierarchical relationships and nesting. YAML allows only white spaces for indentation and tab characters are not allowed. The number of spaces used for indentation does not matter as long as they are consistent at each nesting level to avoid any parsing issues.

```
person: # Nesting level 1 (zero spaces used for indentation)
  name: John # Nesting level 2 (2 spaces used for indentation)
  address: 
    street: 101 Avenue # Nesting level 3 (4 spaces used for indentation)
    city: New York 
    country: USA
```

### Key-Value Pairs
YAML represents data as key-value pairs. The key-value pair is the basic building block of YAML. The key-value pair is represented by a key separated by a colon followed by a space and value such as `<key>: <value>`. YAML also provides a flexibility of marking a key with `? ` (a question mark followed by a space) indicator while value must be marked with `: ` (a colon followed by a space) indicator.
```
name: John 
age: 30
```

### Scalars
Scalars (or Scalar Nodes) in YAML are nothing but values which are represented in various types such as string, integer, float, boolean, etc.  
YAML scalars supports many data types including:
* Numeric datatypes which are `integer`, `float`, `hexadecimal`, `binary`, etc. to represent a number value in various formats.
* String datatype which is `string` to represent a text value.
* Boolean datatype which is `boolean` to represent `true` or `false` value.
* Date datatype which is `timestamp` to represent date and/or time value.

#### Numeric Scalars:
YAML supports many numeric datatypes:
* `integer` which represents a whole number
* `float` which represents a number with decimal point
* `exponential` which represents a number in scientific notation
* `octal` which represents a base-8 number which is prefixed with `0o` (this type is commonly used for file permissions)
* `hexadecimal` which represents a base-16 number which is prefixed with `0x`
* `binary` to represent a number in binary format.

Note that some numeric interpretations vary between YAML 1.1 vs 1.2 version. For example, octal scalar must be prefixed with `0o` in YAML 1.2 while it was prefixed with `0` alone in YAML 1.1 version. 

YAML also supports special numeric data types:
* `infinity` which represents an infinite number, denoted using `.inf` value
* `negative-infinity` which represents a non-positive infinite number, denoted using `-.inf` value
* `not-a-number` which represents a non-number, denoted using `.nan` value.
```
age: 30 # Decimal integer scalar
ageHex: 0x1E # Hexadecimal integer scalar
ageOctal: 0o36 # Octal integer scalar 
ageBinary: 11110 # Binary integer scalar

heightCM: 170.5 # Decimal floating-point scalar
smallscale: 1.0e-10 # Exponential scalar representing 0.0000000001
largescale: 1.0e+5 # Positive exponential scalar representing 1,00,000

inf: .inf # Infinity scalar
inf_: -.inf # Negative infinity scalar
nan: .nan # Not-a-number scalar
```

#### String Scalars:
YAML automatically detects string scalars so that string values need not be explicitly quoted unlike in JSON, Python and other programming languages.
```
name: John #string scalar
userID: user12 #string scalar
```

However, it is necessary to enclose a string scalar in quotations (using either single quotation mark `'` or double quotation mark `"`) when the value contains any special characters such as `#`, `&`, `?`, `|`, `:`, `*`, `@`, `%`, `-`, `{`, `}`, `[`, `]`, `>`, `<`, `=`, `!`,`'`, `"`, `,` , `\`, etc. or when the value must be explicitly represented as string (for example, an integer to be treated as a string).
```
id: "12345" # Quoted to represent number as string
name: 'John D''Ove' # Single quoted to escape internal single quote with another single quote
address: "123 Main Street, Apt #4B" # Double quoted for special characters
```
  
#### Boolean Scalars:
YAML identifies boolean values with keywords `true` or `yes` or `on` for positive statement and keywords `false` or `no` or `off` for negative statement. Note that different versions of YAML may have different rules for interpreting boolean scalars. For example, in YAML 1.1, `yes` and `no` are valid boolean scalars while they are not in YAML 1.2 and so it is recommended to use `true` and `false` for boolean scalars to avoid potential parsing and compatibility issues since `true` and `false` boolean values are standard and widely supported by the most YAML processors.
```
name: John Doe

# Boolean with True/False
verified: True
active: False
  
# Boolean with Yes/No
acceptEmails: Yes
receiveSMS: No

# Boolean with On/Off
notifications: on
awayMode: off
```

#### Date-Time Scalars:
A date-time scalar in YAML represents a specific point in time.  
YAML supports many timestamp formats including:
* **Canonical (ISO 8601 subset) Format:** It is used to specify date and time with milliseconds and UTC (Coordinated Universal Time) in `YYYY-MM-DDThh:mm:ss.sZ` format where `Z` indicates UTC _(for example `2020-10-20T01:23:34.1Z`)_.

* **ISO 8601 Format:** It is used to specify date and time with milliseconds and time zone offset in `YYYY-MM-DDThh:mm:ss.s±hh:mm` format _(e.g. `2020-10-20T01:23:34.10-05:00`)_.

* **Space-separated Format:** It is used to specify date and time values with or without time zone offset separated by spaces in `YYYY-MM-DD hh:mm:ss.s ±h` format or `YYYY-MM-DD hh:mm:ss.s ±hh:mm` format _(e.g. `2020-10-20 01:23:34.10 -5`)_. By default, YAML uses UTC time zone when offset is not explicitly specified.

* **Date only Format:** It is used to specify only the date in `YYYY-MM-DD` format _(e.g. `2020-10-20`)_. In this case, YAML assumes the time part as `00:00:00Z` which is midnight UTC.

Though YAML supports many date-time formats, **ISO 8601 format** is mostly commonly used to maintain consistency across different systems.
```
name: John Doe
birth_date: 1990-05-15 # Date only format with time assumed as 00:00:00Z
register_time: 2023-12-14T21:59:43.10Z # Canonical format with UTC timestamp
last_login: 2024-01-02T08:35:50.10-05:00 # ISO 8601 format with time zone offset (-05:00 indicates Eastern Daylight Time)
last_updated: 2024-01-02 08:35:51 -05:00 # Space-separated format with time zone offset
```

### Mappings
Mappings (or Mapping Nodes) in YAML represent an unordered collection of unique key/value pairs. YAML mappings work like dictionaries in Python or hash maps in Java or associative arrays in other programming languages. Due to the unordered nature of mapping, the order of key-value pairs within a mapping may not be the same after parsing or serialization (though many parsers try to maintain the order during parsing). Each entry in a mapping consists of a unique key and its corresponding value where the key can be a string or number and the value can be of any valid YAML data type such as scalar (string, number, boolean, null) or sequence or a mapping. Mappings in YAML files can be nested by increasing the indentation level and new mappings can be created at the same level by resolving the previous one.

YAML mappings are represented in block style using indentation as below:
```
# Mapping 1
name: John Doe #key: value (string)

# Mapping 2
age: 30 #key: value (number)

# Mapping 3
contact:
  email: jane.doe@example.com #key: value (string)
  phone: #key: value (nested mapping)
    type: home
    details:
      country_code: +1
      area_code: 123
      number: +1-123-456-7890
```

Since YAML is a superset of JSON, the mapping can also be represented in JSON format as flow style by enclosing data in curly brackets `{}` and items separated by a comma.
```
{name: John Doe, age: 30, contact: {email: jane.doe@example.com, phone: {type: home, details: {country_code: +1, area_code: 123, number: +1-123-456-7890}}}}
```

### Sequences
Sequences (or Sequence Nodes) in YAML represent a set of values listed in a specific order.  Sequence works like a list in Python or an array in Bash and other programming languages. Each item in sequence is represented with a hyphen and a space followed by a value. Sequences can be nested using the proper indentation and can also be embedded into a mapping. In YAML, nested sequences need not start with a new line and when a sequence is embedded into a mapping, indentation is not mandatory.

YAML sequences are represented in block style using indentation and hyphen as below:
```
# Sequence 1
skills:
  - Python
  - Java
  - - Core Java # Nested sequence started on same line
    - Advanced Java

# Sequence 2
hobbies: # Sequence in a mapping with indentation
  - Travelling
  - Photography
  - Reading: # Nested sequence of a mapping without indentation
    - Fantasy
    - Science Fiction
    - Historical Fiction
```

YAML sequences can also be represented in JSON format as flow style by enclosing sequence data in square brackets `[]` and items separated by comma.
```
{skills: [Python, Java, [Core Java, Advanced Java]], hobbies: [Travelling, Photography, {fav_genres: [Fantasy, Science Fiction, Historical Fiction]}]}
```

### Nulls
Nulls represent unknown or undefined values and can be used in various ways depending on the context. A null value in YAML can be represented using either `null` keyword or tilde (`~`) special character or empty value.
* A null can be used when the value of data element is unknown or undefined.
* A null can be used to represent an empty value, such as an empty list or an empty string.
* A null can be used as a placeholder value when the actual value is not yet known.
* A null value can be used to represent data that is missing or incomplete.
* A null value can be used with optional parameter such that if the parameter is not specified, the null value will be used.
* A null value can be used to represent when the data is invalid.

```
# Null using null keyword
name: null

# Null using ~ character
age: ~

# Null as an empty value
gender: 
```
<br/>

## YAML Advanced Syntax
YAML offers several advanced features beyond basic key-value pairs and lists, enhancing its utility for complex configurations and data structures.

### Multi-line Strings
YAML has the feasibility of representing large blocks of text in **folded style** or **literal style**.  

In folded style, a string can be specified in multiple lines (as a block) using the folded block scalar (`>`) in YAML file and it is interpreted as a single line without newline characters. Such strings are termed as **Folding strings**. Folding strings can be useful for defining long text fields, such as descriptions, that should appear as a single line after interpretation.
```
example: >
 this looks like 
 a multiline string,
  but it is actually not.
```

The above YAML code is interpreted as below:
```
example: "this looks like a multiline string, but it is actually not."	
```

In literal or block style, a string can be specified in multiple lines (as a block) using the literal block scalar (`|`) in YAML file and it is interpreted as multiple lines with newline characters. Such strings are termed as **Block strings**. Block strings is particularly helpful when defining shell commands.
```
example: |
 This is
  a real
  multiline string.
```

The above YAML code is interpreted with new line characters (`\n`) as below:
```
example: "This is\n a real\n multiline string."
```

When dealing with multi-line strings, **Chomp modifiers** can be used to define how YAML can interpret newlines at the end of the multi-line string.  
YAML provides two chomp modifiers which are **keep** (indicated by `+`) and **strip** (indicated by `-`) to preserve or remove trailing newlines of multi-line string. These modifiers must be used along with folded (`>`) or block (`|`) indicators. 

**Chomp in Folded style:**
```
example: >+
 This is a
  single line with an empty line at the end.

```

The above YAML code is interpreted as below:
```
example: "This is a single line with an empty line at the end.\n"
```

**Chomp in Blocked style:**
```
example: |-
 This is a
  single line with an empty line at the end.

```

The above YAML code is interpreted as below:
```
example: "This is a\n single line with an empty line at the end."
```

YAML follows three chomp modes when handling multiline blocks containing new lines:
* **Clip mode:** This is the default behavior when no chomp indicator is specified. It preserves the first trailing newline and removes any additional trailing empty lines.
  ```
  example: |
   This is a multiline string.
   It has three trailing empty lines.
   
   
   
  ```

  The above YAML code is interpreted as below:
  ```
  example: "This is a multiline string.\nIt has three trailing empty lines.\n"
  ```
  
* **Strip mode:** This is indicated by `–` character in the string block header to remove all trailing spaces and empty lines including the first trailing newline.
  ```
  example: |-
   This is a multiline string.
   It has three trailing empty lines.
   
   
   
  ```

  The above YAML code is parsed as below:

  ```
  "This is a multiline string.\nIt has three trailing empty lines."
  ```
  
* **Keep:** This is indicated by `+` character in the string block header to preserve all trailing spaces and empty lines as they appear in the YAML block.
  ```
  example: |+
   This is a multiline string.
   It has three trailing empty lines.
   
   
   
  ```

  The above YAML code is parsed as below:
  ```
  "This is a multiline string.\nIt has three trailing empty lines.\n\n\n"
  ```
  
### Documents
In YAML, a **Document** refers to a single, complete set of data structures contained within a file. A single YAML file can contain more than one document where each document is considered as a standalone YAML file. This multi-document feature is helpful to organize related but independent configurations within a single file instead of multiple files, making it easier to manage and parse. Each document in a single YAML file can contain its own distinct data structures with scalars, sequences and mappings which means that duplicate keys that are not allowed within a single document can be repeated across different documents in the same file.

YAML files can begin with **Document Start Marker** represented using 3 hyphens (`---`) to indicate the start of the document and optionally end with **Document End Marker** represented using 3 dots (`...`) to indicate the end of the document. When a YAML file has a single document, using `---` is optional but when it contains multiple documents, each document must be separated by a line containing `---` which acts as a document separator. 

```
--- # This is optional for the first document but good to use to indicate start of file
# Document 1: Application configuration
name: MyApp
version: 1.0
environment: production

--- # This is mandatory for the second document
# Document 2: User definition
name: John Doe
email: john.doe@example.com

--- # This is mandatory for the third document
# Document 3: Deployment settings
target: Kubernetes
namespace: default
replicas: 3
resources:
  cpu: 200m
  memory: 256MB

... # This is optional but good to use to indicate end of file
```

In the above example, `name` key is unique in `Document 1` and `Document 2` but repeated across documents.

Though **Document End Marker** is optional, it is useful in some cases. For example, when YAML is used in a stream or over network, it might be important to tell the receiver that the document has ended. 

A YAML document can be started with either mapping block or sequence block. When a YAML document is started with a mapping, then YAML expects only a series of mappings whereas when it is started with a sequence, then YAML expects only a series of sequences.

**YAML started with a mapping block:**
```
---
name: John
age: 30
is_employed: true
gender: Male
address: 
  street: 101 Avenue
  city: New York
  country: USA
hobbies: 
  - Travelling
  - Reading
  - Music Playing
```

When this YAML code is viewed as JSON, it reflects as below:
```
{"name": "John", "age": 30, "is_employed": true, "gender": "Male", "address": {"street": "101 Avenue", "city": "New York", "country": "USA"}, {"hobbies": ["Travelling", "Reading", "Music Playing"]}}
```

**YAML started with a sequence block:**
```
---
- Travelling
- Reading
- Music Playing
- Hours_Played: 100
- Instruments:
  - guitar
  - violin
```

When this YAML code is viewed as JSON, it reflects as below:
```
["Travelling", "Reading", "Music Playing", {"Hours_Played": 100}, {"Instruments": ["guitar", "violin"]}]
```

### Directives
YAML directives are instructions to a YAML processor that appear at the beginning of a YAML document, before the actual data content. Directives are denoted by a percent sign (`%`) followed by the directive name and any parameters. 

YAML directives are declared before a document begins and must be followed by `---` (called as **directives end marker** or **document start marker**) which separates directives from the document's content. YAML directives are applicable to its following document but not the entire YAML file. 

YAML offers two standard directives:
* `%YAML` directive is used to explicitly declare the YAML version that the document confides to. This is helpful to ensure compatibility and consistent parsing across different YAML processors. This directive is declared at the beginning of a YAML document which is followed by the document start marker (`---`).
   ```
   %YAML 1.2
   ---
   # This document adheres to YAML 1.2 version
   name: John Doe
   age: 30
   is_active: true
   ```

   In the above example, the `%YAML 1.2` directive indicates that the document should be parsed according to the YAML 1.2 specification. In YAML 1.2, only `true` and `false` are explicitly recognized as booleans, unlike YAML 1.1 which also recognized `yes`, `no`, `on`, and `off`. Also, YAML applies a `%YAML` directive only to the single document immediately following it. If a YAML file contains multiple documents, each document that requires a specific version directive would need its own `%YAML` declaration.

* `%TAG` directive allows to define the tag handles or shorthand prefixes for URIs (Uniform Resource Identifiers) associated with custom or application-specific data types and these short hands are used in node tags. Basically, this directive helps to create an alias or a shortcut for a longer tag identifier within the YAML document. This makes custom tags more concise and readable within the document. 

   `%TAG` directive must be declared along with a tag handle (shorthand) and a tag prefix (which is generally a URI) at the beginning of the YAML document.
   ```
   %TAG tag_handle tag_prefix
   ---
   ```
   
   There can be three types of tag handles that can be used with tags and `%TAG` directives.
   * **Primary tag handle** is simply an exclamation mark (`!`) which by default associates to `!` tag prefix. This handle is commonly used for custom tags or for explicitly declaring a node (or value) type with a local name.
   * **Secondary tag handle** is written as double exclamation marks `!!` which by default associates to `tag:yaml.org,2002` tag prefix. This handle is commonly used for YAML’s built-in data types.
   * **Named tag handle** defines a custom handle name in between exclamation marks like `!abc!` which is used with `%TAG` directive to create a short alias for longer URI. This handle is commonly used for global tags declaration.
   <br/>
   
   ```
   # Declare TAG directive
   %TAG !py! tag:yaml.org,2002:python/object:
   ---
   - !py!__main__.MyClass # Using the custom tag handle
   ```
   In the above example, `!py!` is the named tag handle or alias defined for the URI `tag:yaml.org,2002:python/object`. When this tag handle is used with in the document, it will be replaced with the URI. So, the sequence item `!py!__main__.MyClass` is evaluated to `tag:yaml.org,2002:python/object:__main__.MyClass` during parsing.

### Tags
YAML tags are identifiers that can be used within a YAML document to explicitly denote the data type of a value (or node) or provide additional metadata. YAML derives data types (implicit typing inference) when no explicit tag is provided which simplifies YAML documents making human-readable.

In YAML, tags are broadly classified into two types:  
 
**1. Non-Specific Tags:**  
  Non-specific tags are the default tags assigned to nodes (values) when the data type of a node (a value) is not explicitly declared in YAML document. They bring in the **implicit typing** feature which automatically determines the data type of values based on the data provided _(for example, a string that starts with a digit is auto-interpreted as a number, and a number that is enclosed in quotes is auto-interpreted as a string)_. YAML parser infers data types automatically. For instance, strings are auto tagged to `tag:yaml.org,2002:str`, maps are auto tagged to `tag:yaml.org,2002:map`, sequences are auto tagged to `tag:yaml.org,2002:seq`, etc. 
   
   The non-specific tag is typically denoted with `!` (single exclamation mark) so that when a node has the `!` tag, it informs the YAML parser to interpret the node as a basic type (string, map, or sequence) resolving to `tag:yaml.org,2002:str` or `tag:yaml.org,2002:map` or `tag:yaml.org,2002:seq` based on its structure. For example, `! 133` value is forcefully interpreted as basic string type though it appears as a number.

   ```
   # Implicitly inferred as a string
   name: John Doe 
    
   # Implicitly inferred as an integer
   age: 30
    
   # Implicitly inferred as a float
   height: 172.5
    
   # Implicitly inferred as a boolean
   active: true
    
   # Implicitly inferred as null
   phone: ~
    
   # Implicitly inferred as a sequence
   hobbies: 
   - Travelling
   - Photography
    
   # Implicitly inferred as a mapping
   address: 
     street: 101 Avenue 
     city: New York 
     country: USA
     zip: "12345" # Explicitly quoted to infer as a string
   
   # Explicitly inferred as a string, overriding potential number inference
   phone: ! 9192939495
   ```

**2. Specific Tags:**  
  Specific tags in YAML provide a flexibility to explicitly declare the data type of a value or provide additional metadata beyond the implicit type reference. 
  
  In YAML, specific tags can be defined using **standard tags** or **custom tags**:
  * **Standard Tags:**  
    Standard tags are used to explicitly declare the data type of a value to avoid any misinterpretations and ensure data is parsed correctly by different applications. Tags for datatype can be declared using double exclamation marks `!!` (secondary tag handle) followed by the name of data type such as `!!int`, `!!str`, `!!seq`, etc. By default, the `!!` expands to `tag:yaml.org,2002:` so the `!!int` tag maps to the built-in YAML integer type as `tag:yaml.org,2002:int`, similarly `!!str` tag maps to `tag:yaml.org,2002:str`, `!!seq` maps to `tag:yaml.org,2002:seq`, etc.

    Note that if a single exclamation mark is used for tagging such as `!int`, it is identified as a local tag which requires a tag resolution mechanism to resolve `!int` to a specific URI that defines the int type.

    The most commonly used standard tags are:
    * Scalar type tags including `!!str` (represents text data), `!!int` (represents whole number), `!!float` (represents number with fractional parts or a floating-point number), `!!binary` (represents binary data encoded in base64), `!!null` (represents a null or empty value), `!!bool` (represents truth values such as true or false), `!!timestamp` (represents a point in time, as date and/or time), etc.
    * Collection type tags including `!!map` (represents a mapping with unordered collection of key-value pairs), `!!seq` (represents a sequence with ordered collection of items), `!!set` (represents an unordered collection of unique values) and `!!omap` (represents a mapping with ordered sequence of key-value pairs).
    <br/>
    
    ```
    # Implicitly inferred as a string
    name: John Doe

    # Explicitly declared to treat as an integer
    height: !!int 172.5 # Treat 172.55 an integer, truncating the decimal

    # Explicitly declared to treat as a boolean
    active: !!bool true

    # Explicitly declared to treat as null
    phone: !!null ~

    # Explicitly declared to treat as a sequence
    hobbies: !!seq
    - Travelling
    - Photography

    # Explicitly declared to treat as a mapping
    address: !!map
      street: 101 Avenue
      city: New York
      country: USA
    ```

  * **Custom Tags:**  
    Custom tags are used to represent complex data types that are not covered by the built-in scalars (strings, integers, floats, booleans) and collections (maps and sequences). Custom tags are useful to create custom schemas for special configurations or data serialization and represent complex and user-defined data structures and domain-specific concepts or objects. 

    Parsing YAML with custom data types involves defining the custom data structure or class (e.g., `!Person` custom type representing a `Person` object with `name`, `age`, and `city` attributes) and  implementing serialization/deserialization mechanism for the custom type in the chosen programming language. This allows the YAML parser to recognize and correctly convert the specific structures within the YAML document into corresponding classes or data structures defined in the programming code.

    YAML allows to create two types of custom tags – **Local tags** and **Global tags** defining their scope.

    * **Local Tags:**  
      Local tags are declared and used within a single YAML document and are not globally unique. These are helpful to define custom data types that are only relevant within the context of that specific YAML document. Local tags are denoted using primary tag handle `!` followed immediately by the custom tag name without any space such as `!tag`.

      ```
      ---
      people:
        - !Person # local tag for a custom Person data type
          name: John Doe
          age: 30
          city: New York
        - !Person
          name: Jane Smith
          age: 25
          city: Los Angeles
      ```

      In the above example, `!Person` is a custom local tag used to identify the subsequent data as representing the `Person` object with `name`, `age` and `city` attributes within this specific document.

      By default, the primary tag handle `!` is associated to tag prefix `!`. However, this default behavior can be overridden by declaring tag prefix beginning with `!` using `%TAG` directive.
      ```
      %TAG !emp! !Employee
      ---
      people:
        - !emp!Person # local tag with named handle for a custom Person data type
            name: John Doe
            age: 30
            city: New York
      ```

      In the above example, `!emp!` is the named tag handle or alias defined for the local tag prefix `!Employee`. When this tag handle is used with in the document, it will be replaced with the tag prefix. So, the sequence item `!emp!Person` is evaluated to `!EmployeePerson` during parsing.

    * **Global Tags:**  
      Global tags are custom URIs used to reference a specific data type or schema in YAML using Universal Resource Identifier (URI). This helps to represent custom data structures that are specific to an application or domain. Global tags must be unique across all applications in the environment.

      A global tag must be declared before the start of the YAML document using the `%TAG` directive followed by the tag handle and tag prefix. For global tag declaration, YAML allows to use either primary tag handle `!` _(though it is commonly used for local tags)_ or secondary tag handle `!!` _(though it is commonly used for standard tags)_ or named tag handle _(commonly used for global tags)_, but the tag prefix must begin with `tag:` to specify URI (which generally includes domain name and year to ensure global uniqueness) such as `%TAG !example! tag:example.com,2025:`.

      ```
      # Global tag declaration with primary tag handle ! 
      %TAG ! tag:example.com,2025: 
      --- !person # Top level object is a custom type !person 
      name: John Doe
      age: 30
      skills: # Sequence of skills
      - !skill # Each skill is a custom type !skill 
        name: Programming
        level: Expert
      - !skill
        name: Cloud Computing
        level: Advanced
      ```

      In the above example, global tag is created with tag handle `!` which is associated with `tag:example.com,2025:` URI. Then, `!person` is defined at the start of the document indicating the subsequent data within the document is a custom type `!person` where `!` represents `tag:example.com,2025:` and it has scalars representing person’s name and age along with skills mapping that has a sequence of skills in which each skill is a custom type `!skill` where `!` represents `tag:example.com,2025:`.

      YAML allows to declare multiple global tags using multiple `%TAG` directives to define tag prefixes, which makes easy to refer to specific tag URIs within a document. While multiple `%TAG` directives can be used in a single YAML document, each directive must define a unique prefix or a unique URI for a given prefix.
      
      For example:
      ```
      %TAG !person! tag:example.com,2024:person/ # General person tag declaration
      %TAG !employee! tag:example.com,2024:person/employee/ # Specific person employee tag declartion
      %TAG !contractor! tag:example.com,2024:person/contractor/ # Specific person contractor tag declaration
      ---
      employees:
      - !employee!FullTime: # Tag for a full-time employee
        id: EMP001
        firstName: Alice
        lastName: Smith
        department: Engineering
        startDate: 2023-01-15
        salary: 75000.00
      - !employee!PartTime: # Tag for a part-time employee
        id: EMP002
        firstName: Bob
        lastName: Johnson
        department: Marketing
        startDate: 2024-03-01
        hoursPerWeek: 20
    
      contractors:
      - !contractor!Individual: # Tag for an individual contractor
        id: CON001
        firstName: Charlie
        lastName: Brown
        company: Independent Solutions
        contractEndDate: 2025-12-31
        hourlyRate: 50.00
      - !contractor!Agency: # Tag for a contractor from an agency
        id: CON002
        firstName: Diana
        lastName: Miller
        company: Global Talent Agency
        contractEndDate: 2026-06-30
        agencyFee: 15.00
      ```

      In the above YAML code, `%TAG !person! tag:example.com,2024:person/` defines `!person!` short alias for the longer URI `tag:example.com,2024:person/`. Here, `!person!` acts as a general tag handle for any person-related data. While it is not directly used in any data, it helps to organize and define the other specific person tags within the YAML document, providing a clear hierarchy and structure for custom data types. Then a `!employee!` tag handle is defined for employee-specific data using a more specific URI prefix and a `!contractor!` tag handle is defined for contractor-specific data with its own URI prefix. These are used to define different types of employees (using `!employee!FullTime`, `!employee!PartTime` tags) and contractors (using `!contractor!Individual`, `!contractor!Agency` tags).

    Standard tags, local tags and global tags can be used depending on the specific needs of YAML data and its intended use:
    * **Standards tags** are recommended when explicit declaration of common YAML data types (strings, integers, mappings, etc.) is needed to avoid any misinterpretations and ensure data is parsed correctly by different applications.
    * **Local tags** can be used when custom data types are only relevant to a specific YAML file and don't require global uniqueness or external referencing.
    * **Global tags** are preferred when data schemas need to be shared across multiple YAML files or different applications ensuring consistent data representation and type validation.

    **Language-specific Tags:**  
    YAML also allows to use language-specific tags, which extend the basic YAML type system to represent objects from a specific programming language. These tags indicate that the subsequent YAML data represents an instance of a specific object or class within that programming language. When a YAML parser encounters a language-specific tag, it uses its knowledge of that tag and the associated language's object model to instantiate the correct object type and populate the object attributes from the YAML data.

    Language-specific tags are denoted with a double exclamation mark (`!!`) followed by the language and then the specific object or type such as `!!python/object`, `!!java/object`, `!!ruby/object`, `!!perl/regexp`, etc. For example, a Python YAML parser uses `!!python/object:module.ClassName` tag to represent an instance of a Python class, `!!python/tuple` tag to represent a Python tuple, `!!python/set` tag to represent a Python set, `!!python/complex` tag to represent a Python complex number.

    ```
    # Represents a Python complex number
    number: !!python/complex 1+2j

    # Represents a Python tuple
    ? !!python/tuple [ 5, 7 ]: Fifty Seven

    # Represents an instance of a custom Python class
    person: !!python/object:__main__.person
      name: John Doe
      age: 30
    ```

    Note that constructing objects using language-specific tags can introduce security vulnerabilities if YAML documents are loaded from untrusted sources. To avoid this, always use safe loading functions _(such as `yaml.safe_load()` in PyYAML)_ when dealing with untrusted YAML data, as these functions limit the types of objects that can be constructed.

### Schema
A **Schema** is the connection between Tags in YAML and Classes (or data types) in the programming language. Schemas in YAML can be thought of as the way that YAML parser resolves or understands data in a YAML file. YAML uses schemas to determine how tags are interpreted and resolved to native data types. 

YAML 1.2 specifically uses three default schemas that build up on each other:
* **FailSafe Schema:** It is the most minimalist schema which only understands strings (`!!str`), maps (`!!map`) and sequences (`!!seq`) and is guaranteed to work for any YAML file due to its simplicity, but it does not support any complex tags.

* **JSON Schema:** It is a foundational schema designed to reliably parse equivalent YAML and JSON files to the same end result. This is the most commonly used schema and is the starting point for most schemas. It understands all types supported within JSON format including integers (`!!int`), floating numbers (`!!float`), Booleans (`!!bool`) and nulls (`!!null`) in addition to the ones supported by the FailSafe schema.

* **Core Schema:** It is the default YAML schema which is an extension of the JSON schema, offering more flexible matching rules for nulls and booleans by supporting the same type but in multiple forms, making YAML files more human-readable. For example, `null` or `Null` or `NULL` will all be resolved to the same null type and `true` or `True` or `TRUE` will all be resolved to the same boolean type.

  * `!!null` matching rule is defined as `null` or `Null` or `NULL` or `~` or empty scalar
  * `!!bool` matching rule is defined as `true` or `True` or `TRUE` for true statement and `false` or `False` or `FALSE` for false statement
  * `!!int` Integer Base 10 matching rule is defined as `[-+]? [0-9]+`
  * `!!int` Octal matching rule is defined as `0o [0-7]+`
  * `!!int` Hex matching rule is defined as `0x [0-9a-fA-F]+`
  * `!!float` Float matching rule is defined as `[-+]? ( \. [0-9]+ | [0-9]+ ( \. [0-9]* )? ) ( [eE] [-+]? [0-9]+ )?`
  * `!!float` infinity matching rule is defined as `[-+]? ( \.inf or \.Inf or \.INF )`
  * `!!float` Not a Number matching rule is defined as `\.nan or \.NaN or \.NAN`

Note that YAML 1.1 version does not have schema concept but it has **Types** concept where the mandatory types/tags are `!!str`, `!!map` and `!!seq` and some optional types are `!!int`, `!!float`, `!!null`, `!!bool`, `!!binary`, `!!timestamp`, etc.

YAML 1.2 also allows to create custom schemas based on the JSON Schema since YAML Schema is a small extension of **JSON Schema Draft 4**. To create a custom schema, a fundamental understanding of JSON Schema concepts like **data types** _(`type`)_ such as `string`, `number`, `integer`, `boolean`, `object`, `array` and `null`, **expected properties** within JSON object _(`properties`)_, **required fields** _(`required`)_, **limitation on values** _(`minLength`/`maxLength` for strings, `minimum`/`maximum` for numbers, `minItems`/`maxItems` for arrays, expected `format`)_, **allowed patterns** _(`pattern`)_, **restrict values** _(`enum`)_, **validate instance** in one or any or all schemas _(`oneOf`, `anyOf`, `allOf`)_, etc. is essential. Refer to [official JSON schema](https://json-schema.org/) website to know more.

Custom YAML schema file can be created either in JSON format with `.json` file extension or in YAML format with `.yaml` file extension. This file will describe the expected structure of YAML documents. Custom schemas are helpful when configuration files include custom objects or when language specific object serialization needs to be created.

For example, the following YAML schema defines a person:
```
# Example custom_schema.yaml
$schema: http://json-schema.org/draft-07/schema#
title: My Custom YAML Schema
description: Schema for a person

type: object
properties:
  name:
	type: string
	description: Name of the person
	minLength: 3
    age: 
      type: integer,
      description: Age of the person,
      minimum: 0,
      maximum: 120
    email: 
      type: string,
      description: Email address of the person,
      format: email
required:
  - name
  - age
```

This schema specifies that a person is an object with three properties: `name`, `age` and `email`. The `name` property must be a `string` with minimum of `3` characters, the `age` property must be an `integer` ranging from `0` to `120` and `email` property must be a `string` to be specified in email format. Out of these 3 properties, the `name` and `age` properties are marked as required which must be specified in the YAML document where this schema is being referenced.

Once the custom schema is defined, it can be referenced at the top of the YAML file by including a comment with `$schema:` keyword.
```
# $schema: ./custom_schema.yaml
person:
  - name: John Doe
    age: 30
    email: jane.doe@example.com
  - name: Jane Smith
    age:25
```
A YAML processor often also implements a language specific schema for serializing objects.
Below is how serializing of generic objects looks like in several languages:
```
---
# Ruby Psych
dice: !ruby/Object:Dice [3, 6]

---
# perl YAML::XS, YAML.pm, YAML::Syck (Dump and Load)
dice: !!perl/array:Dice [3, 6]

---
# perl YAML.pm, YAML::Syck (Load)
dice: !perl/array:Dice [3, 6]

---
# Pyyaml
dice: !!python/object/new:__main__.Dice
  - !!python/tuple [3, 6]
```

### Mapping Key
In a YAML mapping, keys are typically scalar values like strings, numbers, or booleans. However, YAML also supports complex keys where the key itself is a more complex data structure (such as a mapping or sequence) or contains special characters. Complex keys are explicitly denoted by a question mark `?` followed by the key's content. When a key is prefixed with `?` , it signifies that a complex mapping key is defined. This explicit mapping syntax tells the YAML parser that the entire block following the question mark until the colon `'` should be treated as the key, even if it contains elements that would normally be interpreted as values or part of the structure. 

The mapping key is primarily used in complex or ambiguous scenarios where there is a chance that key might be misinterpreted as a value or a sequence item. For example, if a key itself contains special characters or needs to be multiline, using `?` helps to explicitly define it as a key.
```
---
name: John Doe

# Explicit key-value pair using '?' for a multi-line key
? |
  This is a
  multi-line key
: This is the value for the multi-line key.

# Explicit key-value pair with a list as key 
? - item1
  - item2
: This is the value associated with the list key
```

### Anchors & Aliases
YAML Anchors and Aliases are powerful features that facilitate the reuse of data within a YAML document to avoid redundancy and improve maintainability by allowing to define a block of configuration once and then reference it multiple times throughout the YAML document. They are especially useful for creating templates or for sharing common data between multiple parts of an application. YAML anchors and aliases cannot contain the `[`, `]`, `{`, `}`, and `,` characters.
 
An **Anchor** is a named reference point defined on a YAML node (scalar, mapping, or sequence) to mark a specific value or a block of data for reuse. It is denoted by using ampersand symbol (`&`) followed by a unique name.
```
# Define a base person location using an anchor
person_location: &default_location
  location: New York
  country: USA
```
In the above example, `&default_location` defines an anchor named `default_location` for the `person_location` mapping.

An **Alias** is a reference to a previously defined anchor. It is denoted by using an asterisk symbol (`*`) followed by the name of the anchor. When an alias is used, the value or block of data associated with the referenced anchor is effectively copied to the alias’s location in the document.
```
person:
  - name: John Doe # First person, referring default location
    age: 30
    location: *default_location
  - name: Jane Smith # Second person, referring default location
    age: 25
    location: *default_location
```
In the above example, `*default_location` is an alias used to reference content in `default_location` anchor which was defined earlier.

YAML provides a feature to override the content referenced in the anchor while using the alias. The merge key denoted by `<<:` allows merging an aliased mapping into the current mapping. If same keys are used in aliased mapping and current mapping, the current mapping’s value takes precedence. 
```
# Define a base person configuration using an anchor
person_defaults: &default_person_info
  name: Unknown
  occupation: Software Engineer
  skills:
    - Programming
    - Problem-solving
    - Communication
  location: New York
  country: USA
person:
  - <<: *default_person_info # Merge the common person attributes
    name: John Doe # Override the default name
    age: 30
  - <<: *default_person_info # Merge the common person attributes
    name: Jane Smith # Override the default name
    age: 25
    skills: # Override the entire skills list
    - Project Management
    - Team Leadership
    - Budgeting
```
In the above example, both `John Doe` and `Jane Smith` inherit content from the `&default_person_info` anchor, with `John Doe` overriding `name` and `Jane Smith` overriding `name` and `skills`. This eliminates the need to repeat `occupation`, `location` and `country` for each person reducing redundancy and simplifying maintenance.

### Escape Sequences
YAML files treat `#`, `&`, `?`, `|`, `:`, `*`, `@`, `%`, `-`, `{`, `}`, `[`, `]`, `<`, `>`, `=`, `!`,`'`, `"`, `,`, `\`, etc. as special characters. When these special characters are actually part of the data or value, they can be escaped in many different ways though enclosing a string in double quotes is the most common way to escape special characters.

YAML offers **Escape Sequences** to indicate if the character should be interpreted as a special character or as part of the scalar.  
There are four types of Escape Sequences that can be used in YAML:
* **Single Quoted Escapes** allows to enclose a string in single quotes (`'`) which treats all characters (except single quote itself) literally, meaning backslashes are not interpreted as special character. To include a literal single quote within a single-quoted string, it must be escaped by using two consecutive single quotes (`''`).
  ```
  text: 'This string contains a literal backslash: \\ and a single quote: '\''Hello'\'''
  ```

* **Double Quoted Escapes** allows to enclose a string in double quotes (`"`) and use backslash for escape sequences to represent special characters like new lines (`\n`), tab (`\t`), or to include backslash (`\\`) or even double quotes (`\"`) within the string.
  ```
  text: "This string has a tab \t and a newline: \n along with backslash and a double quote: \"Hello\\\""
  ```

* **Entity Escapes** are HTML characters that have special meaning in HTML and can be used in YAML to represent special characters within data so that characters are treated as literal content rather than indicators of structure. A string using entity escapes must be enclosed in double quotes (`"`).

  For example, entity escapes like  
  `&#x20;` is used to represent space character.  
  `&#58;` is used to represent colon character.  
  `&lt;` is used to represent less than character.  
  `&gt;` is used to represent greater than character.  
  `&amp;` is used to represent ampersand character.  

  ```
  person:
    name: John Doe
    title: "Senior Developer &amp; Team Lead" # Using &amp; for & character
    contact:
      email: "jane.doe&#x40;example.com"  # Using &#x40; for @ character
    skills:
      - Programming: "Java, Python"  
      - Web Development: "HTML5, CSS3, &lt;Frameworks&gt;" # Using &lt; for < character and &gt; for > character
    experience:
      - company: "Tech Solutions, Inc."
        role: "Lead Developer (2020 &ndash; Present)" # Using &ndash; for en dash
      - company: "Creative Minds Corp."
        role: "Junior Developer (2018 &mdash; 2020)" # Using &mdash; for em dash
  ```

* **Unicode Escapes** can also be used to represent special characters in format `\uXXXX` where `XXXX` is the hexadecimal Unicode point. This is particularly useful when dealing with characters that might not be easily typable or displayed in editor, or when need to embed Unicode characters within a string that also contains special YAML characters. A string using Unicode escapes must be enclosed in double quotes (`"`).

  For example, Unicode escapes like  
  `\u0020` is used to represent space character.  
  `\u0027` is used to represent single quote character.  
  `\u0022` is used to represent double character.  

  ```
  # Representing unicode characters
  "Name in Japanese": "\u5C71\u7530 \u592A\u90CE" # Yamada Tarō (山田 太郎) in Japanese language

  # Combining unicode escapes with other escape sequences
  copyright: "Copyright symbol: \u00A9\nNewline and tab: \t"
  ```

### Advanced Data Types
Beyond basic scalars (strings, numbers, booleans) and collections (sequences and mappings), YAML supports advanced data types such as ordered mappings, sets and pairs that provide greater flexibility while representing data.

* **Ordered Mappings:**  
  The standard YAML mappings are unordered in nature which means when a YAML parser processes a mapping, it does not guarantee that the order of key-value pairs in the input file is preserved after parsing.   To maintain the order of key-value pairs, YAML provides the `!!omap` tag that defines an ordered sequence of unique key-value pairs. 
  ```
  person: !!omap
    - name: John Doe
    - age: 30
    # Representing ordered mapping in flow style
    - address: !!omap [street: 101 Avenue, city: New York, country: USA] 
  ```
  
  Some YAML parsers may not support ordered mappings in which case the order can be stored separately in a YAML sequence which is used to iterate through the mapping.
  ```
  ordered_person_data:
    order:
	    - name
	    - age
	    - location
    person:
	    name: John Doe
	    age: 30
	    location: USA
  ```
  In the above example, the `order` sequence explicitly defines the desired order of keys from the `person` mapping. The application logic then uses this `order` sequence to iterate through the `person`   mapping in the specified order. 

* **Sets:**  
  In YAML, a set is a mapping that represents as an unordered collection of unique keys where each key has a null value. A YAML set can also be explicitly declared using `!!set` tag.

  A set in YAML can be represented in three ways:
  * Using the `?` indicator explicitly indicates a set by placing a `?` before each item, signifying that item is a key in a mapping with a null value.
  * Using a flow-style notation similar to a JSON object with keys to represent a mapping where all values are implicitly null.
  * Using the `!!set` tag explicitly indicates a set.
  <br/>
  
  ```
  person:
    name: Alice Smith
    skills: # Represents a set with ? indicator
      ? Python
      ? Java
    hobbies: !!set # Represents an explicit set with !!set tag
      ? Reading
      ? Hiking
    contact: { email, phone }# Represents a set in flow style
    address: # Represents a set since all keys has null values
      city: null 
      country: null 
  ```
  In the above example, the `?` before each item signifies that it is a key in a mapping, and implicitly considered to have a null value (since no value is provided).

* **Pairs:**  
  YAML pairs, denoted using `!!pairs` tag, defines a mapping with ordered sequence of key-value pairs where keys can be duplicated. Using `!!pairs` tag preserves the order in which key-value pairs appear even after parsing. This is useful in scenarios where both the order of key-value pairs and the possibility of duplicate keys are significant. For example, it can be used to represent data structures that are ordered lists of named values, which is commonly seen when modeling data like XML documents. However, many programming languages do not have a direct native equivalent for this data type, in which case a library support is needed for handling `!!pairs` when parsing YAML.

  ```
  name: John Doe
  age: 30
  address: !!pairs
    - home:
        street: 10 Downing Street
        city: London
        country: UK
        start_date: 2010-01-01
        end_date: 2015-12-31
    - work:
        street: 1600 Pennsylvania Avenue NW
        city: Washington DC
        country: USA
        start_date: 2016-01-01
        end_date: 2018-06-30
    - work:
        street: 17 Avenue
        city: New York
        country: USA
        start_date: 2018-07-01
        end_date: null # null implies current or ongoing
  ```

  In the above example, the `work` address appears twice indicating a move from one work location to another, with both previous and current address listed in the order worked.
<br/>

## YAML Indicators
It is important to understand that YAML uses specific characters (called as **indicators**) for specific functionality to describe the content of YAML document.

Some of these indicators are listed below:  
`_` indicator denotes a block sequence entry  
`?` indicator denotes a mapping key  
`:` indicator denotes a mapping value  
`,` indicator denotes flow collection entry  
`[` indicator denotes the start of a flow sequence  
`]` indicator denotes the end of a flow sequence  
`{` indicator denotes the start of a flow mapping  
`}` indicator denotes the end of a flow mapping  
`#` indicator denotes comments  
`&` indicator denotes anchor node  
`*` indicator denotes alias node  
`!` indicator denotes tag handle  
`|` indicator denotes a literal block scalar  
`>` indicator denotes a folded block scalar  
`'` indicator is used to surround a single quoted flow scalar  
`"` indicator is used to surround a double quoted flow scalar  
`%` indicator denotes the directive used  

YAML provides an official [Reference Card](https://yaml.org/refcard.html) which lists out all characters used for specific YAML representation. 

Below is a sample YAML file (`sample.yaml`) showcasing all it's indicators
```
# Lines starting with # are ignored by parsers

%YAML 1.2 # It specifies the version that this document adheres to
%TAG !app! tag:mydomain.com,2025: # It creates `!app!` shorthand name for the specified URI

--- # It indicates the start of a YAML document
server_config:
  # Mappings
  host: "api.example.com" # Quoted to avoid misinterpretation due to . character
  port: 8080
  # Sequences
  endpoints:
    - /data
    - /status
    - /healthz
    # Flow styles use brackets and braces for in-line collections
    - [error, timeout, redirect]
  
  # Scalars
  is_secure: true # Boolean scalar
  user_agent: 'MyApp/1.0 (#version-info)' # Single-quoted scalar with special characters
  status_message: "Server is running.\nAll systems green." # Single-quoted scalar to allow escape sequences
  
  # Block scalars
  literal_text: | # Literal block to preserve line breaks and indentation
    This is a block of text.
      The indentation here is preserved.
    Newlines are kept exactly as written.
  
  folded_text: > # Folded block to fold newlines into spaces
    This is a very long text that can
    be folded into a single line.
    
      Blank lines, however,
      will remain as line breaks.
  
  # Anchor and Alias
  default_user: &DEFAULT_USER # Anchored to reuse later
    name: guest
    roles: [read-only]

  current_user: *DEFAULT_USER # Aliased to replace with anchor content

  # Tags 
  admin_user: !app!user # Using named tag handle defined by %TAG directive above
    name: admin
    roles: !!seq [admin, read-only] # Using built-in type to represent a list
  binary_data: !!binary "QmFzZTY0IGV4YW1wbGU=" # Using built-in type to represent binary value

# Multiple documents
--- # It indicates a second, independent document
? - production # `?` indicator is used for non-scalar keys
  - database_host
:
  - primary_db: "prod-db-1"
  - secondary_db: "prod-db-2"
... # It indicates the end of the file or a document
```
<br/>

## YAML Validators
A YAML file can be created or modified using any text editor such as [VS Code](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml) _(with YAML plugins)_, [PyCharm](https://www.jetbrains.com/pycharm/) _(with built-in YAML support)_, [Sublime Text](https://www.sublimetext.com/) _(with YAML syntax highlighting)_ but it is recommended to validate YAML file for any syntactical errors like using tabs in place of spaces, weird issues like repeated characters, trailing spaces, etc. using YAML linting tools.

There are many CLI and online tools available to ensure correct YAML structure is followed:
* **CLI Tools:**  
  CLI tools such as [yamllint](https://github.com/adrienverge/yamllint), [yamle](https://github.com/23andMe/Yamale), [yq](https://github.com/mikefarah/yq), [yaml-validator](https://github.com/paazmaya/yaml-validator), [yaml-lint](https://www.npmjs.com/package/yaml-lint), etc. are available in market to validate and format YAML files. The most popular tool is **yamllint** which is a Python based linter that not only checks for syntax validity, but also for weird nesses like key repetition and cosmetic problems such as lines length, trailing spaces, indentation, etc. Follow [this documentation](https://yamllint.readthedocs.io/en/stable/quickstart.html#installing-yamllint) on installing `yamllint` via command line. 

* **Online Tools:**  
  The popular online tools are [YAML Lint](https://www.yamllint.com/) _(checks for YAML syntax errors and cosmetic issues)_, [JSON Formatter’s YAML Validator](https://jsonformatter.org/yaml-validator) _(validates and converts JSON to YAML format)_ and [Online YAML Parser](https://yaml-online-parser.appspot.com/) _(converts YAML to JSON or Python format)_ that can be used to parse YAML structure online.

Additionally, several programming languages can be utilized for parsing and validation. The commonly used YAML parsers include:
* [PyYAML](https://pyyaml.org/wiki/PyYAMLDocumentation) (`pyyaml` library) or [Ruamel YAML](https://pypi.org/project/ruamel.yaml/) (`ruamel.yaml` library) for **Python** language
* [SnakeYAML](https://mvnrepository.com/artifact/org.yaml/snakeyaml) (`snakeyaml` library) for **Java** language
* [Rapid YAML](https://rapidyaml.readthedocs.io/latest/) (`ryaml` library) for **C++** language
* [JS YAML](https://www.npmjs.com/package/js-yaml) (`js-yaml` library) for **Java Script** language
* [Go YAML](https://github.com/go-yaml/yaml) (`go-yaml` library) for **Go** language
* [YAML DotNet](https://www.nuget.org/packages/yamldotnet) (`YamlDotNet` library) for **.Net** language
* [YAML Rust](https://docs.rs/yaml-rust/latest/yaml_rust/) (`yaml-rust` library) for **Rust** language.

For example:
* Parse in **Python** language with `pyyaml` library installed:
  ```
  python -c "from yaml import load, Loader; load(open('test.yml'), Loader=Loader)"
  ```

* Parse in **Ruby** language with `rbyaml` package installed:
  ```
  ruby -rbyaml -e "p yaml.load(STDIN.read)" < test.yml
  ```

* Parse in **Perl** language with `YAML.pm` module installed:
  ```
  perl -MYAML -e 'use YAML;YAML::LoadFile("./test.yml")'
  ```
<br/>

