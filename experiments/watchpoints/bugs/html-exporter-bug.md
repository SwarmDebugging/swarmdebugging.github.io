# bug description 

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

HTML writers generate output HTML markup using a simple stack.
Let us take the example of an HTML list.
For that, let us assume that we use a writer object stored in a variable `writer`.
This writer has an empty stack, that we represent as the following:

| |
| :------------- |
|  | 
|  | 




## The problem

## Your task
