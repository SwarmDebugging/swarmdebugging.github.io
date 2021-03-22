---
layout: page
permalink: /microdown-comment-bug
---

<!---# The microdown comment bug-->
In this task, we demonstrate a failure in the development environment of Pharo.
Trying to comment a class with a particular string provokes the opening of a debugger.

The task is about understanding and fixing this bug.

## Context: commenting a class

To comment a classe, one has to first open a system browser through the general menu: <br>
*Browse > System browser*.

Then, as illustrated in the following picture:
1. Select a class (for the purpose of this task, you can select any)
2. Click the *comment* pane in the text editor
3. Untick the *toggle edit* checkbox to be able to edit the text

![Screenshot 2021-03-22 at 14 39 34](https://user-images.githubusercontent.com/26929529/111998842-b3fd5000-8b1c-11eb-92d5-bcf3c2914ff1.png)

From there, you can write your class comment and save it by doing a right click in the editor and click *Accept*, or by doing *CTRL + S* (*CMD* for Mac users).

## The problem

If you try to copy/paste this string into the comment text editor, and then save it, the system crashes and opens a debugger on a primitive failure:

```
I'm a simple lexer. I'm used bt the DLitlleLParser.

I recogniseI
- names: list of characters letter and number and '
- separators: one character separator.
- escape char \

Whitespaces and separators can be customised using setters.
Subclasses may change the definition of names by redefining isCurrentALetter.
```
