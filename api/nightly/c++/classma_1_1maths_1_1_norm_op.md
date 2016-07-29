[**](https://github.com/openma/openma-doc/edit/api/nightly/c++/classma_1_1maths_1_1_norm_op.md "Improve this documentation")
ma::maths::NormOp
=================

Compute the Euclidean norm for each row.

Detailed Description
--------------------

Member Function Documentation
-----------------------------

    ma::maths::NormOp::NormOp ( const  XprBase < Xpr > &  x ) [inline]

Constructor

------------------------------------------------------------------------

    auto ma::maths::NormOp::residuals ( ) const noexcept [inline]

Returns the residuals associated with this operation. The residuals is generated based on the input one.

------------------------------------------------------------------------

    Index ma::maths::NormOp::rows ( ) const noexcept [inline]

Returns the number of rows that shall have the result of this operation. Internaly, this method relies on the number of rows of the given expresion.

------------------------------------------------------------------------

    auto ma::maths::NormOp::values ( ) const noexcept [inline]

Returns a template expression corresponding to the calculation of this operation.

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


