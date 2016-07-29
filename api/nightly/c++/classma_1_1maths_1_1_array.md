ma::maths::Array
================

Class to store reconstructed data.

Detailed Description
--------------------

This class is usefull for any reconstructed data that can be stored as an array with any number of columns. The values can be access by the method [values()](#base_1aa9a2529ddb19f6932207dd8280bc9112) and the reconstruction residuals with the method [residuals()](#base_1ab00830eccc9c76283e192d2238584f39). In general, this is not necessary to pass by these methods but directly use the operators and methods to do computations. Indeed, internally, this class use template expression to manage invalid data (negative residuals). There is no need to loop through samples to check if it is valid or not.

Todo
Add example related to the automatic management of the residuals.

Member Type Documentation
-------------------------

    ma::maths::Array::Index

------------------------------------------------------------------------

    ma::maths::Array::Residuals

------------------------------------------------------------------------

    ma::maths::Array::Values

------------------------------------------------------------------------

Member Function Documentation
-----------------------------

    ma::maths::Array::Array ( ) [inline]

Default constructor. Create an empty array (method isValue() returns false).

------------------------------------------------------------------------

    ma::maths::Array::Array ( Index  rows ) [inline]

Create an array with a fixed number of *Cols* columns and a dynamic number of *rows*.

------------------------------------------------------------------------

    ma::maths::Array::Array ( const  Values  &  values ) [inline]

Create an array based on the given *values*. All the samples are set to valid (residuals set to 0).

Note: The number of colums for the ** must be the same than the number of **. :

------------------------------------------------------------------------

    ma::maths::Array::Array ( const  Values  &  values ,  const  Residuals  &  residuals ) [inline]

Create a constructor based on the given *values* and residuals.

Note: The number of row for the ** and teh ** must be the same. :

------------------------------------------------------------------------

    ma::maths::Array::Array ( const  XprBase < U > &  other ) [inline]

Constructor from an [XprBase](classma_1_1maths_1_1_xpr_base.html) object (generaly used to store the result of a computation).

    // a and b are other Array object.
    auto c = a + b; // The assignment of c is realized with this constructor. 

------------------------------------------------------------------------

    Array < Cols > & ma::maths::Array::operator= ( const  XprBase < U > &  other ) [inline]

Assignment operator from an [XprBase](classma_1_1maths_1_1_xpr_base.html) object.

------------------------------------------------------------------------

Related Non-Members Documentation
---------------------------------

    using Position =  Vector

Define an [Array](classma_1_1maths_1_1_array.html) with three columns. This could represent a 3D trajectory along a sequence.

------------------------------------------------------------------------

    using Scalar =  Array < 1 >

Define an [Array](classma_1_1maths_1_1_array.html) with one column. This could represent a scalar value along a sequence.

------------------------------------------------------------------------

    using Vector =  Array < 3 >

Define an [Array](classma_1_1maths_1_1_array.html) with three columns. This could represent a 3D vector along a sequence.

------------------------------------------------------------------------

    Map <  Array < N > > ma::maths::Array::to_array ( TimeSequence  *  ts ,  int  offset  = 0 ,  int  type  = -1 ) [inline]

Extract from a [TimeSequence](classma_1_1_time_sequence.html) *ts* a Map&gt; where the number of columns of the resulting array is used as the number of components to extract. It is possible to specify a possible *offset* to shift the data to extract. The use of *type* will verify if the [TimeSequence](classma_1_1_time_sequence.html) has the requeted type.

------------------------------------------------------------------------

    Map < const  Array < N > > ma::maths::Array::to_array ( const  TimeSequence  *  ts ,  int  offset  = 0 ,  int  type  = -1 ) [inline]

Extract from a [TimeSequence](classma_1_1_time_sequence.html) *ts* a Map&gt; where the number of columns of the resulting array is used as the number of components to extract. It is possible to specify a possible *offset* to shift the data to extract. The use of *type* will verify if the [TimeSequence](classma_1_1_time_sequence.html) has the requeted type.

------------------------------------------------------------------------

    Result ma::maths::Array::to_arraybase_derived ( T *  ts ,  int  components ,  int  offset  = 0 ,  int  type  = -1 ) [inline]

Extract a Result Map object from the given [TimeSequence](classma_1_1_time_sequence.html) *ts*. The Result object will have *componments* columns. If necessary the position of the data to extract can be shifted. It is also possible to specify the type of the [TimeSequence](classma_1_1_time_sequence.html) by specifying a [TimeSequence::Type](classma_1_1_time_sequence.html#1a8e5ba2425b030c3b7726203c1efbdac2) value to *type*. If no type is required, you can let the value to -1. In case the number of components or the shift is greater than the number of columns, a empty object will be returned, This is the same if the expected type is not the good one.

------------------------------------------------------------------------

    Map <  Position  > ma::maths::Array::to_position ( TimeSequence  *  ts ) [inline]

Specialized extraction method where the resulting Map has 3 columns (as well as the input - no possible offset) and the type must be set to [TimeSequence::Marker](classma_1_1_time_sequence.html#1a8e5ba2425b030c3b7726203c1efbdac2a41224d53bbc08dfbffc316515e13a698).

------------------------------------------------------------------------

    Map < const  Position  > ma::maths::Array::to_position ( const  TimeSequence  *  ts ) [inline]

Specialized extraction method where the resulting Map has 3 columns (as well as the input - no possible offset) and the type must be set to [TimeSequence::Marker](classma_1_1_time_sequence.html#1a8e5ba2425b030c3b7726203c1efbdac2a41224d53bbc08dfbffc316515e13a698).

------------------------------------------------------------------------

    Map <  Scalar  > ma::maths::Array::to_scalar ( TimeSequence  *  ts ,  int  offset  = 0 ,  int  type  = -1 ) [inline]

Specialized extraction method where the resulting Map has 1 column. It is possible to specify a possible *offset* to shift the data to extract. The use of *type* will verify if the [TimeSequence](classma_1_1_time_sequence.html) has the requeted type.

------------------------------------------------------------------------

    Map < const  Scalar  > ma::maths::Array::to_scalar ( const  TimeSequence  *  ts ,  int  offset  = 0 ,  int  type  = -1 ) [inline]

Specialized extraction method where the resulting Map has 1 column. It is possible to specify a possible *offset* to shift the data to extract. The use of *type* will verify if the [TimeSequence](classma_1_1_time_sequence.html) has the requeted type.

------------------------------------------------------------------------

    Map <  Vector  > ma::maths::Array::to_vector ( TimeSequence  *  ts ,  int  offset  = 0 ,  int  type  = -1 ) [inline]

Specialized extraction method where the resulting Map has 3 columns. It is possible to specify a possible *offset* to shift the data to extract. The use of *type* will verify if the [TimeSequence](classma_1_1_time_sequence.html) has the requeted type.

------------------------------------------------------------------------

    Map < const  Vector  > ma::maths::Array::to_vector ( const  TimeSequence  *  ts ,  int  offset  = 0 ,  int  type  = -1 ) [inline]

Specialized extraction method where the resulting Map has 3 columns. It is possible to specify a possible *offset* to shift the data to extract. The use of *type* will verify if the [TimeSequence](classma_1_1_time_sequence.html) has the requeted type.

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


