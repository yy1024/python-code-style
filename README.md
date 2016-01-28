介绍（Introduction）
============

这篇文档说明了Python主要发行版中标准库代码所遵守的规范。请参考实现Python的C代码风格指南信息PEP。

这篇文档和PEP 257(Docstring Conventions)都改编自Guido(译注：Python之父)最早的Python风格指南文章，并加入了Barry风格指南里的内容。

语言自身在发生着改变，随着新的规范的出现和旧规范的过时，代码风格也会随着时间演变。

很多项目都有自己的一套风格指南。若和本指南有任何冲突，应该优先考虑其项目相关的那套指南。

保持盲目的一致是头脑简单的表现(A Foolish Consistency is the Hobgoblin of Little Minds)

(注：标题语出自Ralph Waldo Emerson, Hobgolin意指民间故事中友好但常制造麻烦的动物角色。)

Guido的一个重要观点是代码被读的次数远多于被写的次数。这篇指南旨在提高代码的可读性，使浩瀚如烟的Python代码风格能保持一致。正如PEP 20那首《Zen of Python》的小诗里所说的：“可读性很重要(Readability counts)”。

这本风格指南是关于一致性的。同风格指南保持一致性是重要的，但是同项目保持一致性更加重要，同一个模块和一个函数保持一致性则最为重要。

然而最最重要的是：要知道何时去违反一致性，因为有时风格指南并不适用。当存有疑虑时，请自行做出最佳判断。请参考别的例子去做出最好s的决定。并且不要犹豫，尽管提问。

特别的：千万不要为了遵守这篇PEP而破坏向后兼容性！

如果有以下借口，则可以忽略这份风格指南：

* 当采用风格指南时会让代码更难读，甚至对于习惯阅读遵循这篇PEP的代码的人来说也是如此。

* 需要和周围的代码保持一致性，但这些代码违反了指南中的风格（可是时历史原因造成的）——尽管这可能也是一个收拾别人烂摊子的机会（True in XP style?）。

* 若是有问题的某段代码早于引入指南的时间，那么没有必要去修改这段代码。

* 代码需要和更旧版本的Python保持兼容，而旧版本的Python不支持风格指南所推荐的特性。



一致性考虑
======================================================

Guido的关键点之一是：代码更多是用来读而不是写。本指南旨在改善Python代码的可读性，即PEP 20所说的“可读性计数"(Readability counts)。

风格指南强调一致性。项目、模块或函数保持一致都很重要。

最重要的是知道何时不一致, 有时风格指南并不适用。当有疑惑时运用你的最佳判断，参考其他例子并多问！

特别注意：不要因为遵守本PEP而破坏向后兼容性！

部分可以违背指南情况：

* 遵循指南会降低可读性。

* 与周围其他代码不一致。

* 代码在引入指南完成，暂时没有理由修改。

* 旧版本兼容。


代码布局
============

缩进
-----------

每级缩进用4个空格。

括号中使用垂直隐式缩进或使用悬挂缩进。后者应该注意第一行要没有参数，后续行要有缩进。

Yes:

    # 对准左括号
    foo = long_function_name(var_one, var_two,
                             var_three, var_four)

    # 不对准左括号，但加多一层缩进，以和后面内容区别
    def long_function_name(
            var_one, var_two, var_three,
            var_four):
        print(var_one)

    # 悬挂缩进必须加多一层缩进
    foo = long_function_name(
        var_one, var_two,
        var_three, var_four)

No:

    # 不使用垂直对齐时，第一行不能有参数.
    foo = long_function_name(var_one, var_two,
        var_three, var_four)

    # 参数的缩进和后续内容缩进不能区别
    def long_function_name(
        var_one, var_two, var_three,
        var_four):
        print(var_one)

4个空格的规则对于续行是可选的，可以不是4个空格

例如:

    # 缩进2个空格
    foo = long_function_name(
      var_one, var_two,
      var_three, var_four)

f语句跨行时，两个字符关键字(比如if)加上一个空格，再加上左括号构成了很好的缩进。后续行暂时没有规定，至少有如下三种格式。

    # 没有额外缩进
    if (this_is_one_thing and
        that_is_another_thing):
        do_something()

    # 添加注释
    if (this_is_one_thing and
        that_is_another_thing):
        # Since both conditions are true, we can frobnicate.
        do_something()

    # 额外添加缩进
    if (this_is_one_thing
            and that_is_another_thing):
        do_something()

右边括号也可以另起一行。有两种格式：

* 右括号缩进
	
		my_list = [
        	1, 2, 3,
        	4, 5, 6,
        	]
    	result = some_function_that_takes_arguments(
        	'a', 'b', 'c',
        	'd', 'e', 'f',
        	)
