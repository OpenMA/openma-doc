ma::maths::TransformOp
======================

Compute the transformation of two expressions.

Detailed Description
--------------------

Member Function Documentation
-----------------------------

    auto ma::maths::TransformOp::residuals ( ) const noexcept [virtual][inline]

Returns the residuals associated with this operation. The residuals is generated based on the ones of each input.

------------------------------------------------------------------------

    Index ma::maths::TransformOp::rows ( ) const noexcept [inline]

Returns the number of rows that shall have the result of this operation. Internaly, this method relies on the number of rows of the first expresion.

------------------------------------------------------------------------

    ma::maths::TransformOp::TransformOp ( const  XprBase < XprOne > &  x1 ,  const  XprBase < XprTwo > &  x2 ) [inline]

Constructor

------------------------------------------------------------------------

    auto ma::maths::TransformOp::values ( ) const noexcept [inline]

Returns the transformation of the two expressions as a template expression.

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


