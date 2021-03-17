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
Once that model is in memory, we use an HTML generator, whose job is to produce a specific code for the person's website.
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
 
![Screenshot 2021-03-17 at 10 14 22](https://user-images.githubusercontent.com/26929529/111443315-8d4cad00-8709-11eb-8114-a51cf60580ba.png)

## The problem

## Your task
