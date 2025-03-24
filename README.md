# srs-latex
Support for software engineering tasks in LaTeX2e.  
These include:
- User & Software requirements
- Use cases
- Components
- Verification & validation tests
- Autogeneration of traceability matrixes between them

You can find a full example in [`example.tex`](example.tex)/[`example.pdf`](example.pdf).



## Usage
First, store the [`srs.sty`](srs.sty) file in the same directory as your main `.tex` file, and include the package:
```latex
\usepackage[en,enableTraceability,enableCaptions]{srs}
```

### Configuration
- To set the language, choose either the `en` (English) or the `es` (Spanish) option.
- To enable the computation of the traceability matrixes, set the `enableTraceability` option
- To enable captions on the requirement tables, set the `enableCaptions` option


### Requirements
Each requirement has a type, a subtype, and an ID. The combination of these parameters uniquely identify a requirement.

The different types and subtypes are:
- User requirement
    - Capacity (`CA`)
    - Restriction (`RE`)
- Software requirement
    - Functional (`FN`)
    - Non-Functional (`NF`)

The general syntax of the user requirements is the following:
```latex
\begin{userReq}{<subtype>}{<id>}{<properties>}
  <description>
\end{<type>}
```

The general syntax is the following:
```latex
\begin{userReq}{<subtype>}{<id>}{<properties>}{<origin-list>}
  <description>
\end{<type>}
```

> [!NOTE]
> The `<origin-list>` is a list of comma-separated `<subtype>-<id>`, used to track the traceability between software and user requirements.


#### Properties
The properties of the requirement are the following:
- `pc` - Client priority: Can be high (`h`), medium (`m`) or low (`l`)
- `pd` - Developer priority: Can be high (`h`), medium (`m`) or low (`l`)
- `s` - Stability: Can be constant (`c`), inconstant (`i`) or very unstable (`vu`)
- `v` - Verifiability: Can be high (`h`), medium (`m`) or low (`l`)


### Use cases
The general syntax is the following:
```latex
\begin{useCase}{<id>}
  {<name>}
  {<actors>}
  {<objective>}
  {<pre-conditions>}
  {<post-conditions>}
  <description>
\end{<type>}
```


### Components
The general syntax is the following:
```latex
\begin{component}{<id>}
  {<role>}
  {<dependencies>}
  {<input-data>}
  {<output-data>}
  {<origin-list>}
  <description>
\end{<type>}
```

> [!NOTE]
> The `<origin-list>` is a list of comma-separated `<subtype>-<id>`, used to track the traceability between software requirements and components.


### Tests
There are two subtypes:
- Verification tests (`VET`)
- Validation tests (`VAT`)

The general syntax is the following:
```latex
\begin{testCase}{<subtype>}{<id>}
  {<precondition>}
  {<postcondition>}
  {<description>}
  {<evaluation>}
  {<origin-list>}
  <procedure>
\end{<type>}
```


### Templates
To simplify the _tedious_ process of defining how the requirements are defined, you have some helpful commands that do the work for you:
- `\printureqtemplate`: Prints the User Requirements template
- `\printsreqtemplate`: Prints the Software Requirements template
- `\printuctemplate`: Prints the Use Case template
- `\printtesttemplate`: Prints the Test template


### References
To reference the different elements, you can use one of the following functions:
- `\ureqref[<prefix>]{<subtype>-<id>}`: References user requirement of subtype `<subtype>` `<id>`
- `\sreqref[<prefix>]{<subtype>-<id>}`: References user requirement of subtype `<subtype>` `<id>`
- `\ucref[<prefix>]{<id>}`: References use case `<id>`
- `\testcref[<prefix>]{<subtype>-<id>}`: References test case of subtype `<subtype>` `<id>`
- `\compref[<prefix>]{<id>}`: References component `<id>`


### Traceability matrixes
We provide you with the most common traceability matrixes, easily accesible trough the following commands:
- `\traceabilityFNCA`: Traceability between functional software requirements and capabilities
- `\traceabilityNFRE`: Traceability between non-functional software requirements and restrictions
- `\traceabilityCompFN`: Traceability between components and functional software requirements
- `\traceabilityVETSR`: Traceability between verification tests and software requirements
- `\traceabilityVATUR`: Traceability between validation tests and user requirements

> [!IMPORTANT]
> Remember to set the `enableTraceability` option when importing the package.

#### Custom matrixes
To generate custom traceability matrixes, you can make use of the `\traceabilityPrintMatrix` command. This commands use [Lua Patterns](https://www.lua.org/pil/20.2.html) to search the _displayed_ IDs.


> [!NOTE]
> There is a difference between the _reference_ ID and the _displayed_ ID. The _reference_ ID is the one you provide in your code, e.g. `cool-req`, and is relative to the specific type and subtype. This then automatically numerated and converted into the _displayed_ ID, e.g. `UR-CA-01`.
>
> There is also an _internal_ intermediate representation, that would be `UR-CA-cool-req`, but that's a problem for the maintainers.

The general syntax is:
```latex
\traceabilityPrintMatrix{<item-pattern>[,...]}{<origin-pattern>[,...]}{<options>}
```
where `<options>` may include values for `[io]_offset=N` (skip N items/origins) and `[io]_count=N` (number of items/origins to typeset).

> [!NOTE]
> Note that in patterns, `-` is a special character an should be escaped, using `\37`.


## Compilation
This requires [LaTeX](https://www.latex-project.org/) (_duh_) and [LuaTeX](https://www.luatex.org/).

To compile the example with `latexmk`, use the following command:
```latex
latexmk -pdflua example.tex
```
