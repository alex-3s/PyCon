# PyCon 2022 - Notes

## Day One
&nbsp;

### Keynote - Łukasz Langa
#### **Recommend: Yes**

Łukasz Langa is the creator of Black and the first core python developer to be hired as a full-time developer on the CPython project.

On Type Annotations:

* Type Annotations are documentation
* Ugly Type Annotations hint at ugle code
    * They expose complexity that was always there
* Give Types Meaningful Names
    * Create reusable annotations to describe data
    * Use NewType and Type Aliasing
* Dispatch early to specialize
    * Break up functions that take multiple-types arg into other functions
    * One variable, one type

&nbsp;
\
&nbsp;

### Python Oddities Explained - Trey Hunner
#### **Recommend: Yes**

Trey gave a fun talk on interesting behavior in the python language than can be summarized by the statement below:

* += does something different depending on whether you are using a mutable vs immutable ds (list vs tuple for example)

&nbsp;
\
&nbsp;

### Demystifying Python’s Internals: Diving into CPython by implementing a pipe operator - Sebastiaan Zeeff
#### **Recommend: Maybe**

* CPython Internals
    * Tokens, Grammar, PEG Parser
        * File Grammer/Tokens: Dictionary for syntactic symbols
        * File Grammer/python.gram (easy but not best way) to add new rules
        * File Parser/Python.asdl defines AST nodes
        * File Lib/opcode.py 
        * File Python/compile.c 
    * Abstract Syntax Trees (AST)
        * A representation for source code for the parser
    * The Compiler, bytecode, and "opcodes" 
    * The Evaluation Loop

*Additional Resources*:  
https://devguide.python.org/  
https://realpython.com/cpython-source-code-guide/

&nbsp;
\
&nbsp;

### Best Practices for Continuous Integration in Python - Moshe Zadka
#### **Recommend: Not Really**

While great for beginners, Moshe didn't really provide any additional information beyonds the basics one can find online.

Why is CI Important?
* A lot of time goes into patching, so optimizing this workflow is extremely important
* CI are automated gates for regression testing

What makes a good CI system?
* Accuracy
* Detailed
    * Provides instructions on build
    * Provides instructions on reproducing errors
* Speed

How to improve a CI system?
* Use Containers
    * Manage dependencies
* Add detailed Exceptions
    * A good CI system will have good logs, make use of them by providing good error messages to report when something goes wrong.
* Log as many releveant environment details as possible.

&nbsp;
\
&nbsp;

### A Perfect Match: The history, design, implementation, and future of Python's structural pattern matching. - Brandt Butcher
#### **Recommend: Yes**

Brandt Butcher is a Python Core Developer, and gave an excellent talk on how the Structural Pattern matching introduced in Python 3.10

* https://docs.python.org/3/whatsnew/3.10.html#pep-634-structural-pattern-matching

Introduced in PEP-622, Later split into 634, 635, 636:  
* https://peps.python.org/pep-0634/
* https://peps.python.org/pep-0635/
* https://peps.python.org/pep-0636/

Structural Pattern Matching is NOT a switch statement, it does:
* Control Flow (Branching)
* Destructuring (exposing data)

But more importantly, it can do *both at the same time*.

Additional Features:
* Cases are PATTERNS not EXPRESSIONS
* Soft Keywords:
    match and case are not locked keywords, and the interpreter can tell whether you are using match or case as a variable name or as the SPaM.
* More performant than if/else because of the opcodes

&nbsp;
\
&nbsp;

### How to Succeed with Python Across the Enterprise - Greg Compestine
#### **Recommend: No**

Greg Compestine of Bloomberg reflected on how they became a leading contributor to the python scene. They migrated from C++ several decades ago, and attribute their successful transition to their strong internal communities:
* 3 Pillars
    * Strong Community Interest
    * Organized communication and coordination
    * Organized technical support
* Guilds
    * serve as communities within an organization centered around certain technologies

&nbsp;
\
&nbsp;

### Understanding attributes (Or: They're not nearly as boring as you think!) - Reuven Lerner
#### **Recommend: Yes**

