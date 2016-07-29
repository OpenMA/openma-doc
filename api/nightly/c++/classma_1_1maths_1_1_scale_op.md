ma::maths::ScaleOp
==================

Scale the data.

Detailed Description
--------------------

Member Function Documentation
-----------------------------

    auto ma::maths::ScaleOp::residuals ( ) const noexcept [inline]

Returns the residuals associated with this operation. The residuals is generated based on the input one.

------------------------------------------------------------------------

    Index ma::maths::ScaleOp::rows ( ) const noexcept [inline]

Returns the number of rows that shall have the result of this operation. Internaly, this method relies on the number of rows of the given expresion.

------------------------------------------------------------------------

    ma::maths::ScaleOp::ScaleOp ( double  scale ,  const  XprBase < Xpr > &  x ) [inline]

Constructor

------------------------------------------------------------------------

    auto ma::maths::ScaleOp::values ( ) const noexcept [inline]

Returns a template expression corresponding to the calculation of this operation.

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


