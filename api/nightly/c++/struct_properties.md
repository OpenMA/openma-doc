[**](https://github.com/openma/openma-doc/edit/api/nightly/c++/struct_properties.md "Improve this documentation")
Properties
==========

Template interface used to manage static properties defined for a class.

Detailed Description
--------------------

The goal of this interface is to visit each static properties defined for an object and see if the given key exist. If it is the case, then the associated given value is accessed or modified depending the context. All this part is transparent for the user which will use the method Node::property() and Node::setProperty().

Note: This class should not be used directly but instead the macro OPENMA\_DECLARE\_STATIC\_PROPERTIES().

Member Function Documentation
-----------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


