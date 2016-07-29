ma::maths::InverseOp
====================

Compute the inverse.

Detailed Description
--------------------

Note: this operator would be used with [](classma_1_1maths_1_1_pose.html) object or [](classma_1_1maths_1_1_array.html) with 12 columns.

Member Function Documentation
-----------------------------

    ma::maths::InverseOp::InverseOp ( const  XprBase < Xpr > &  x ) [inline]

Constructor

------------------------------------------------------------------------

    auto ma::maths::InverseOp::residuals ( ) const noexcept [inline]

Returns the residuals associated with this operation. The residuals is generated based on the input one.

------------------------------------------------------------------------

    Index ma::maths::InverseOp::rows ( ) const noexcept [inline]

Returns the number of rows that shall have the result of this operation. Internaly, this method relies on the number of rows of the given expresion.

------------------------------------------------------------------------

    auto ma::maths::InverseOp::values ( ) const noexcept [inline]

Returns a template expression corresponding to the calculation of this operation.

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