* 右括号不缩进

    	my_list = [
        	1, 2, 3,
        	4, 5, 6,
    	]
    	result = some_function_that_takes_arguments(
        	'a', 'b', 'c',
        	'd', 'e', 'f',
    	)


空格或Tab?
---------------

* 空格是首选的缩进方法。

* Tab仅仅在已经使用tab缩进的代码中为了保持一致性而使用。

* Python 3中不允许混合使用Tab和空格缩进。

* Python 2的包含空格与Tab和空格缩进的应该全部转为空格缩进。

Python2命令行解释器使用-t选项时有非法混合Tab和空格的情况会告警。当使用-tt警告提升为错误。强烈推荐这些选项！另外个人推荐pep8和autopep8模块。

最大行宽
-------------------

限制所有行的最大行宽为79字符。

文本长块，比如文档字符串或注释，行长度应限制为72个字符。

多数工具默认的续行功能会破坏代码结构，使它更难理解，不推荐使用。但是超过80个字符加以提醒是必要的。一些工具可能根本不具备动态换行功能。

一些团队强烈希望更长的行宽。如果能达成一致，可以从从80提高到100个字符(最多99个字符)增加了标称线的长度，不过依旧建议文档字符串和注释保持在72的长度。

Python标准库比较保守，限制行宽79个字符(文档字符串/注释72）。

续行的首选方法是使用小括号、中括号和大括号反斜线仍可能在适当的时候。其次是反斜杠。比如with语句中：

    with open('/path/to/some/file/you/want/to/read') as file_1, \
         open('/path/to/some/file/being/written', 'w') as file_2:
        file_2.write(file_1.read())

类似的还有assert。

注意续行要尽量不影响可读性。比如通常在二元运算符之后续行：

    class Rectangle(Blob):

        def __init__(self, width, height,
                     color='black', emphasis=None, highlight=0):
            if (width == 0 and height == 0 and
                    color == 'red' and emphasis == 'strong' or
                    highlight >                     100):
                raise ValueError("sorry, you lose")
            if width == 0 and height == 0 and (color == 'red' or
                                               emphasis is None):
                raise ValueError("I don't think so -- values are %s, %s" %
                                 (width, height))
            Blob.__init__(self, width, height,
                          color, emphasis, highlight)

空行
-----------

* 两行空行分割顶层函数和类的定义。

* 类的方法定义用单个空行分割。

* 额外的空行可以必要的时候用于分割不同的函数组，但是要尽量节约使用。

* 额外的空行可以必要的时候在函数中用于分割不同的逻辑块，但是要尽量节约使用。

* Python接 contol-L作为空白符；许多工具视它为分页符，这些要因编辑器而异。

源文件编码
--------------------

在核心Python发布的代码应该总是使用UTF-8(ASCII在Python 2)。

ASCII文件(Python 2)或UTF-8(Python 3)不应有编码声明。

标准库中非默认的编码应仅用于测试或当注释或文档字符串,比如包含非ASCII字符的作者姓名，尽量使用\x , \u , \U , or \N。

Python 3.0及以后版本，PEP 3131可供参考，部分内容如下：在Python标准库必须使用ASCII标识符，并尽量只使用英文字母。此外字符串和注释也必须用ASCII。唯一的例外是：（a）测试非ASCII的功能，和（b）作者的名字不是拉丁字母。


Imports
-------

- 导入类库最好是单行:

      Yes: 
      	
      	import os
      	import sys

      No:  
      	import sys, os

  这样也可以:

      from subprocess import Popen, PIPE

- 导入始终在文件的顶部，在模块注释和文档字符串之后，在模块全局变量和常量之前。

  导入顺序:

  1. 标准库
  2. 相关的第3方库
  3. 本地库

  这3组的导入之间要有空行。

- 推荐绝对路径导入，因为它们通常更可读，而且往往是表现更好的（或至少提供更好的错误消息）:

    	import mypkg.sibling
    	from mypkg import sibling
    	from mypkg.sibling import example

  在绝对路径比较长的情况下，也可以使用相对路径:

    	from . import sibling
    	from .sibling import example

  Python 3中已经禁止隐式的相对导入。

- 导入类的方法:

      from myclass import MyClass
      from foo.bar.yourclass import YourClass

  如果和本地名字有冲突:

      import myclass
      import foo.bar.yourclass

  使用 "myclass.MyClass" 和 "foo.bar.yourclass.YourClass".

- 禁止使用通配符导入

  通配符导入(from <module> import *)应该避免，因为它不清楚命名空间有哪些名称存，混淆读者和许多自动化的工具。唯一的例外是重新发布对外的API时可以考虑使用。


字符串引用
=============

Python中单引号字符串和双引号字符串都是相同的。注意尽量避免在字符串中的反斜杠以提高可读性。

根据PEP 257, 三个引号都使用双引号。


表达式和语句中的空格
========================================

强制要求
----------

Avoid extraneous whitespace in the following situations:

- Immediately inside parentheses, brackets or braces. ::

      Yes: 
      		spam(ham[1], {eggs: 2})
      No:  
      		spam( ham[ 1 ], { eggs: 2 } )

- Immediately before a comma, semicolon, or colon::

      Yes: 
      		if x == 4: print x, y; x, y = y, x
      No:  
      		if x == 4 : print x , y ; x , y = y , x

- However, in a slice the colon acts like a binary operator, and
  should have equal amounts on either side (treating it as the
  operator with the lowest priority).  In an extended slice, both
  colons must have the same amount of spacing applied.  Exception:
  when a slice parameter is omitted, the space is omitted.

  Yes::

      ham[1:9], ham[1:9:3], ham[:9:3], ham[1::3], ham[1:9:]
      ham[lower:upper], ham[lower:upper:], ham[lower::step]
      ham[lower+offset : upper+offset]
      ham[: upper_fn(x) : step_fn(x)], ham[:: step_fn(x)]
      ham[lower + offset : upper + offset]

  No::

      ham[lower + offset:upper + offset]
      ham[1: 9], ham[1 :9], ham[1:9 :3]
      ham[lower : : upper]
      ham[ : upper]

- Immediately before the open parenthesis that starts the argument
  list of a function call::

      Yes: spam(1)
      No:  spam (1)

- Immediately before the open parenthesis that starts an indexing or
  slicing::

      Yes: dct['key'] = lst[index]
      No:  dct ['key'] = lst [index]

- More than one space around an assignment (or other) operator to
  align it with another.

  Yes::

      x = 1
      y = 2
      long_variable = 3

  No::

      x             = 1
      y             = 2
      long_variable = 3


Other Recommendations
---------------------

- Avoid trailing whitespace anywhere.  Because it's usually invisible,
  it can be confusing: e.g. a backslash followed by a space and a
  newline does not count as a line continuation marker.  Some editors
  don't preserve it and many projects (like CPython itself) have
  pre-commit hooks that reject it.

- Always surround these binary operators with a single space on either
  side: assignment (``=``), augmented assignment (``+=``, ``-=``
  etc.), comparisons (``==``, ``<``, ``>``, ``!=``, ``<>``, ``<=``,
  ``>=``, ``in``, ``not in``, ``is``, ``is not``), Booleans (``and``,
  ``or``, ``not``).

- If operators with different priorities are used, consider adding
  whitespace around the operators with the lowest priority(ies). Use
  your own judgment; however, never use more than one space, and
  always have the same amount of whitespace on both sides of a binary
  operator.

  Yes::

      i = i + 1
      submitted += 1
      x = x*2 - 1
      hypot2 = x*x + y*y
      c = (a+b) * (a-b)

  No::

      i=i+1
      submitted +=1
      x = x * 2 - 1
      hypot2 = x * x + y * y
      c = (a + b) * (a - b)

- Don't use spaces around the ``=`` sign when used to indicate a
  keyword argument or a default parameter value.

  Yes::

      def complex(real, imag=0.0):
          return magic(r=real, i=imag)

  No::

      def complex(real, imag = 0.0):
          return magic(r = real, i = imag)

- Function annotations should use the normal rules for colons and
  always have spaces around the ``->`` arrow if present.  (See
  `Function Annotations`_ below for more about function annotations.)

  Yes::

      def munge(input: AnyStr): ...
      def munge() -> AnyStr: ...

  No::

      def munge(input:AnyStr): ...
      def munge()->PosInt: ...

- When combining an argument annotation with a default value, use
  spaces around the ``=`` sign (but only for those arguments that have
  both an annotation and a default).

  Yes::

      def munge(sep: AnyStr = None): ...
      def munge(input: AnyStr, sep: AnyStr = None, limit=1000): ...

  No::

      def munge(input: AnyStr=None): ...
      def munge(input: AnyStr, limit = 1000): ...

- Compound statements (multiple statements on the same line) are
  generally discouraged.

  Yes::

      if foo == 'blah':
          do_blah_thing()
      do_one()
      do_two()
      do_three()

  Rather not::

      if foo == 'blah': do_blah_thing()
      do_one(); do_two(); do_three()

- While sometimes it's okay to put an if/for/while with a small body
  on the same line, never do this for multi-clause statements.  Also
  avoid folding such long lines!

  Rather not::

      if foo == 'blah': do_blah_thing()
      for x in lst: total += x
      while t < 10: t = delay()

  Definitely not::

      if foo == 'blah': do_blah_thing()
      else: do_non_blah_thing()

      try: something()
      finally: cleanup()

      do_one(); do_two(); do_three(long, argument,
                                   list, like, this)

      if foo == 'blah': one(); two(); three()

Comments
========

Comments that contradict the code are worse than no comments.  Always
make a priority of keeping the comments up-to-date when the code
changes!

Comments should be complete sentences.  If a comment is a phrase or
sentence, its first word should be capitalized, unless it is an
identifier that begins with a lower case letter (never alter the case
of identifiers!).

If a comment is short, the period at the end can be omitted.  Block
comments generally consist of one or more paragraphs built out of
complete sentences, and each sentence should end in a period.

You should use two spaces after a sentence-ending period.

When writing English, follow Strunk and White.

Python coders from non-English speaking countries: please write your
comments in English, unless you are 120% sure that the code will never
be read by people who don't speak your language.

Block Comments
--------------

Block comments generally apply to some (or all) code that follows
them, and are indented to the same level as that code.  Each line of a
block comment starts with a ``#`` and a single space (unless it is
indented text inside the comment).

