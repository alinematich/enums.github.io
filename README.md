# نحوه ی استفاده از اینام در پایتون
### چگونه در پایتون می توانیم از اینام آماده استفاده کنیم

از پایتون 3.4 اینام به پایتون اضافه شد و شما با دستورات زیر میتوانید آن را نصب کنید:

```enum34:   $ pip install enum34
aenum:    $ pip install aenum```

و به صورت زیر آن ها را استفاده کنید:

`from enum import Enum     # for enum34, or the stdlib version`
`# from aenum import Enum  # for the aenum version`
`Animal = Enum('Animal', 'ant bee cat dog')`
`Animal.ant  # returns <Animal.ant: 1>`
`Animal['ant']  # returns <Animal.ant: 1> (string lookup)`
`Animal.ant.name  # returns 'ant' (inverse lookup)`

و یا به این صورت:

`class Animal(Enum):`
    `ant = 1`
    `bee = 2`
    `cat = 3`
    `dog = 4`

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/alinematich/enums.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
