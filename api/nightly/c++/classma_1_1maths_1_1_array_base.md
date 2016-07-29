[**](https://github.com/openma/openma-doc/edit/api/nightly/c++/classma_1_1maths_1_1_array_base.md "Improve this documentation")
ma::maths::ArrayBase
====================

Base class for data storage.

Detailed Description
--------------------

Todo
Write a detailed description

Member Type Documentation
-------------------------

    ma::maths::ArrayBase::Index

------------------------------------------------------------------------

    ma::maths::ArrayBase::Residuals

------------------------------------------------------------------------

    ma::maths::ArrayBase::Values

------------------------------------------------------------------------

Member Function Documentation
-----------------------------

    ma::maths::ArrayBase::ArrayBase ( const  ArrayBase  &  other )

Default copy constructor

------------------------------------------------------------------------

    ma::maths::ArrayBase::ArrayBase ( const  Values  &  values ,  const  Residuals  &  residuals ) [inline]

Constructor from data

------------------------------------------------------------------------

    Index ma::maths::ArrayBase::cols ( ) const noexcept [inline]

Returns the number of values' columns.

------------------------------------------------------------------------

    Derived  & ma::maths::ArrayBase::derived ( ) noexcept [inline]

Cast the object to a *Derived* type reference.

------------------------------------------------------------------------

    const  Derived  & ma::maths::ArrayBase::derived ( ) const noexcept [inline]

Cast the object to a *Derived* type consts reference.

------------------------------------------------------------------------

    bool ma::maths::ArrayBase::isOccluded ( ) const noexcept [inline]

Convient method to determine if some value were not correctly reconstructed (i.e. occluded). Internaly, the associated residual is analyzed to find if some of them are negative.

------------------------------------------------------------------------

    bool ma::maths::ArrayBase::isValid ( ) const noexcept [inline]

Convient method to determine if the content of the object is valid. A valid object has at least 1 row. An object with no row is invalid.

------------------------------------------------------------------------

    BlockOp <  ArrayBase < Derived >, 3 > ma::maths::ArrayBase::o ( ) noexcept [inline]

Convenient method to extract the columns \#10-12 of the values (could be usefull with [Pose](classma_1_1maths_1_1_pose.html) object).

Warning: This method does not check the number of existing columns. Unknown behaviour will happen if the number of columns is less than the one requested. :

------------------------------------------------------------------------

    const  BlockOp < const  ArrayBase < Derived >, 3 > ma::maths::ArrayBase::o ( ) const noexcept [inline]

Convenient method to extract the columns \#10-12 of the values (could be usefull with [Pose](classma_1_1maths_1_1_pose.html) object).

Warning: This method does not check the number of existing columns. Unknown behaviour will happen if the number of columns is less than the one requested. :

------------------------------------------------------------------------

    Residuals  & ma::maths::ArrayBase::residuals ( ) noexcept [inline]

Returns a reference for the residuals associated with the stored values. The number of rows is equal to the number of values' rows. The number of columns is always 1.

------------------------------------------------------------------------

    const  Residuals  & ma::maths::ArrayBase::residuals ( ) const noexcept [inline]

Returns a const reference for the residuals associated with the stored values. The number of rows is equal to the number of values' rows. The number of columns is always 1.

------------------------------------------------------------------------

    Index ma::maths::ArrayBase::rows ( ) const noexcept [inline]

Returns the number of values' rows .

------------------------------------------------------------------------

    BlockOp <  ArrayBase < Derived >, 3 > ma::maths::ArrayBase::u ( ) noexcept [inline]

Convenient method to extract the columns \#1-3 of the values (could be usefull with [Pose](classma_1_1maths_1_1_pose.html) object).

Warning: This method does not check the number of existing columns. Unknown behaviour will happen if the number of columns is less than the one requested. :

------------------------------------------------------------------------

    const  BlockOp < const  ArrayBase < Derived >, 3 > ma::maths::ArrayBase::u ( ) const noexcept [inline]

Convenient method to extract the columns \#1-3 of the values (could be usefull with [Pose](classma_1_1maths_1_1_pose.html) object).

Warning: This method does not check the number of existing columns. Unknown behaviour will happen if the number of columns is less than the one requested. :

------------------------------------------------------------------------

    BlockOp <  ArrayBase < Derived >, 3 > ma::maths::ArrayBase::v ( ) noexcept [inline]

Convenient method to extract the columns \#4-6 of the values (could be usefull with [Pose](classma_1_1maths_1_1_pose.html) object).

Warning: This method does not check the number of existing columns. Unknown behaviour will happen if the number of columns is less than the one requested. :

------------------------------------------------------------------------

    const  BlockOp < const  ArrayBase < Derived >, 3 > ma::maths::ArrayBase::v ( ) const noexcept [inline]

Convenient method to extract the columns \#4-6 of the values (could be usefull with [Pose](classma_1_1maths_1_1_pose.html) object).

Warning: This method does not check the number of existing columns. Unknown behaviour will happen if the number of columns is less than the one requested. :

------------------------------------------------------------------------

    Values  & ma::maths::ArrayBase::values ( ) noexcept [inline]

Returns a reference for the values stored in this object.

------------------------------------------------------------------------

    const  Values  & ma::maths::ArrayBase::values ( ) const noexcept [inline]

Returns a const reference for the values stored in this object.

------------------------------------------------------------------------

    BlockOp <  ArrayBase < Derived >, 3 > ma::maths::ArrayBase::w ( ) noexcept [inline]

Convenient method to extract the columns \#7-9 of the values (could be usefull with [Pose](classma_1_1maths_1_1_pose.html) object).

Warning: This method does not check the number of existing columns. Unknown behaviour will happen if the number of columns is less than the one requested. :

------------------------------------------------------------------------

    const  BlockOp < const  ArrayBase < Derived >, 3 > ma::maths::ArrayBase::w ( ) const noexcept [inline]

Convenient method to extract the columns \#7-9 of the values (could be usefull with [Pose](classma_1_1maths_1_1_pose.html) object).

Warning: This method does not check the number of existing columns. Unknown behaviour will happen if the number of columns is less than the one requested. :

------------------------------------------------------------------------

    BlockOp <  ArrayBase < Derived >, 1 > ma::maths::ArrayBase::x ( ) noexcept [inline]

Convenient method to extract the first column of the values.

Warning: This method does not check the number of existing columns. Unknown behaviour will happen if the number of columns is less than the one(s) requested. :

------------------------------------------------------------------------

    const  BlockOp < const  ArrayBase < Derived >, 1 > ma::maths::ArrayBase::x ( ) const noexcept [inline]

Convenient method to extract the first column of the values.

Warning: This method does not check the number of existing columns. Unknown behaviour will happen if the number of columns is less than the one(s) requested. :

------------------------------------------------------------------------

    BlockOp <  ArrayBase < Derived >, 1 > ma::maths::ArrayBase::y ( ) noexcept [inline]

Convenient method to extract the second column of the values.

Warning: This method does not check the number of existing columns. Unknown behaviour will happen if the number of columns is less than the one(s) requested. :

------------------------------------------------------------------------

    const  BlockOp < const  ArrayBase < Derived >, 1 > ma::maths::ArrayBase::y ( ) const noexcept [inline]

Convenient method to extract the second column of the values.

Warning: This method does not check the number of existing columns. Unknown behaviour will happen if the number of columns is less than the one(s) requested. :

------------------------------------------------------------------------

    BlockOp <  ArrayBase < Derived >, 1 > ma::maths::ArrayBase::z ( ) noexcept [inline]

Convenient method to extract the third column of the values.

Warning: This method does not check the number of existing columns. Unknown behaviour will happen if the number of columns is less than the one(s) requested. :

------------------------------------------------------------------------

    const  BlockOp < const  ArrayBase < Derived >, 1 > ma::maths::ArrayBase::z ( ) const noexcept [inline]

Convenient method to extract the third column of the values.

Warning: This method does not check the number of existing columns. Unknown behaviour will happen if the number of columns is less than the one(s) requested. :

------------------------------------------------------------------------

Related Non-Members Documentation
---------------------------------

    const  ScaleOp < Xpr > ma::maths::ArrayBase::operator* ( double  x1 ,  const  XprBase < Xpr > &  x2 )

Convenient multiplication operator to scale the template expressions *x2* by the scalara*x1*.

------------------------------------------------------------------------

    const  ScaleOp < Xpr > ma::maths::ArrayBase::operator* ( const  XprBase < Xpr > &  x1 ,  double  x2 )

Convenient multiplication operator to scale the template expressions *x1* by *x2*.

------------------------------------------------------------------------

    const  SumOp < XprOne, XprTwo > ma::maths::ArrayBase::operator+ ( const  XprBase < XprOne > &  x1 ,  const  XprBase < XprTwo > &  x2 ) noexcept

Convenient okys operator to compute the sum between two template expressions

------------------------------------------------------------------------

    const  DifferenceOp < XprOne, XprTwo > ma::maths::ArrayBase::operator- ( const  XprBase < XprOne > &  x1 ,  const  XprBase < XprTwo > &  x2 ) noexcept

Convenient minus operator to compute the difference between two template expressions

------------------------------------------------------------------------

    const  ScaleOp < Xpr > ma::maths::ArrayBase::operator/ ( const  XprBase < Xpr > &  x1 ,  double  x2 )

Convenient division operator to scale the template expressions *x1* by *x2*.

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


