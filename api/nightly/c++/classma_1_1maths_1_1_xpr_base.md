ma::maths::XprBase
==================

Base class for all template expressions used in the maths module.

Detailed Description
--------------------

Todo
Write a detailed description ingroup openma\_maths

Member Type Documentation
-------------------------

    ma::maths::XprBase::DerivedType

------------------------------------------------------------------------

    ma::maths::XprBase::Index

------------------------------------------------------------------------

Member Function Documentation
-----------------------------

    BlockOp < Derived, Cols > ma::maths::XprBase::block ( Index  index ) noexcept [inline]

Returns a block of the current expression with *Cols* columns and starting at the column *index* (0-based).

------------------------------------------------------------------------

    const  BlockOp < const Derived, Cols > ma::maths::XprBase::block ( Index  index ) const noexcept [inline]

Returns a const block of the current expression with *Cols* columns and starting at the column *index* (0-based).

------------------------------------------------------------------------

    const  CrossOp < Derived, U > ma::maths::XprBase::cross ( const  XprBase < U > &  other ) const noexcept [inline]

Returns an object representing a cross product operator between *this* object and the *other* object.

------------------------------------------------------------------------

    const  EulerAnglesOp < Derived > ma::maths::XprBase::eulerAngles ( Index  a0 ,  Index  a1 ,  Index  a2 ) const noexcept [inline]

Returns an object representing an euler angles operation using the given order *a0*, *a1*, *a2* for the sequence order.

------------------------------------------------------------------------

    const  InverseOp < Derived > ma::maths::XprBase::inverse ( ) const noexcept [inline]

Returns an object representing this object with all this rows inversed.

------------------------------------------------------------------------

    const  MeanOp < Derived > ma::maths::XprBase::mean ( ) const noexcept [inline]

Returns an object representing an average of each row of this object.

------------------------------------------------------------------------

    const  NormOp < Derived > ma::maths::XprBase::norm ( ) const noexcept [inline]

Returns an object representing the Euclidian norm of each row of this object.

------------------------------------------------------------------------

    const  NormalizedOp < Derived > ma::maths::XprBase::normalized ( ) const noexcept [inline]

Returns an object representing this object with all this rows normalized.

------------------------------------------------------------------------

    ma::maths::XprBase::operator const Derived & ( ) const noexcept [inline]

Returns a casted version of *this* object as a const reference to a *Derived* type.

------------------------------------------------------------------------

    ma::maths::XprBase::operator Derived & ( ) noexcept [inline]

Returns a casted version of *this* object as a reference to a *Derived* type.

------------------------------------------------------------------------

    ma::maths::XprBase::operator double ( ) const noexcept [inline]

Convenient method to extract the first value if valid (i.e the associated residial is null or positive), otherwise returns 0.0.

Warning: No assertion is realized to know if the expression is empty or not. :

------------------------------------------------------------------------

    const  ReplicateOp < Derived > ma::maths::XprBase::replicate ( Index  rows ) const noexcept [inline]

Returns an object representing a replicated version of this *rows* time.

------------------------------------------------------------------------

    const  TransformOp < Derived, U > ma::maths::XprBase::transform ( const  XprBase < U > &  other ) const noexcept [inline]

Returns an object representing a transformation between *this* object and the *other* object.

------------------------------------------------------------------------

Member Data Documentation
-------------------------

    ma::maths::XprBase::ColsAtCompileTime[static]

------------------------------------------------------------------------

    ma::maths::XprBase::Processing[static]

Note: This information is only for internal purpose. :

------------------------------------------------------------------------

Related Non-Members Documentation
---------------------------------

    auto ma::maths::XprBase::generate_residuals ( const  U  &  condition ) [inline]

Returns a column vector representing the result of the given *condition*. For elements where the condition is respected, the value is set to 0. Otherwise the value is set to -1.0. This represent valid (&gt;= 0) and invalid (&lt; 0) reconstructed data.

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


