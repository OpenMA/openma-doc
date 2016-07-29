ma::maths::BlockOp
==================

Expression to extract a block of data.

Detailed Description
--------------------

Todo
Write a detailed description

Member Function Documentation
-----------------------------

    ma::maths::BlockOp::BlockOp ( Xpr  &  x ,  Index  index ) [inline]

Store a reference of the expression *xpr* and the *index* of the first column to extract.

Note: The number of columns (**) plus the ** must be lower or equal than the number of columns in the expression **. :

------------------------------------------------------------------------

    Index ma::maths::BlockOp::cols ( ) const noexcept [inline]

Returns the number of values' columns.

------------------------------------------------------------------------

    const  BlockOp  & ma::maths::BlockOp::derived ( ) const noexcept [inline]

Return a const reference of this object

------------------------------------------------------------------------

    BlockOp  & ma::maths::BlockOp::operator= ( const  BlockOp  &  other ) [inline]

Assignment operator from another block object. This will assign the content of *other* to the expression stored in this Block object.

------------------------------------------------------------------------

    BlockOp  & ma::maths::BlockOp::operator= ( const  BlockOp < U, V > &  other ) [inline]

Assignment operator from another block object. This will assign the content of *other* to the expression stored in this Block object.

------------------------------------------------------------------------

    auto ma::maths::BlockOp::residuals ( ) noexcept [inline]

Returns a block expression from the expression's residuals.

------------------------------------------------------------------------

    auto ma::maths::BlockOp::residuals ( ) const noexcept [inline]

Returns a block expression from the expression's residuals.

------------------------------------------------------------------------

    Index ma::maths::BlockOp::rows ( ) const noexcept [inline]

Returns the number of values' rows .

------------------------------------------------------------------------

    auto ma::maths::BlockOp::values ( ) noexcept [inline]

Returns a block expression from the expression's values.

------------------------------------------------------------------------

    auto ma::maths::BlockOp::values ( ) const noexcept [inline]

Returns a block expression from the expression's values.

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


