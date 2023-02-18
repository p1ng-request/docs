# Markdown in Jupyter

Text can be added to Jupyter Notebooks using Markdown cells.\
Markdown is a popular markup language that is a superset of HTML. Its specification can be found [here](https://daringfireball.net/projects/markdown/).\
You can change the cell type to Markdown by clicking on the dropdown on the top menu, or with a hardware keyboard shortcut `m` on your selected celle.

### Markdown basics

You can make text _italic_ or **bold**.

You can build nested itemized or enumerated lists:

* One
  * Sublist
    * This
  * Sublist - That - The other thing
* Two
  * Sublist
* Three
  * Sublist

Now another list:

1. Here we go
   1. Sublist
   2. Sublist
2. There we go
3. Now this

You can add horizontal rules:

***

Here is a blockquote:

> Beautiful is better than ugly. Explicit is better than implicit. Simple is better than complex. Complex is better than complicated. Flat is better than nested. Sparse is better than dense. Readability counts. Special cases aren't special enough to break the rules. Although practicality beats purity. Errors should never pass silently. Unless explicitly silenced. In the face of ambiguity, refuse the temptation to guess. There should be one-- and preferably only one --obvious way to do it. Although that way may not be obvious at first unless you're Dutch. Now is better than never. Although never is often better than _right_ now. If the implementation is hard to explain, it's a bad idea. If the implementation is easy to explain, it may be a good idea. Namespaces are one honking great idea -- let's do more of those!

And a simple way to create links:

[Jupyter's website](http://jupyter.org)

### Headings

You can add headings by starting a line with one (or multiple) `#` followed by a space, as in the following example:

```
# Heading 1
# Heading 2
## Heading 2.1
## Heading 2.2
```

### Embedded code

You can embed code meant for illustration instead of execution in Python:

```
def f(x):
    """a docstring"""
    return x**2
```

or other languages:

```
if (i=0; i<n; i++) {
  printf("hello %d\n", i);
  x += 4;
}
```