Paragraphs inside a block comment are separated by a line containing a
single ``#``.

Inline Comments
---------------

Use inline comments sparingly.

An inline comment is a comment on the same line as a statement.
Inline comments should be separated by at least two spaces from the
statement.  They should start with a # and a single space.

Inline comments are unnecessary and in fact distracting if they state
the obvious.  Don't do this::

    x = x + 1                 # Increment x

But sometimes, this is useful::

    x = x + 1                 # Compensate for border

Documentation Strings
---------------------

Conventions for writing good documentation strings
(a.k.a. "docstrings") are immortalized in PEP 257.

- Write docstrings for all public modules, functions, classes, and
  methods.  Docstrings are not necessary for non-public methods, but
  you should have a comment that describes what the method does.  This
  comment should appear after the ``def`` line.

- PEP 257 describes good docstring conventions.  Note that most
  importantly, the ``"""`` that ends a multiline docstring should be
  on a line by itself, e.g.::

      """Return a foobang

      Optional plotz says to frobnicate the bizbaz first.
      """

- For one liner docstrings, please keep the closing ``"""`` on
  the same line.


Version Bookkeeping
===================

If you have to have Subversion, CVS, or RCS crud in your source file,
do it as follows. ::

    __version__ = "$Revision$"
    # $Source$

