[**](https://github.com/openma/openma-doc/edit/api/nightly/c++/classma_1_1maths_1_1_pose.md "Improve this documentation")
ma::maths::Pose
===============

Define an [Array](classma_1_1maths_1_1_array.html) with 12 columns to represent a 3D orientation and a 3D position along a sequence. Convenient class with dedicated methods to construct/access poses.

Member Type Documentation
-------------------------

    ma::maths::Pose::Orientations

------------------------------------------------------------------------

    ma::maths::Pose::Positions

------------------------------------------------------------------------

Member Function Documentation
-----------------------------

    const Eigen::Block< const  Array < 12 >:: Values  > ma::maths::Pose::orientations ( ) const noexcept [inline]

Returns the nine first columns to access to the 3D orientation part.

------------------------------------------------------------------------

    ma::maths::Pose::Pose ( ) [inline]

Default constructor

------------------------------------------------------------------------

    ma::maths::Pose::Pose ( Index  rows ) [inline]

Initialize a motion with a number of samples (lines) equals to *rows*

------------------------------------------------------------------------

    ma::maths::Pose::Pose ( const  XprBase < U > &  u ,  const  XprBase < V > &  v ,  const  XprBase < W > &  w ,  const  XprBase < O > &  o ) [inline]

Constructor from vectors (u,v,w,o). Internally, these vectors are joined into an array with 12 components. They represents a compact affine transformation. The storage order is the following u\_x, u\_y, u\_z, v\_x, v\_x, v\_y, v\_z, w\_x, w\_y, w\_z, o\_x, o\_y, o\_z.

------------------------------------------------------------------------

    ma::maths::Pose::Pose ( const  XprBase < U > &  other )

Convenient constructor to store the result of an expression.

------------------------------------------------------------------------

    const Eigen::Block< const  Array < 12 >:: Values  > ma::maths::Pose::positions ( ) const noexcept [inline]

Returns the three last columns to access to the 3D orientation part.

------------------------------------------------------------------------

Related Non-Members Documentation
---------------------------------

    Map <  Pose  > ma::maths::Pose::to_pose ( TimeSequence  *  ts ) [inline]

Specialized extraction method where the result is a Map object (as well as the input - no possible offset) and the type must be set to [TimeSequence::Pose](classma_1_1_time_sequence.html#1a8e5ba2425b030c3b7726203c1efbdac2ae06cf3a79f0abb9466209d281b7a5de5).

------------------------------------------------------------------------

    Map < const  Pose  > ma::maths::Pose::to_pose ( const  TimeSequence  *  ts ) [inline]

Specialized extraction method where the result is a Map object (as well as the input - no possible offset) and the type must be set to [TimeSequence::Pose](classma_1_1_time_sequence.html#1a8e5ba2425b030c3b7726203c1efbdac2ae06cf3a79f0abb9466209d281b7a5de5).

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


