[**](https://github.com/openma/openma-doc/edit/api/nightly/c++/classma_1_1maths_1_1_unary_op.md "Improve this documentation")
ma::maths::UnaryOp
==================

Base class for unary operations.

Detailed Description
--------------------

Member Function Documentation
-----------------------------

    Index ma::maths::UnaryOp::cols ( ) const noexcept [inline]

Returns the number of columns that shall have the result of the binary operation. Internaly, this method relies on the template arguments of given expression.

------------------------------------------------------------------------

    const  Derived  & ma::maths::UnaryOp::derived ( ) const noexcept [inline]

Cast this object as a const reference of the Derived class.

------------------------------------------------------------------------

    Index ma::maths::UnaryOp::rows ( ) const noexcept [inline]

Returns the number of rows that shall have the result of the unary operation. Internaly, this method relies on the [rows()](#1a064a9cd1dbda700c686aac50efb92616) method of the Derived class.

------------------------------------------------------------------------

    ma::maths::UnaryOp::UnaryOp ( const  XprBase < Xpr > &  x ) [inline]

Store the expression *x* as plain object or reference depending of their type.

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


