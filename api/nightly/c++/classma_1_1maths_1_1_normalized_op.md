ma::maths::NormalizedOp
=======================

Normalize the data.

Detailed Description
--------------------

Member Function Documentation
-----------------------------

    ma::maths::NormalizedOp::NormalizedOp ( const  XprBase < Xpr > &  x ) [inline]

Constructor

------------------------------------------------------------------------

    auto ma::maths::NormalizedOp::residuals ( ) const noexcept [inline]

Returns the residuals associated with this operation. The residuals is generated based on the input one.

------------------------------------------------------------------------

    Index ma::maths::NormalizedOp::rows ( ) const noexcept [inline]

Returns the number of rows that shall have the result of this operation. Internaly, this method relies on the number of rows of the given expresion.

------------------------------------------------------------------------

    auto ma::maths::NormalizedOp::values ( ) const noexcept [inline]

Returns a template expression corresponding to the calculation of this operation.

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