Reuven did a fantasic talk on how the attribute system works in python. Under the hood, everything is an object, and every dot '.' is accessing an attribute. 

He started by clarifying that, in python:  
`x = 100`  
does not mean assign 100 to memory space named x, but instead x references an integer which has an attribute 'value' of 100  
`x.y = 100`  
y is not a variable, it's an attribute

We can think of Classes as file-less modules
* functions defined in a class body are actually class attributes
* inside it looks like a variable, outside it's an attribute

The way Python resolves lookups is **I.C.P.O.**:
1. Instance - Does the specific instance has this attribute?
2. Class - If not, does the class definition has this attribute?
3. Parent - If not, does this class' parent have this attribute?
4. Object - If not, does the base object class have this attribute?

If the attribute is not found after ICPO, an AttributeError is raised.

an attribute may be a descriptor, which acts differently depending on whether its called via instance or class.

Example:  
`'abcd'.upper()`  
and  
`str.upper('abcd')`  
produce the same results

*Takeaway Item: Read more about descriptors*

&nbsp;
\
&nbsp;

### Distributed Web Scraping in Python - Josh Weissbock
#### **Recommend: Maybe**

Josh spoke about collecting data, specifically through web scraping. While interesting, I'm not sure how applicable it is to my current responsibilties.

Web Scraping
* Act of extracting data from websites
* Distributed means moving it across multiple computers
* Useful when you routinely collect data from the same source
* Issues
    * Slow
        * Can be fixed by distributing load across different machines
    * Bot Detection
        * Bot requests usually don't have headers, so add them (with different data)
        * Add random delays between each requests
        * Use selenium instead of beautifulsoup
        * fake-useragent package
    * Tracking / Duplicating Effort
        * Job/Result Queues
    * Failure Prevention
        * Add try-until-sucess wrappers (with timeouts)
    * Static vs Dynamic Content

&nbsp;
\
&nbsp;

### When to refactor your code into generators and how - Jan-Hein Bührman
#### **Recommend: Yes**

Jan-Hein used the example of a Fibonacci sequence function to demonstrate how generators can be preferable to iterators.

* Generators use *yield* instead of *return*
* Can be infinite
* Can be transformed into lists

If we wanted to get a number or create a list of numbers in the Fibonacci sequence based on some condition such as
* nth number
* numbers greater than x
* odd numbers

Without generators, we would need to create a function to get each number or list depending on which condition we wanted to implement.

With generators, we can use a singular generator object and use list comp to pull out whichever numbers we want.

Generators can also be used in conjunction with itertools to chunk large amounts of data.

&nbsp;
\
&nbsp;

### Implementing shared functionality using Middleware - Amit Saha
#### **Recommend: Maybe**

Middleware is:
* "Glue"
* "Interface between hardware and software"
* Runs before and/or after request processing, WSGI frameworks define their own mechanism to define middleware

While informative, I think there are probably better resources online for explaining them.

*Idea: Middleware to translate requests from Wordpress?*

&nbsp;
## Day Two
&nbsp;

### Keynote - Sara Issaoun
#### **Recommend: Maybe**

Sara Issaoun is a NASA Einsten Fellow and was one of 300+ members who contributed to the first imaging of a black hole back in 2019. This talk was **incredibly** interesting, however, it's not exactly related to SWE.

The team created a 'Digital' Telescope 13 million meters around the earth to focus on the black hole 55 million light years away.


The telescopes collected over 3 Petabytes of raw data. From there, they removed overlapping data, condensing the data size to Terrabytes. After that, they calibrating the data, unscrambling variables such as atmospheric data and getting averages. This brought the data down to megabytes. From here, the image was composed into a final file measured in kilobytes.

12 orders of magnitude in data reduction. It took 2 years.

&nbsp;
\
&nbsp;

### Keynote - Peter Wang
#### **Recommend: Yes**  

Peter Wang is the co-founder of Anaconda. He had a very exciting announcing to make regarding the alpha reveal of PyScript.

He said that python is...
* Excellent "Glue" Language, but stuck to everthings it's glued to
* "Honda Civic with mounting bolts for a warp drive"
* Cpython has a low level C API that lets programmers write huge numbers of high-performace bindings to C, C++, FORTRAN

