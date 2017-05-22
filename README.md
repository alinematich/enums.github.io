<html>
    <head>
        <meta charset="UTF-8">
        <style>
            @font-face {
                font-family: nazanin;
                src: url('https://fonts.googleapis.com/css?family=BNazanin');
                direction: rtl;
            }
        </style>
    </head>
</html>

# نحوه ی استفاده از اینام در پایتون


### چگونه در پایتون می توانیم از اینام آماده استفاده کنیم

از پایتون 3.4 اینام به پایتون اضافه شد و شما با دستورات زیر میتوانید آن را نصب کنید:

```
enum34:   $ pip install enum34
aenum:    $ pip install aenum
```

و به صورت زیر آن ها را استفاده کنید:

```python
from enum import Enum  # for enum34, or the stdlib version
# from aenum import Enum  # for the aenum version
Animal = Enum('Animal', 'ant bee cat dog')
Animal.ant  # returns <Animal.ant: 1>
Animal['ant']  # returns <Animal.ant: 1> (string lookup)
Animal.ant.name  # returns 'ant' (inverse lookup)
```

و یا به این صورت:

```python
class Animal(Enum):
    ant = 1
    bee = 2
    cat = 3
    dog = 4
```
### اینام در ورژن های قبل

در ورژن های قدیمی تر پایتون نیز شما میتواند اینام را به صورت دستی پیاده سازی کنید و از آن استفاده کنید.
در زیر روش های پیاده سازی دستی اینام را که با استفاده از متاکلاس هستند با همدیگر مرور میکنیم.

ساده ترین روش:

```python
def enum(**enums):
    return type('Enum', (), enums)
```

روش استفاده:

```python
>>> Numbers = enum(ONE=1, TWO=2, THREE='three')
>>> Numbers.ONE
1
>>> Numbers.TWO
2
>>> Numbers.THREE
'three'
```

و با کمی پیشرفت دادن:

```python
def enum(*sequential, **named):
    x = range(len(sequential))
    enums = dict(zip(sequential, x), **named)
    return type('Enum', (), enums)
```

روش استفاده:

```python
>>> Numbers = enum('ZERO', 'ONE', 'TWO')
>>> Numbers.ZERO
0
>>> Numbers.ONE
1
```

و حتی میتوانیم کلید ها را از اعداد بدست اوریم:

```python
def enum(*sequential, **named):
    x = range(len(sequential))
    enums = dict(zip(sequential, x), **named)
    reverse = \
        dict((value, key) for key,
            value in enums.iteritems())
    enums['reverse_mapping'] = reverse
    return type('Enum', (), enums)
```

روش استفاده:

```python
>>> Numbers.reverse_mapping['three']
'THREE'
```
ورژن کمی پیشرفته ی آن را نیز میتوانید در زیر ببینید:

```python
def cmp(a,b):
   if a < b: return -1
   if b < a: return 1
   return 0


def Enum(*names):
   ##assert names, "Empty enums are not supported" # <- Don't like empty enums? Uncomment!

   class EnumClass(object):
      __slots__ = names
      def __iter__(self):        return iter(constants)
      def __len__(self):         return len(constants)
      def __getitem__(self, i):  return constants[i]
      def __repr__(self):        return 'Enum' + str(names)
      def __str__(self):         return 'enum ' + str(constants)

   class EnumValue(object):
      __slots__ = ('__value')
      def __init__(self, value): self.__value = value
      Value = property(lambda self: self.__value)
      EnumType = property(lambda self: EnumType)
      def __hash__(self):        return hash(self.__value)
      def __cmp__(self, other):
         # C fans might want to remove the following assertion
         # to make all enums comparable by ordinal value {;))
         assert self.EnumType is other.EnumType, "Only values from the same enum are comparable"
         return cmp(self.__value, other.__value)
      def __lt__(self, other):   return self.__cmp__(other) < 0
      def __eq__(self, other):   return self.__cmp__(other) == 0
      def __invert__(self):      return constants[maximum - self.__value]
      def __nonzero__(self):     return bool(self.__value)
      def __repr__(self):        return str(names[self.__value])

   maximum = len(names) - 1
   constants = [None] * len(names)
   for i, each in enumerate(names):
      val = EnumValue(i)
      setattr(EnumClass, each, val)
      constants[i] = val
   constants = tuple(constants)
   EnumType = EnumClass()
   return EnumType


if __name__ == '__main__':
   print( '\n*** Enum Demo ***')
   print( '--- Days of week ---')
   Days = Enum('Mo', 'Tu', 'We', 'Th', 'Fr', 'Sa', 'Su')
   print( Days)
   print( Days.Mo)
   print( Days.Fr)
   print( Days.Mo < Days.Fr)
   print( list(Days))
   for each in Days:
      print( 'Day:', each)
   print( '--- Yes/No ---')
   Confirmation = Enum('No', 'Yes')
   answer = Confirmation.No
   print( 'Your answer is not', ~answer)
```
