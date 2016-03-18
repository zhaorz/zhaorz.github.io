---
layout: post
title: Markdown
---

This page contains most of the standard Markdown elements.

<!--excerpt-->

Below is just about everything you'll need to style in the theme. Check the source code to see the many embedded elements within paragraphs.

---

# Heading 1

## Heading 2

### Heading 3

#### Heading 4

##### Heading 5

###### Heading 6

---

Lorem ipsum dolor sit amet, <a title="test link" href="#">test link</a> adipiscing elit. <strong>This is strong.</strong> Nullam dignissim convallis est. Quisque aliquam. <em>This is emphasized.</em> Donec faucibus. Nunc iaculis suscipit dui. 5<sup>3</sup> = 125. Water is H<sub>2</sub>O. Nam sit amet sem. Aliquam libero nisi, imperdiet at, tincidunt nec, gravida vehicula, nisl. <cite>The New York Times</cite> (That's a citation). <span style="text-decoration:underline;">Underline.</span> Maecenas ornare tortor. Donec sed tellus eget sapien fringilla nonummy. Mauris a ante. Suspendisse quam sem, consequat at, commodo vitae, feugiat in, nunc. Morbi imperdiet augue quis tellus.

<abbr title="Hyper Text Markup Language">HTML</abbr> and <abbr title="Cascading Style Sheets">CSS</abbr> are our tools. Mauris a ante. Suspendisse quam sem, consequat at, commodo vitae, feugiat in, nunc. Morbi imperdiet augue quis tellus.  Praesent mattis, massa quis luctus fermentum, turpis mi volutpat justo, eu volutpat enim diam eget metus. To copy a file type <code>COPY <var>filename</var></code>. <del>Dinner's at 5:00.</del> <ins>Let's make that 7.</ins> This <span style="text-decoration:line-through;">text</span> has been struck.

---

## Text-level semantics


The <a href="#">a element</a> example
The <abbr>abbr element</abbr> and <abbr title="Title text">abbr element with title</abbr> examples
The <b>b element</b> example
The <cite>cite element</cite> example
The <code>code element</code> example
The <del>del element</del> example
The <dfn>dfn element</dfn> and <dfn title="Title text">dfn element with title</dfn> examples
The <em>em element</em> example
The <i>i element</i> example
The <ins>ins element</ins> example
The <kbd>kbd element</kbd> example
The <mark>mark element</mark> example
The <q>q element <q>inside</q> a q element</q> example
The <s>s element</s> example
The <samp>samp element</samp> example
The <small>small element</small> example
The <span>span element</span> example
The <strong>strong element</strong> example
The <sub>sub element</sub> example
The <sup>sup element</sup> example
The <var>var element</var> example
The <u>u element</u> example

---

## Code

Code can be presented inline, like <code>&lt;?php bloginfo('stylesheet_url'); ?&gt;</code>, or within a <code>&lt;pre&gt;</code> block.

Automatic syntax highlighting is provided by the markdown processor, which uses
rouge to perform the highlighting. Enclose any code in a fenced block:

<pre><code>~~~ lang
# ... code here

~~~</code></pre>

~~~ sml
(* make_change: int list -> int -> (int list -> 'a) ->
 *                          (unit -> 'a) -> 'a *)
fun make_change L 0 s k = s []
  | make_change [] n s k = k ()
  | make_change (x::xs) n s k =
      if n - x >= 0 then
        make_change xs (n - x)
          (fn A => s(x::A))
          (fn () => make_change xs n s k)
      else
        make_change xs n s k
~~~

---

## Blockquotes

Let's keep it simple. Italics are good to help set it off from the body text. Be sure to style the citation.

> Good afternoon, gentlemen. I am a HAL 9000 computer. I became operational at the H.A.L. plant in Urbana, Illinois on the 12th of January 1992. My instructor was Mr. Langley, and he taught me to sing a song. If you'd like to hear it I can sing it for you. <cite>— [HAL 9000](http://en.wikipedia.org/wiki/HAL_9000)</cite>

And here's a bit of trailing text.

---

## Media

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore.

### Big Image

![Test Image](http://demo.ghost.io/content/images/2014/09/testimg1.jpeg)

Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.

### Small Image

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore.

![Small Test Image](http://demo.ghost.io/content/images/2014/09/testimg2.jpg)

Labore et dolore.

---

## List Types

### Definition List

<dl>
<dt>Definition List Title</dt>
<dd>This is a definition list division.</dd>
<dt>Definition</dt>
<dd>An exact statement or description of the nature, scope, or meaning of something: <em>our definition of what constitutes poetry.</em></dd>
</dl>

### Ordered List

1. List Item 1
2. List Item 2
   1. Nested list item A
   2. Nested list item B
3. List Item 3

### Unordered List

* List Item 1
* List Item 2
   * Nested list item A
   * Nested list item B
* List Item 3

---

## Table

<table>
<tbody>
<tr>
<th>Table Header 1</th>
<th>Table Header 2</th>
<th>Table Header 3</th>
</tr>
<tr>
<td>Division 1</td>
<td>Division 2</td>
<td>Division 3</td>
</tr>
<tr class="even">
<td>Division 1</td>
<td>Division 2</td>
<td>Division 3</td>
</tr>
<tr>
<td>Division 1</td>
<td>Division 2</td>
<td>Division 3</td>
</tr>
</tbody>
</table>

---

## Forms

<form>
  <fieldset>
    <legend>Legend</legend>

    <label for="email">Email</label>
    <input id="email" type="email" placeholder="Email">

    <label for="password">Password</label>
    <input id="password" type="password" placeholder="Password">

    <label for="state">State</label>
    <select id="state">
        <option>AL</option>
        <option>CA</option>
        <option>IL</option>
    </select>

    <label for="remember" class="checkbox">
        <input id="remember" type="checkbox"> Remember me
    </label>

    <button type="submit" class="button">Sign in</button>

  </fieldset>
</form>

---