This raised the question, can we ever unshackle Python from all this?

PyScript announcement
* https://pyscript.net/
* JavaScript Alternative with full DOM control


Built on WebAssembly
* Virtual CPU /instruction set
* 32-bit memory space (4gb)
* Supported by most modern browsers
* Runs almost everywhere


&nbsp;
\
&nbsp;

### Securing Code with the Python Type System - Graham Bleaney and Pradeep Kumar Srinivasan of Meta
#### **Recommend: Maybe**

While informative, the main takeaway was that it's best to catch bugs before they hit prod, and using a type-checker can help catch these errors before they're committed to the codebase. The focus of the talk seemed to be moreso on Meta's type checker, Pyre.

Bugs can be found on a spectrum:
* Prevented > Auto > Manual > External > Never > Exploited
    * Catching them in the 2 leftmost phases is crucial

The speakers proposed that type Annotations can help secure your application
* Side note: Bandit Linter can check security issues
* MonkeyType captures runtime type info for use in static type annotations
* Use Pyre type checker
* Pyre Infer: Propagates types already availble to the type checker

Roadmap:
1. Enforce types in your API
2. Start using a type checker, Locally and in CI
3. Expand coverage with Pyre infer, MonkeyType and manual annotations
4. Start running Pysa to detect dataflow based vulnerabilities

&nbsp;
\
&nbsp;

### Let's talk about JWT - Jessica Temporal
#### **Recommend: No**

Jessica did a great job explaining JWTs and their use cases, but ultmately, it was just the information already available on https://jwt.io/

&nbsp;
\
&nbsp;

### Making Data Classes Work for You - Bruce Eckel
#### **Recommend: Yes**


Data classes create three dunder methods for a class:
1. `__eq__` to compare instances of the data class
2. `__init__` to initialize the attributes of the data class
3. `__repr__` to describe the representation of the data class


Usable with replace() function, which can replace an object's attribute value


Dataclasses are not hashable because all properties are mutable, and therefore cannot be used as dict keys. However, if you set the parameter 'frozen=true' in the dataclass wrapper, the dataclass will act as if it is immutable and can therefore be hashed/used as a dict key.

Attempting to change a frozen dataclass raises a frozen error.

**A class is not a type** but rather *a set of values*

Add data validation as part of the dataclass `__post_init__` function.

Person example, use dataclasses for FullName, Phone, Birthdate so that you don't have to validate them inside the person object, keeping it cleaner.

A common misconception is that dataclasses are somehow 'leaner' versions of concrete classes that have functionality stripped away since they are just being used for data. However, the contrary is true. Dataclasses do not strip functionality away from concrete classes, and in most cases will actually require **more** resources than a concrete class because of the auto-implemented dunder methods.

&nbsp;
\
&nbsp;

### Making Python better one error message at a time - Pablo Galindo Salgado
#### **Recommend: Yes**

Pablo Galindo Salgado is a Python Core Developer and a member of the Steering Council. He has the 2nd most contributions to the Python language. He was also the release manager for Python versions 3.10 and 3.11

Pablo introduced the PEG Parser ("Parser Expression Grammar"). He explained previous issues with how Python was parsed and the need for the updates. He continued by describing the challenges encountered when trying to target new error messages.

New Errors captured with the PEG Parser
https://devguide.python.org/parser/ 
* Colon Expected
* using = when you meant ==
* Forgotten comma in dict, list
* Indention Error
* Unclosed Brackets
* Attribute on Null value
* Nonetype in nested subscriptable identification
* Division by Zero Identification

&nbsp;
\
&nbsp;

### Writing Docs Devs Love - Mason Egger
#### **Recommend: Maybe**

Unfortunately, there were technical difficulties and this broadcast got messed up. It looks like the video is now available so I'd like to go back and watch it, but I was able to find the presentation slides on Mason's site.

https://masonegger.com/docs/docs-devs-love.pdf

&nbsp;
\
&nbsp;

### Writing Functional Code in Python - Vic Kumar
#### **Recommend: No**

