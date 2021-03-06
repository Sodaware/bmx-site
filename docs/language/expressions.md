---
id: expressions
title: Expressions
sidebar_label: Expressions
---

## Operators

BlitzMax supports the following operators. Operators are grouped into levels of precedence,
starting with the highest precedence operators:

| Operator  | Syntax  |
|---|---|
| Sub expression  | ( Expression )  |
| New object  | [New] Typename  |
| Literal  | Value  |
| Identifier  | Value  |
| Self object  | [Self]  |
| Super object  | [Super]  |
| Null value  | [Null]  |
| Pi  | [Pi]  |
| True  | [True]  |
| False  | [False]  |
| Member  | Expression . Identifier  |
| Index  | Expression [ IndexExpressions ]  |
| Call  | Expression ( Parameters ) |
| Posate  | `+` Expression  |
| Negate  | `-` Expression  |
| Bitwise complement  | `~` Expression  |
| Boolean not  | [Not] Expression  |
| Value byte size  | [SizeOf] Expression  |
| Variable address  | [Varptr] Variable  |
| Convert type expression  | Type Expression  |
| Power  | Expression `^` Expression  |
| Multiply  | Expression `*` Expression  |
| Divide  | Expression `/` Expression  |
| Remainder  | Expression [Mod] Expression  |
| Bitwise shift left  | Expression [Shl] Expression  |
| Bitwise shift right  | Expression [Shr] Expression  |
| Arithmetic shift right  | Expression [Sar] Expression  |
| Add  | Expression `+` Expression  |
| Subtract  | Expression `-` Expression  |
| Bitwise and  | Expression `&` Expression  |
| Bitwise or  | Expression <code>&#124;</code>  Expression  |
| Bitwise exclusive or  | Expression `~` Expression  |
| Equal  | Expression = Expression  |
| Not equal  | Expression `<>` Expression  |
| Less than  | Expression `<` Expression  |
| Greater than  | Expression `>` Expression  |
| Less than or equal  | Expression `<=` Expression  |
| Greater than or equal  | Expression `>=` Expression  |
| Conditional and  | Expression [And] Expression  |
| Conditional or  | Expression [Or] Expression  |

In addition, the following built in functions are also supported:

| Function  | Syntax  |
|---|---|
| Character code  | [Asc] ( Expression )  |
| Character  | [Chr] ( Expression )  |
| Value length  | [Len] ( Expression )  |

[Null] returns 0, an empty string, an empty array, the null object or a pointer to 0 depending on context.

[True] and [False] are integer constants with the values 1 and 0, respectively.

The index operator can be used on either arrays or strings. If used on an array,
the element at the specified index is returned. If used on a string, the character code
of the character at the specified index is returned.

The [Not] operator `inverts` the logic of a boolean expression. If the expression
evaluates to true, [Not] returns false and vice versa.

[Asc] returns the character value of the first character of a string, or -1 if the length of the string is 0.

[Chr] constructs a 1 character string with the specified character value.

[Len] can be used with either a string or array. When used with a string, [Len]
returns the number of characters in the string. When used with an array, [Len] returns
the number of elements in the array. In the case of multidimensional arrays, [Len]
returns the total number of elements.

## Boolean expressions

It is frequently necessary to consider an expression as `true` or `false`, for
example, for use with an [If] statement.

The rules for determining whether an expression is true or false are:

| Expression Type  | Truth condition  |
|---|---|
| Numeric  | True if value is not equal to 0  |
| Object  | True if object is not equal to [Null]  |
| String  | True if length is not equal to 0  |
| Array  | True if length is not equal to 0  |


[Null]: ../../api/brl/brl.blitz/#null
[True]: ../../api/brl/brl.blitz/#true
[False]: ../../api/brl/brl.blitz/#false
[Not]: ../../api/brl/brl.blitz/#not
[Asc]: ../../api/brl/brl.blitz/#asc
[Chr]: ../../api/brl/brl.blitz/#chr
[Len]: ../../api/brl/brl.blitz/#len
[If]: ../../api/brl/brl.blitz/#if
[Or]: ../../api/brl/brl.blitz/#or
[And]: ../../api/brl/brl.blitz/#and
[New]: ../../api/brl/brl.blitz/#new
[Self]: ../../api/brl/brl.blitz/#self
[Super]: ../../api/brl/brl.blitz/#super
[Pi]: ../../api/brl/brl.blitz/#pi
[SizeOf]: ../../api/brl/brl.blitz/#sizeof
[Varptr]: ../../api/brl/brl.blitz/#varptr
[Mod]: ../../api/brl/brl.blitz/#mod
[Shl]: ../../api/brl/brl.blitz/#shl
[Shr]: ../../api/brl/brl.blitz/#shr
[Sar]: ../../api/brl/brl.blitz/#sar