These lines should be included after the module's docstring, before
any other code, separated by a blank line above and below.


Naming Conventions
==================

The naming conventions of Python's library are a bit of a mess, so
we'll never get this completely consistent -- nevertheless, here are
the currently recommended naming standards.  New modules and packages
(including third party frameworks) should be written to these
standards, but where an existing library has a different style,
internal consistency is preferred.

Overriding Principle
--------------------

Names that are visible to the user as public parts of the API should
follow conventions that reflect usage rather than implementation.

Descriptive: Naming Styles
--------------------------

There are a lot of different naming styles.  It helps to be able to
recognize what naming style is being used, independently from what
they are used for.

The following naming styles are commonly distinguished:

- ``b`` (single lowercase letter)
- ``B`` (single uppercase letter)
- ``lowercase``
- ``lower_case_with_underscores``
- ``UPPERCASE``
- ``UPPER_CASE_WITH_UNDERSCORES``
- ``CapitalizedWords`` (or CapWords, or CamelCase -- so named because
  of the bumpy look of its letters [3]_).  This is also sometimes known
  as StudlyCaps.

  Note: When using abbreviations in CapWords, capitalize all the
  letters of the abbreviation.  Thus HTTPServerError is better than
  HttpServerError.
- ``mixedCase`` (differs from CapitalizedWords by initial lowercase
  character!)
- ``Capitalized_Words_With_Underscores`` (ugly!)

There's also the style of using a short unique prefix to group related
names together.  This is not used much in Python, but it is mentioned
for completeness.  For example, the ``os.stat()`` function returns a
tuple whose items traditionally have names like ``st_mode``,
``st_size``, ``st_mtime`` and so on.  (This is done to emphasize the
correspondence with the fields of the POSIX system call struct, which
helps programmers familiar with that.)

The X11 library uses a leading X for all its public functions.  In
Python, this style is generally deemed unnecessary because attribute
and method names are prefixed with an object, and function names are
prefixed with a module name.

In addition, the following special forms using leading or trailing
underscores are recognized (these can generally be combined with any
case convention):

- ``_single_leading_underscore``: weak "internal use" indicator.
  E.g. ``from M import *`` does not import objects whose name starts
  with an underscore.

- ``single_trailing_underscore_``: used by convention to avoid
  conflicts with Python keyword, e.g. ::

      Tkinter.Toplevel(master, class_='ClassName')