In functional programming, you should write functions that don't have side effects
* modifying variable
* modifying data structures
* setting field on obj
* drawing on screen
* reading from or writing to file
* printing to console
* throwing exception

This is an interesting premise which I believe can be adapted to OOP in some capacity to help write cleaner code.

Vic went on to demonstrate a functional program in Python. While informative, I am not particularly attracted to the functional programming style, which aims to read left-to-right like text. While it sounds nice, the implementation introduces design patterns that aren't intuitive.

&nbsp;
\
&nbsp;

### Write faster Python! Common performance anti-patterns - Anthony Shaw
#### **Recommend: Yes**

Anthony Shaw, author of CPython Internals, describes how to identify "Hot Loops" and other processing-intensive anti-patterns in python, and how to fix them.

He said that while other methods exist which can help you improve program speed, the number one method to get better results is to optimize existing code. He goes on to break this down and suggest fixes.

* Micro-Optimizing
    * DO:
        * Meuasure before chaning
        * vary outputs
        * isolate changes
        * reproduce impact 1000s of times
    * DONT
        * assume the impact will be the same accros python versions
        * make changes for ~ <10% improvements
* Benchmakring
    * Tracing Profiler
        * Can Slow down code
    * Sampling profile
* Pyflint
    * Loop Invariance
    * List Comps are faster than for loops
    * Inefficient Data Structures
    * Reduce Mapping whenever possible
* Concrete classes are faster than dataclasses and namedtuples, but are more code & less readable
* Calling too many functions
    DRY, BUT python has overhead to calling functions
    * Small util funcs in hot loops
* Use Match statements for sequences and mappings

&nbsp;
## Day Three
&nbsp;

### Keynote - Python Steering Council
#### **Recommend: Maybe**

What is the Steering Council?
    * Defined in PEP 13
    * In Charge of Python (The Language) and CPython (The Implementation)
    * Govern by Consensus
    * Meet Weekly, Separate from the PSF (but in good relation)
    * Pushblish monthly updates github/python/steering-council

Highlights of the Year?
    * Bugs.python.org migrated to github issues
    * Hired Developer in Residence (Lukasz Langa)

What's new in Python 3.11
    * More Specfic Exceptions
    * Speed Increase speed.python.org 
    * Typing improvements
        * Collateral improvement: Unpack in middle of list
    * LiteralString typing

&nbsp;
\
&nbsp;

### Getting Started With Statically Yyped Python - Peacock
#### **Recommend: No**

While informative, the talk covered pretty much the same information that can be found in this article:   
https://realpython.com/python-type-checking/

&nbsp;
\
&nbsp;

### Speed Up Data Access with PyArrow (Apache Arrow) - Data is the new API - Deepak K Gupta
#### **Recommend: ?**

Constituents of a Software Program:
1. Data
2. Functions

Apache Arrow
1. "is primarily a specification" of data
2. language-independant columnar memory format for flat and heirarchical data
3. Has libraries in multiple languages
    * In Python, this is PyArrow

You have to serialize and deserialize data when communicating with dbs. This can take some time. So what if this didn't need to happen?

"Data is the new API"
* When we are getting data, it is possible for the data to self-describe
* In-memory columnar data

PyArrow includes functions than can be used directly on the data:
* Vector, Scalar, Aggregate functions

"Speed up data access"
1. Arrow is faster than pandas read_csv
    * you can read csv and convert arrow to pandas faster than reading csv in pandas
2. Memory Mapped File

&nbsp;
\
&nbsp;

### Keynote - Naomi Ceder
#### **Recommend: Maybe**

Naomi Ceder has been a part of PyCon since the first event in 2003 and was a large part of many initiaves the PSF has taken since then. She is the immediate past chair of the PSF's board of directors.

She gave a heart-felt speech on the realities of the Open Source community. She explained how people's passion for contributing to projects is a gift that is more often than not taken for granted. This burns people out and drives them away from the community. She asks project leaders to trust more in the community to off-load the burden and train replacements, so they can take breaks as needed to stay fresh.

It was a great talk overall, and refreshing to see the efforts the PSF is taking to remain respectful to corporate sponsors while simultaniously avoiding becoming a business in which they are clients.
