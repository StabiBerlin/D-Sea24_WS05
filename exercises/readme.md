# XML + XPATH basics

----

## XML

----

### Exercise 1

Create a first document with one "root" element

- Open eXide
- Create a new XML document in eXide 
- Press "New" in the top row of buttons
- then "Create" in the following dialog

----

```
<root/>
```

- Root node
- Unary tag
- Element

----

Can also be written as

```
<root></root>
```

- Empty tag

----

### Exercise 2

Now create a new element "other"

----

<!--
<root/>
<other/>
-->

```
<root>
  <other />
</root>
```

- Well-formed
- open tag
- Closing tag
- Child element 
- Parent element

----

### Exercise 3

Add an attribute "id" to the "other" element with any value

```
<element attribute="value" />
```

----

```
<root>
  <other id=“special”/>
</root>
```

- attributes are children of the element _and_ its parent elements

----

### Exercise 4

- Add an element "child" to the root node.
- Add an element "other" as _its_ child and set its text content to "test".

----

```
<root>
  <other id=“special”/>
  <child>
    <other>test</other>
  </child>
</root>
```

----

### Exercise 5

Save this document in eXide

File > Save > my-doc.xml

----

## Namespaces

The X in XML stands for extensible.
Namespaces can be used to extend existing encodings with new elements and to validate
documents agains a schema

- `xmlns=http://www.tei-c.org/ns/1.0`

----

### Exercise 6

Encode a Poem in a TEI document

----

— pause

----

## XPath

- `/` selects the _children_ of a node
- `//` selects the _descendants_ of a node
- `.` represents the _current_ node
- `..` represents the _parent_ node

- `<a><b/></a>/b` will select the `b` element inside the `a` node

----

- Create a new XQuery document in eXide
- Using the "New XQuery"-button
- copy and paste the contents of your first document in your new XQuery file
- either after `xquery version "3.1";` or replace the contents entirely

----

### Exercise 7

Select the "other" element that is the direct child of "root"

Hint: use `/` 

----

```
<root>
  <other id=“special”/>
  <child>
    <other>test</other>
  </child>
</root>
/other
```

----

### Exercise 8

Select all descendant "other" elements of "root"

Hint: use `//` 

----

```
<root>
  <other id=“special”/>
  <child>
    <other>test</other>
  </child>
</root>
//other
```
----

### Exercise 9

Select all text inside the root element

- with `text()` you can select the textual contents of an element 

----

```
<root>
  <other id=“special”/>
  <child>
    <other>test</other>
  </child>
</root>
/text()
```

----

How does the output change with  `//text()` or `//other/text()`?

----

## Selecting attributes

- with `@id` you can select the id attribute

----

### Exercise 10

Select the id attribute of "other" elements

Hint: use `//` with `/` _and_ `@id`

----

```
<root>
  <other id=“special”/>
  <child>
    <other>test</other>
  </child>
</root>
//other/@id
```
----

To get to the text part of the attribute use 

```
//other/@id/string()
```

----

## Filtering selections with predicates

Predicates are in square brackets following a selection or node (set)

- `<a><b/><c/>[CONDITION]`
- `/b[CONDITION]`

----

### Exercise 11

Select all "other" elements with an id-attribute "root"

Hint: use `@id` in a predicate

----

```
<root>
  <other id=“special”/>
  <child>
    <other>test</other>
  </child>
</root>
//other[@id]
```

----

TIP: you can invert the selection with `not()`

```
<root>
  <other id=“special”/>
  <child>
    <other>test</other>
  </child>
</root>
//other[not(@id)]
```

----

### Exercise 12

Select the parent of the "other" element without an id-attribute

Hint: use `not()` in a predicate and `/..` to select the parent

----

```
<root>
  <other id=“special”/>
  <child>
    <other>test</other>
  </child>
</root>
//other[not(@id)]/..
```

----

### Exercise 13

Loading a document and selecting all other elements

Hint: use `doc("/db/my-doc.xml")` to load the document we created earlier

----

```
doc("/db/my-doc.xml")//other
```