- ``__double_leading_underscore``: when naming a class attribute,
  invokes name mangling (inside class FooBar, ``__boo`` becomes
  ``_FooBar__boo``; see below).

- ``__double_leading_and_trailing_underscore__``: "magic" objects or
  attributes that live in user-controlled namespaces.
  E.g. ``__init__``, ``__import__`` or ``__file__``.  Never invent
  such names; only use them as documented.

Prescriptive: Naming Conventions
--------------------------------

Names to Avoid
~~~~~~~~~~~~~~

Never use the characters 'l' (lowercase letter el), 'O' (uppercase
letter oh), or 'I' (uppercase letter eye) as single character variable
names.

In some fonts, these characters are indistinguishable from the
numerals one and zero.  When tempted to use 'l', use 'L' instead.

Package and Module Names
~~~~~~~~~~~~~~~~~~~~~~~~

Modules should have short, all-lowercase names.  Underscores can be
used in the module name if it improves readability.  Python packages
should also have short, all-lowercase names, although the use of
underscores is discouraged.

When an extension module written in C or C++ has an accompanying
Python module that provides a higher level (e.g. more object oriented)
interface, the C/C++ module has a leading underscore
(e.g. ``_socket``).

Class Names
~~~~~~~~~~~

Class names should normally use the CapWords convention.

The naming convention for functions may be used instead in cases where
the interface is documented and used primarily as a callable.

Note that there is a separate convention for builtin names: most builtin
names are single words (or two words run together), with the CapWords
convention used only for exception names and builtin constants.

Exception Names
~~~~~~~~~~~~~~~

Because exceptions should be classes, the class naming convention
applies here.  However, you should use the suffix "Error" on your
exception names (if the exception actually is an error).

Global Variable Names
~~~~~~~~~~~~~~~~~~~~~

(Let's hope that these variables are meant for use inside one module
only.)  The conventions are about the same as those for functions.

