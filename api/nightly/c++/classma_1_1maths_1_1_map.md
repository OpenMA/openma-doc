[**](https://github.com/openma/openma-doc/edit/api/nightly/c++/classma_1_1maths_1_1_map.md "Improve this documentation")
ma::maths::Map
==============

An array expression mapping an existing array of data.

Detailed Description
--------------------

Todo
Write a detailed description

Member Type Documentation
-------------------------

    ma::maths::Map::Index

Type used to access elements in Values or Residuals.

------------------------------------------------------------------------

    ma::maths::Map::Residuals

Type representing the residuals associated with the data. Depending of the inheriting class (e.g [Array](classma_1_1maths_1_1_array.html) or [Map](classma_1_1maths_1_1_map.html)), the residuals are stored using specific Eigen ([http://eigen.tuxfamily.org](http://eigen.tuxfamily.org.html)) object (i.e. Eigen::Array or Eigen::Map).

------------------------------------------------------------------------

    ma::maths::Map::Scalar

Type used for each element in Values and Residuals.

------------------------------------------------------------------------

    ma::maths::Map::Values

Type representing the data. Depending of the inheriting class (e.g [Array](classma_1_1maths_1_1_array.html) or [Map](classma_1_1maths_1_1_map.html)), the data are stored using specific Eigen ([http://eigen.tuxfamily.org](http://eigen.tuxfamily.org.html)) object (i.e. Eigen::Array or Eigen::Map).

------------------------------------------------------------------------

Member Function Documentation
-----------------------------

    ma::maths::Map::Map ( ) [inline]

Default constructor. This create a null map. The method [isValid()](classma_1_1maths_1_1_array_base.html#1a541b335de173114d5efd0a7adeaaab96) will return false. The use of this constructor is interesting only if you want to reuse a variable.

------------------------------------------------------------------------

    ma::maths::Map::Map ( Index  rows ,  Scalar  *  values ,  Scalar  *  residuals ) [inline]

Constructor where *rows* must correspond to the number of rows provided in *values* and *residuals*. The number of elements in *values* must correspond to *rows* multiplied by the number of columns used by the *Derived* class. The number of elements in *residuals* must correspond to *rows* elements.

------------------------------------------------------------------------

    ma::maths::Map::Map ( const  Map < U > &  other ) [inline]

Copy constructor for const [Map](classma_1_1maths_1_1_map.html) only

------------------------------------------------------------------------

    Map < Derived > & ma::maths::Map::operator= ( const  XprBase < U > &  other ) [inline]

Assignment operator from any other template expression

Warning: You should be sur to have a [](classma_1_1maths_1_1_map.html) object able to store the result of the template expression **. Otherwise, you should have a crash (buffer overflow). Do not use the default constructor. :

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


