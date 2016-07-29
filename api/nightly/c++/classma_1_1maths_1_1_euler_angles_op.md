[**](https://github.com/openma/openma-doc/edit/api/nightly/c++/classma_1_1maths_1_1_euler_angles_op.md "Improve this documentation")
ma::maths::EulerAnglesOp
========================

Compute euler angles.

Detailed Description
--------------------

Note: This operator would be used with an array with at least 9 columns representing an orientation. It can be for example a [](classma_1_1maths_1_1_pose.html) object.

Member Function Documentation
-----------------------------

    ma::maths::EulerAnglesOp::EulerAnglesOp ( const  XprBase < Xpr > &  x ,  Index  a0 ,  Index  a1 ,  Index  a2 ) [inline]

Constructor. The Index *a0*, *a1*, *a2* reprensent the sequence order.

-   The rotation along the axis X will be given with the value 0.
-   The rotation along the axis Y will be given with the value 1.
-   The rotation along the axis Z will be given with the value 2.

        auto eao1 = EulerAnglesOp(pose,0,1,2); // Extract eurler angles using axes X, Y', and Z".
        auto eao2 = EulerAnglesOp(pose,2,0,1); // Extract eurler angles using axes Z, X', and Y".

------------------------------------------------------------------------

    auto ma::maths::EulerAnglesOp::residuals ( ) const noexcept [inline]

Returns the residuals associated with this operation. The residuals is generated based on the input one.

------------------------------------------------------------------------

    Index ma::maths::EulerAnglesOp::rows ( ) const noexcept [inline]

Returns the number of rows that shall have the result of this operation. Internaly, this method relies on the number of rows of the given expresion.

------------------------------------------------------------------------

    auto ma::maths::EulerAnglesOp::values ( ) const noexcept [inline]

Returns a template expression corresponding to the calculation of this operation.

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


