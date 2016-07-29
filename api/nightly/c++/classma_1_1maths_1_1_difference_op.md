[**](https://github.com/openma/openma-doc/edit/api/nightly/c++/classma_1_1maths_1_1_difference_op.md "Improve this documentation")
ma::maths::DifferenceOp
=======================

Compute difference between given expressions.

Detailed Description
--------------------

Member Function Documentation
-----------------------------

    ma::maths::DifferenceOp::DifferenceOp ( const  XprBase < XprOne > &  x1 ,  const  XprBase < XprTwo > &  x2 ) [inline]

Constructor

------------------------------------------------------------------------

    auto ma::maths::DifferenceOp::residuals ( ) const noexcept [virtual][inline]

Returns the residuals associated with this operation. The residuals is generated based on the ones of each input.

------------------------------------------------------------------------

    Index ma::maths::DifferenceOp::rows ( ) const noexcept [inline]

Returns the number of rows that shall have the result of this operation. Internaly, this method relies on the number of rows of the first expresion.

------------------------------------------------------------------------

    auto ma::maths::DifferenceOp::values ( ) const noexcept [inline]

Returns the difference of the two expressions as a template expression.

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


