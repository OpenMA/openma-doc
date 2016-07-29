[**](https://github.com/openma/openma-doc/edit/api/nightly/c++/classma_1_1maths_1_1_binary_op.md "Improve this documentation")
ma::maths::BinaryOp
===================

Base class for binary operations.

Detailed Description
--------------------

Member Function Documentation
-----------------------------

    ma::maths::BinaryOp::BinaryOp ( const  XprBase < XprOne > &  x1 ,  const  XprBase < XprTwo > &  x2 ) [inline]

Store the expressions *x1* and *x2* as plain objects or references depending of their type.

------------------------------------------------------------------------

    Index ma::maths::BinaryOp::cols ( ) const noexcept [inline]

Returns the number of columns that shall have the result of the binary operation. Internaly, this method relies on the template arguments of given expressions.

------------------------------------------------------------------------

    const  Derived  & ma::maths::BinaryOp::derived ( ) const noexcept [inline]

Cast this object as a const reference of the Derived class.

------------------------------------------------------------------------

    Index ma::maths::BinaryOp::rows ( ) const noexcept [inline]

Returns the number of rows that shall have the result of the binary operation. Internaly, this method relies on the [rows()](#1a8352327ad515f5ff8c687614b46092a9) method of the Derived class.

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