Modules that are designed for use via ``from M import *`` should use
the ``__all__`` mechanism to prevent exporting globals, or use the
older convention of prefixing such globals with an underscore (which
you might want to do to indicate these globals are "module
non-public").

Function Names
~~~~~~~~~~~~~~

Function names should be lowercase, with words separated by
underscores as necessary to improve readability.

mixedCase is allowed only in contexts where that's already the
prevailing style (e.g. threading.py), to retain backwards
compatibility.

Function and method arguments
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Always use ``self`` for the first argument to instance methods.

Always use ``cls`` for the first argument to class methods.

If a function argument's name clashes with a reserved keyword, it is
generally better to append a single trailing underscore rather than
use an abbreviation or spelling corruption.  Thus ``class_`` is better
than ``clss``.  (Perhaps better is to avoid such clashes by using a
synonym.)

Method Names and Instance Variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Use the function naming rules: lowercase with words separated by
underscores as necessary to improve readability.

Use one leading underscore only for non-public methods and instance
variables.

To avoid name clashes with subclasses, use two leading underscores to
invoke Python's name mangling rules.

Python mangles these names with the class name: if class Foo has an
attribute named ``__a``, it cannot be accessed by ``Foo.__a``.  (An
insistent user could still gain access by calling ``Foo._Foo__a``.)
Generally, double leading underscores should be used only to avoid
name conflicts with attributes in classes designed to be subclassed.

Note: there is some controversy about the use of __names (see below).

Constants
~~~~~~~~~

Constants are usually defined on a module level and written in all
capital letters with underscores separating words.  Examples include
``MAX_OVERFLOW`` and ``TOTAL``.

Designing for inheritance
~~~~~~~~~~~~~~~~~~~~~~~~~

Always decide whether a class's methods and instance variables
(collectively: "attributes") should be public or non-public.  If in
doubt, choose non-public; it's easier to make it public later than to
make a public attribute non-public.

Public attributes are those that you expect unrelated clients of your
class to use, with your commitment to avoid backward incompatible
changes.  Non-public attributes are those that are not intended to be
used by third parties; you make no guarantees that non-public
attributes won't change or even be removed.

We don't use the term "private" here, since no attribute is really
private in Python (without a generally unnecessary amount of work).

Another category of attributes are those that are part of the
"subclass API" (often called "protected" in other languages).  Some
classes are designed to be inherited from, either to extend or modify
aspects of the class's behavior.  When designing such a class, take
care to make explicit decisions about which attributes are public,
which are part of the subclass API, and which are truly only to be
used by your base class.

With this in mind, here are the Pythonic guidelines:

- Public attributes should have no leading underscores.

- If your public attribute name collides with a reserved keyword,
  append a single trailing underscore to your attribute name.  This is
  preferable to an abbreviation or corrupted spelling.  (However,
  notwithstanding this rule, 'cls' is the preferred spelling for any
  variable or argument which is known to be a class, especially the
  first argument to a class method.)

  Note 1: See the argument name recommendation above for class methods.

- For simple public data attributes, it is best to expose just the
  attribute name, without complicated accessor/mutator methods.  Keep
  in mind that Python provides an easy path to future enhancement,
  should you find that a simple data attribute needs to grow
  functional behavior.  In that case, use properties to hide
  functional implementation behind simple data attribute access
  syntax.

  Note 1: Properties only work on new-style classes.

  Note 2: Try to keep the functional behavior side-effect free,
  although side-effects such as caching are generally fine.

  Note 3: Avoid using properties for computationally expensive
  operations; the attribute notation makes the caller believe that
  access is (relatively) cheap.

- If your class is intended to be subclassed, and you have attributes
  that you do not want subclasses to use, consider naming them with
  double leading underscores and no trailing underscores.  This
  invokes Python's name mangling algorithm, where the name of the
  class is mangled into the attribute name.  This helps avoid
  attribute name collisions should subclasses inadvertently contain
  attributes with the same name.

  Note 1: Note that only the simple class name is used in the mangled
  name, so if a subclass chooses both the same class name and attribute
  name, you can still get name collisions.

  Note 2: Name mangling can make certain uses, such as debugging and
  ``__getattr__()``, less convenient.  However the name mangling
  algorithm is well documented and easy to perform manually.

  Note 3: Not everyone likes name mangling.  Try to balance the
  need to avoid accidental name clashes with potential use by
  advanced callers.


Public and internal interfaces
------------------------------

Any backwards compatibility guarantees apply only to public interfaces.
Accordingly, it is important that users be able to clearly distinguish
between public and internal interfaces.

Documented interfaces are considered public, unless the documentation
explicitly declares them to be provisional or internal interfaces exempt
from the usual backwards compatibility guarantees. All undocumented
interfaces should be assumed to be internal.

To better support introspection, modules should explicitly declare the
names in their public API using the ``__all__`` attribute. Setting
``__all__`` to an empty list indicates that the module has no public API.

Even with ``__all__`` set appropriately, internal interfaces (packages,
modules, classes, functions, attributes or other names) should still be
prefixed with a single leading underscore.

An interface is also considered internal if any containing namespace
(package, module or class) is considered internal.

Imported names should always be considered an implementation detail.
Other modules must not rely on indirect access to such imported names
unless they are an explicitly documented part of the containing module's
API, such as ``os.path`` or a package's ``__init__`` module that exposes
functionality from submodules.


Programming Recommendations
===========================

- Code should be written in a way that does not disadvantage other
  implementations of Python (PyPy, Jython, IronPython, Cython, Psyco,
  and such).

  For example, do not rely on CPython's efficient implementation of
  in-place string concatenation for statements in the form ``a += b``
  or ``a = a + b``.  This optimization is fragile even in CPython (it
  only works for some types) and isn't present at all in implementations
  that don't use refcounting.  In performance sensitive parts of the
  library, the ``''.join()`` form should be used instead.  This will
  ensure that concatenation occurs in linear time across various
  implementations.

- Comparisons to singletons like None should always be done with
  ``is`` or ``is not``, never the equality operators.

  Also, beware of writing ``if x`` when you really mean ``if x is not
  None`` -- e.g. when testing whether a variable or argument that
  defaults to None was set to some other value.  The other value might
  have a type (such as a container) that could be false in a boolean
  context!

- Use ``is not`` operator rather than ``not ... is``.  While both
  expressions are functionally identical, the former is more readable
  and preferred.

  Yes::

      if foo is not None:

  No::

      if not foo is None:

- When implementing ordering operations with rich comparisons, it is
  best to implement all six operations (``__eq__``, ``__ne__``,
  ``__lt__``, ``__le__``, ``__gt__``, ``__ge__``) rather than relying
  on other code to only exercise a particular comparison.

  To minimize the effort involved, the ``functools.total_ordering()``
  decorator provides a tool to generate missing comparison methods.

  PEP 207 indicates that reflexivity rules *are* assumed by Python.
  Thus, the interpreter may swap ``y > x`` with ``x < y``, ``y >= x``
  with ``x <= y``, and may swap the arguments of ``x == y`` and ``x !=
  y``.  The ``sort()`` and ``min()`` operations are guaranteed to use
  the ``<`` operator and the ``max()`` function uses the ``>``
  operator.  However, it is best to implement all six operations so
  that confusion doesn't arise in other contexts.

- Always use a def statement instead of an assignment statement that binds
  a lambda expression directly to an identifier.

  Yes::

      def f(x): return 2*x

  No::

      f = lambda x: 2*x

  The first form means that the name of the resulting function object is
  specifically 'f' instead of the generic '<lambda>'. This is more
  useful for tracebacks and string representations in general. The use
  of the assignment statement eliminates the sole benefit a lambda
  expression can offer over an explicit def statement (i.e. that it can
  be embedded inside a larger expression)

- Derive exceptions from ``Exception`` rather than ``BaseException``.
  Direct inheritance from ``BaseException`` is reserved for exceptions
  where catching them is almost always the wrong thing to do.

  Design exception hierarchies based on the distinctions that code
  *catching* the exceptions is likely to need, rather than the locations
  where the exceptions are raised. Aim to answer the question
  "What went wrong?" programmatically, rather than only stating that
  "A problem occurred" (see PEP 3151 for an example of this lesson being
  learned for the builtin exception hierarchy)

  Class naming conventions apply here, although you should add the
  suffix "Error" to your exception classes if the exception is an
  error.  Non-error exceptions that are used for non-local flow control
  or other forms of signaling need no special suffix.

- Use exception chaining appropriately. In Python 3, "raise X from Y"
  should be used to indicate explicit replacement without losing the
  original traceback.

  When deliberately replacing an inner exception (using "raise X" in
  Python 2 or "raise X from None" in Python 3.3+), ensure that relevant
  details are transferred to the new exception (such as preserving the
  attribute name when converting KeyError to AttributeError, or
  embedding the text of the original exception in the new exception
  message).

- When raising an exception in Python 2, use ``raise ValueError('message')``
  instead of the older form ``raise ValueError, 'message'``.

  The latter form is not legal Python 3 syntax.

  The paren-using form also means that when the exception arguments are
  long or include string formatting, you don't need to use line
  continuation characters thanks to the containing parentheses.

- When catching exceptions, mention specific exceptions whenever
  possible instead of using a bare ``except:`` clause.

  For example, use::

      try:
          import platform_specific_module
      except ImportError:
          platform_specific_module = None

  A bare ``except:`` clause will catch SystemExit and
  KeyboardInterrupt exceptions, making it harder to interrupt a
  program with Control-C, and can disguise other problems.  If you
  want to catch all exceptions that signal program errors, use
  ``except Exception:`` (bare except is equivalent to ``except
  BaseException:``).

  A good rule of thumb is to limit use of bare 'except' clauses to two
  cases:

  1. If the exception handler will be printing out or logging the
     traceback; at least the user will be aware that an error has
     occurred.

  2. If the code needs to do some cleanup work, but then lets the
     exception propagate upwards with ``raise``.  ``try...finally``
     can be a better way to handle this case.

- When binding caught exceptions to a name, prefer the explicit name
  binding syntax added in Python 2.6::

      try:
          process_data()
      except Exception as exc:
          raise DataProcessingFailedError(str(exc))

  This is the only syntax supported in Python 3, and avoids the
  ambiguity problems associated with the older comma-based syntax.

- When catching operating system errors, prefer the explicit exception
  hierarchy introduced in Python 3.3 over introspection of ``errno``
  values.

- Additionally, for all try/except clauses, limit the ``try`` clause
  to the absolute minimum amount of code necessary.  Again, this
  avoids masking bugs.

  Yes::

      try:
          value = collection[key]
      except KeyError:
          return key_not_found(key)
      else:
          return handle_value(value)

  No::

      try:
          # Too broad!
          return handle_value(collection[key])
      except KeyError:
          # Will also catch KeyError raised by handle_value()
          return key_not_found(key)

- When a resource is local to a particular section of code, use a
  ``with`` statement to ensure it is cleaned up promptly and reliably
  after use. A try/finally statement is also acceptable.

- Context managers should be invoked through separate functions or methods
  whenever they do something other than acquire and release resources.
  For example:

  Yes::

               with conn.begin_transaction():
                   do_stuff_in_transaction(conn)

  No::

               with conn:
                   do_stuff_in_transaction(conn)

  The latter example doesn't provide any information to indicate that
  the __enter__ and __exit__ methods are doing something other than
  closing the connection after a transaction.  Being explicit is
  important in this case.

- Be consistent in return statements.  Either all return statements in
  a function should return an expression, or none of them should.  If
  any return statement returns an expression, any return statements
  where no value is returned should explicitly state this as ``return
  None``, and an explicit return statement should be present at the
  end of the function (if reachable).

  Yes::

      def foo(x):
          if x >= 0:
              return math.sqrt(x)
          else:
              return None

      def bar(x):
          if x < 0:
              return None
          return math.sqrt(x)

  No::

      def foo(x):
          if x >= 0:
              return math.sqrt(x)

      def bar(x):
          if x < 0:
              return
          return math.sqrt(x)

- Use string methods instead of the string module.

  String methods are always much faster and share the same API with
  unicode strings.  Override this rule if backward compatibility with
  Pythons older than 2.0 is required.

- Use ``''.startswith()`` and ``''.endswith()`` instead of string
  slicing to check for prefixes or suffixes.

  startswith() and endswith() are cleaner and less error prone.  For
  example::

      Yes: if foo.startswith('bar'):
      No:  if foo[:3] == 'bar':

- Object type comparisons should always use isinstance() instead of
  comparing types directly. ::

      Yes: if isinstance(obj, int):

      No:  if type(obj) is type(1):

  When checking if an object is a string, keep in mind that it might
  be a unicode string too!  In Python 2, str and unicode have a
  common base class, basestring, so you can do::

      if isinstance(obj, basestring):

  Note that in Python 3, ``unicode`` and ``basestring`` no longer exist
  (there is only ``str``) and a bytes object is no longer a kind of
  string (it is a sequence of integers instead)

- For sequences, (strings, lists, tuples), use the fact that empty
  sequences are false. ::

      Yes: if not seq:
           if seq:

      No: if len(seq)
          if not len(seq)

- Don't write string literals that rely on significant trailing
  whitespace.  Such trailing whitespace is visually indistinguishable
  and some editors (or more recently, reindent.py) will trim them.

- Don't compare boolean values to True or False using ``==``. ::

      Yes:   if greeting:
      No:    if greeting == True:
      Worse: if greeting is True:

Function Annotations
--------------------

With the acceptance of PEP 484, the style rules for function
annotations are changing.

- In order to be forward compatible, function annotations in Python 3
  code should preferably use PEP 484 syntax.  (There are some
  formatting recommendations for annotations in the previous section.)

- The experimentation with annotation styles that was recommended
  previously in this PEP is no longer encouraged.

- However, outside the stdlib, experiments within the rules of PEP 484
  are now encouraged.  For example, marking up a large third party
  library or application with PEP 484 style type annotations,
  reviewing how easy it was to add those annotations, and observing
  whether their presence increases code understandabilty.

- The Python standard library should be conservative in adopting such
  annotations, but their use is allowed for new code and for big
  refactorings.

- For code that wants to make a different use of function annotations
  it is recommended to put a comment of the form::

    # type: ignore

  near the top of the file; this tells type checker to ignore all
  annotations.  (More fine-grained ways of disabling complaints from
  type checkers can be found in PEP 484.)

- Like linters, type checkers are optional, separate tools.  Python
  interpreters by default should not issue any messages due to type
  checking and should not alter their behavior based on annotations.

- Users who don't want to use type checkers are free to ignore them.
  However, it is expected that users of third party library packages
  may want to run type checkers over those packages.  For this purpose
  PEP 484 recommends the use of stub files: .pyi files that are read
  by the type checker in preference of the corresponding .py files.
  Stub files can be distributed with a library, or separately (with
  the library author's permission) through the typeshed repo [5]_.

- For code that needs to be backwards compatible, function annotations
  can be added in the form of comments.  Basically, this Python 3 annotation::

    def embezzle(self, account: str, funds: int = 1000000, **fake_receipts: str) -> None:
        """Embezzle funds from account using fake receipts."""
        <code goes here>

  is equivalent to the following::

    def embezzle(self, account, funds=1000000, **fake_receipts):
        # type: (str, int, **str) -> None
        """Embezzle funds from account using fake receipts."""
        <code goes here>

  The mypy type checker [6]_ currently supports this syntax, and other
  type checkers are encouraged to adopt it.


.. rubric:: Footnotes

.. [#fn-hi] *Hanging indentation* is a type-setting style where all
   the lines in a paragraph are indented except the first line.  In
   the context of Python, the term is used to describe a style where
   the opening parenthesis of a parenthesized statement is the last
   non-whitespace character of the line, with subsequent lines being
   indented until the closing parenthesis.


References
==========

.. [1] PEP 7, Style Guide for C Code, van Rossum

.. [2] Barry's GNU Mailman style guide
       http://barry.warsaw.us/software/STYLEGUIDE.txt

.. [3] http://www.wikipedia.com/wiki/CamelCase

.. [4] PEP 8 modernisation, July 2013
   http://bugs.python.org/issue18472

.. [5] Typeshed repo
   https://github.com/python/typeshed

.. [6] mypy type checker
   http://mypy-lang.org
   https://github.com/JukkaL/mypy



Copyright
=========

This document has been placed in the public domain.



..
   Local Variables:
   mode: indented-text
   indent-tabs-mode: nil
   sentence-end-double-space: t
   fill-column: 70
   coding: utf-8
   End: