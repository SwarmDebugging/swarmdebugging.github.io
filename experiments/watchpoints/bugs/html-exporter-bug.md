---
layout: page
permalink: /bugs/html-exporter-bug/
---

# The HTML exporter bug
In this task, we provide you with a program exporting input data to HTML and a unit test to test it.
The unit test encounters a failure and cannot run completely.

The task is about understandind and fixing this unit test.

## Context: the website generator

We use a program that takes as input a model representing a person's CV, and generates HTML code for this person's website.
For instance, the following code represents an input for an academic publication:

```Smalltalk
  {
    #type: #journal,
    #title: 'Lub: A pattern for fine grained behavior adaptation at runtime',
    #authors: 'Steven Costiou, Mickaël Kerboeuf, Glenn Cavarlé, Alain Plantec',
    #year: 2018,
    #publisher: 'Science of Computer Programming, Volume 161, ISSN 0167-6423',
    #doi: 'https://doi.org/10.1016/j.scico.2017.09.006',
    #link: 'pdf/papers/lub-pattern.pdf'
  }
 ```
This input is processed by the software to produce an internal representation of that academic publication.
In that case, that would be an instance of a class named `CVGPublication`.
Once that model is in memory, we use an HTML writer object, whose job is to produce a specific code for the person's website.
In our case, it should generate the following HTML code: 
 
 ```HTML
<li>
  <b>Lub: A pattern for fine grained behavior adaptation at runtime</b>.
  <i>Steven Costiou</i>, Mickaël Kerboeuf, Glenn Cavarlé, Alain Plantec. 
  Science of Computer Programming, Volume 161, ISSN 0167-6423. 2018. 
  <span class="paper-pdf">
    <a href="pdf/papers/lub-pattern.pdf" target=_blank>
      <i class="material-icons md-18">link</i>
    </a>
  </span>
</li>
```
 
HTML writer objects are part of a set of classes whose job is to export the model into various formats.
For instance, in the following image we can see a code browser opened on the `CVGSimpleHTMLWriter` class (second column).
This writer class has several export protocols (third column), each one regrouping methods (fourth column) to export particular HTML markup.
To illustrate, we selected the `openListItem` method, whose job is to open an HTML list:
 
![Screenshot 2021-03-17 at 10 14 22](https://user-images.githubusercontent.com/26929529/111443315-8d4cad00-8709-11eb-8114-a51cf60580ba.png)

HTML writers generate output HTML on a stream, and manage HTML markup using a stack.
Let us take the example of an HTML list.
For that, let us assume that we use a writer object stored in a variable `writer`.
This writer has an empty stack, that we represent as the following:

| |
| :-------------: |
|  | 
|  | 

Let us open an ordered list: `writer startOrderedList`. 
The stack will become as follows:

| |
| :-------------: |
|  | 
| ol | 

And the writer will write the following HTML on its internal stream: `<ol>`.
Let us now write a list item: `writer listItem: 'hello world'`.
First, the generator will put a list item on the stack:

| |
| :-------------: |
| li | 
| ol | 

The writer then writes the following HTML on its internal stream:
```HTML
<ol>
  <li>'hello world'
```
Just after, the writer closes the markup by poping the stack, and closes the popped element in the HTML code:
| |
| :-------------: |
| | 
| ol | 

```HTML
<ol>
  <li>'hello world'</li>
```

We then close the list: `writer stopOrderedList`.
Similarly, the stack is popped and the popped element is closed in the HTML:
| |
| :-------------: |
| | 
| | 

```HTML
<ol>
  <li>'hello world'</li>
</ol>
```


## The problem

To test our HTML export, we write a unit test that takes as input the above academic publication data, and tests that the generated HTML corresponds to valid HTML code and to the expected format.
You will find this test in class `CVGGeneratorTest`, under the name `testGeneratePublication`. 

```Smalltalk
testGeneratePublication

	| publication generator |
	publication := self publication.
	generator := CVGGenerator new.
	generator html.
	publication acceptGenerator: generator.
	self
		assert: generator stream contents
		equals:
		'<li>
       <b>Lub: A pattern for fine grained behavior adaptation at runtime</b>.
       <i>Steven Costiou</i>, Mickaël Kerboeuf, Glenn Cavarlé, Alain Plantec. 
        Science of Computer Programming, Volume 161, ISSN 0167-6423. 2018. 
        <span class="paper-pdf">
          <a href="pdf/papers/lub-pattern.pdf" target=_blank>
            <i class="material-icons md-18">link</i>
          </a>
        </span>
     </li>>'
 ```
The test first create the publication model from the input data, then instantiate a generator.
The generator is set to the *html* mode, and is passed to the publication object.
The publication object will ask the generator to output the publication data.
The generator will transform that publication to HTML (as we set the *html* mode) using an HTML writer.

Unfortunately, the test cannot complete because it encounters a bug.
When you try to run it, it starts but its execution stops and a debugger opens.

## Your task

For this task, you must:
* Understand the problem and explain it when you think you found it
* Fix the problem and the test must pass

To explain the problem, you will provide a few sentences describing what you understood.
