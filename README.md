Python Algebraic Data Types
===========================

This project aims to implement algebraic data types in Python using the
[Hy][hy] language. In effect, we would like to input code such as this

```lisp
(data TypeName (TypeConstructor (name str)) :deriving (Show, Eq))
```

and get something like the following out using macros.

```python
class TypeName(object):
    def __init__(self, name):
        if not isinstance(name, str):
            raise ValueError("{} must be of type str".format(name))

        self._name = name

    @property
    def name(self):
        return self._name

    ## __repr__ derived automatically (from :deriving Show)
    def __repr__(self):
        return "TypeName({})".format(self._name)

    ## __eq__ derived automatically (from :deriving Eq)
    def __eq__(self, other):
        return self._name == other._name

def TypeConstructor(name):
    return TypeName(name)
```

The eventual goal would be to support

- product types
- sum types
- [parametric polymorphism](https://en.wikipedia.org/wiki/Parametric_polymorphism)
- Automatic deriving, ideally for the following cases: Show/Read, Eq, Ord,
  Enum, Bounded, Functor, and Foldable.

<!--
      Links
             -->
[hy]: http://docs.hylang.org/en/latest/
