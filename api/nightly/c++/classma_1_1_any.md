[**](https://github.com/openma/openma-doc/edit/api/nightly/c++/classma_1_1_any.md "Improve this documentation")
ma::Any
=======

Generic type to store and convert other types.

Detailed Description
--------------------

As the C++ language is a strong typed language it is not possible to use the same variable to hold an integer, a real, or a string. In most of the cases, this is not a problem as this is a feature of the C++ language. However, some applications would require to store different kind of data in a same variable (like a database's fields). There are already existing solutions like union keyword in the C++ language, Boost::Variant, Boost::Any, or QVariant solution. However, some of them are only definable at compile time (union, Boost::Variant) or cannot freely convert stored value between different types (e.g. string to integer) like Boost::Any. In case the stored type is not known at run-time and the use of the run-time type information (RTTI) mechanism is discouraged, only the Qt class QVariant gives the possibity to store a generic content and convert it (if possible) in the desired type. However, the use of QVariant means you need to link your code the QtCore module which could be very heavy if you have a lightweight project. Moreover, QVariant could support more type than desired (QColor, QFont, QByteArray, etc.)

The class [ma::Any](classma_1_1_any.html) was implemented to have a similiar behaviour than QVariant using the Boost naming convention. Indeed, the purpose of [ma::Any](classma_1_1_any.html) is closer of Boost::Any than Boost::Variant.

The implementation of the class [ma::Any](classma_1_1_any.html) relies heavily on the features introduced in the C++11 revision of the C++ standard (constexpr, variadic templates, initializer lists, static assertions, rvalue, move, etc.).

The internal behaviour of the class is mostly composed of three elements:

-   A type-erasure storage containing the data
-   A [cast()](#1a68b769039b9b910297480cdcd0cba4ba) method implemented differently depending the type requested (using the SFINAE technique)
-   A static table (std::unordered\_map) containing all the custom conversions between registered types.

By default, all the arithmetic types (bool, integers, floating points) and the std::string type are convertible between them

    ma::Any a(5); // store an integer with the value 5
    int ifive = a; // will contain the value 5.
    std::string str = a; // will contain the string "5".
    bool active = a; // will be set to true.
    float ffive = a; // will store the value 5.0f.
    a = "something else"; // And now 'a' contains a string
    ifive = a; // invalid conversion, the stored value is now 0.
    str = a; // Will contain the string "something else".
    active = a; // Still the value is equal to true.
    ffive = a; // Invalid conversion, the stored value is set to 0.0f

It is possible to register new types verified at compile time. For this, the type must answer two requirements:

-   Have a valid default constructor
-   Have an non-member equal operator

For example, if you want to register the class `Date` defined as:

    struct Date
    {
      int Year, Month, Day;

      friend bool operator==(const Date& lhs,const Date& rhs)
      {
        return ((lhs.Year == rhs.Year) && (lhs.Month == rhs.Month) && (lhs.Day == rhs.Day));
      };
    };

It is then possible to register it using the [ma::Any::Register](structma_1_1_any_1_1_register.html) command.

    // Must be in a function. For example the main(). The scope of the registration
    // is valid until the end of the program.
    ma::Any::Register< Date, ma::converter<>, ma::converter<> >();
    //                 ^^^^
    //      Registered type
    //                       ^^^^^^^^^^^^^^^
    //     A Date stored in a ma::Any object
    //       can be converted to these types
    //      (none available in this example)
    //                                        ^^^^^^^^^^^^^^^
    //          A Date object can be created from another type
    //                         (none available in this example)

When conversions are intended. the internal converter must be specialized in consequence. For example, if a `Date` can be converted to a `std::string` or created from a `std::string`, two specializations are required.

    template<>
    // From std::string to Date.
    struct ma::Any::Converter::Helper : ma::Any::Converter::HelperBase
    {
      // Fake conversion. The goal is only the show the specialization of the converter. 
      static inline Date convert(const std::string& )
      {
        return Date{2009,05,02};
      };
    };

    // From Date to std::string.
    template<>
    struct ma::Any::Converter::Helper : ma::Any::Converter::HelperBase
    {
      static inline std::string convert(const Date& val)
      {
        return std::to_string(val.Year) + "-" + std::to_string(val.Month) + "-" + std::to_string(val.Day);
      };
    };

The registration in the conversion table would be then:

    ma::Any::Register< Date, ma::converter< Date,std::string >, ma::converter< std::string > >();

In case a user type has to be unregistered (e.g. plugin unloaded), the command [ma::Any::Unregister](structma_1_1_any_1_1_unregister.html) must be called.

    // The next line unregisters all the conversions related to a Date object. 
    // You can still store a Date object in ma::Any, but only a conversion to
    // it its own type will be valid
    ma::Any::Unregister();
    ma::Any a(Date{2009,05,02});
    ma::Date b = a; // 2009,05,02
    std::string c = a; // empty string

Member Function Documentation
-----------------------------

    ma::Any::Any ( ) noexcept

Default constructor. This kind of [Any](classma_1_1_any.html) object is defined as null (method [Any::isValid()](#1a536031be6fb18b27a41d648538ce6038) returns true).

------------------------------------------------------------------------

    ma::Any::Any ( const  Any  &  other )

Copy constructor. If the content of the copied object (`other`) is not null, it will be cloned (deep copy) in the copy

------------------------------------------------------------------------

    ma::Any::Any ( Any  &&  other ) noexcept

Move constructor The content of `other` is moved to this object. The content of `other` is then defined as null (method [Any::isValid()](#1a536031be6fb18b27a41d648538ce6038) returns true).

------------------------------------------------------------------------

    ma::Any::Any ( U  &&  value ,  D  &&  dimensions  = D{} )

Constructor which store the given *value* and *dimensions* (optional). When no dimension is given, this one is set automatically based on the given *value*.

In case the number of elements in the *value* is not the same than the number of *dimension*, the later is chosen. Data can be truncated or expanded with default value.

------------------------------------------------------------------------

    ma::Any::Any ( std::initializer_list< U >  values ,  std::initializer_list< size_t >  dimensions  = {} )

Constructor which store the given *value* and *dimensions* (optional). When no dimension is given, this one is set automatically based on the given *value*.

In case the number of elements in the *value* is not the same than the number of *dimension*, the later is chosen. Data can be truncated or expanded with default value.

------------------------------------------------------------------------

    ma::Any::~Any ( )

Destrutor Delete the internal data.

------------------------------------------------------------------------

    void ma::Any::assign ( U  &&  value ) noexcept

Convenient method to assign a value to an [Any](classma_1_1_any.html) object.

------------------------------------------------------------------------

    U ma::Any::cast ( ) const noexcept

Method to explicitly convert the content of this object to the given type.

    ma::Any a("5");
    std::string str = a.cast();

See also [Any::operator U()](#1a4c5dced3339bd6ddda5572e67fdd54ac)

------------------------------------------------------------------------

    U ma::Any::cast ( size_t  idx ) const noexcept

Method to explicitely convert one element of this object to the given type.

    ma::Any a({"5","7"});
    std::string str = a.cast(1);

See also [Any::operator U()](#1a4c5dced3339bd6ddda5572e67fdd54ac)

------------------------------------------------------------------------

    std::vector< size_t > ma::Any::dimensions ( ) const noexcept

Return a vector with the dimensions associated with the data stored.

------------------------------------------------------------------------

    bool ma::Any::isEmpty ( ) const noexcept

Return true if the object as a non-empty content, otherwise false. In case the object is not valid, this method returns false too.

------------------------------------------------------------------------

    bool ma::Any::isEqual ( U  &&  value ) const noexcept

Convenient method to compare the content of an [Any](classma_1_1_any.html) object with the given value.

------------------------------------------------------------------------

    bool ma::Any::isValid ( ) const noexcept

Return true if the object has a content, otherwise false.

------------------------------------------------------------------------

    ma::Any::operator U ( ) const noexcept

Type conversion operator. Internally this operator uses the [Any::cast()](#1a68b769039b9b910297480cdcd0cba4ba) method.

------------------------------------------------------------------------

    Any  & ma::Any::operator= ( const  Any  &  other )

Copy assignement operator. In case the assigned object is not this one, the previous content is deleted and replaced by a deep copy of the content of the `other` object.

------------------------------------------------------------------------

    Any  & ma::Any::operator= ( Any  &&  other ) noexcept

Move assignement operator. In case the assigned object is not this one, the previous content is deleted and replaced by the content of the `other` object. The `other` object is then defined as null (method [Any::isValid()](#1a536031be6fb18b27a41d648538ce6038) returns true).

------------------------------------------------------------------------

    size_t ma::Any::size ( ) const noexcept

Returns the number of elements stored.

------------------------------------------------------------------------

    void ma::Any::swap ( Any  &  other ) noexcept

Swap the content of two [Any](classma_1_1_any.html) object.

------------------------------------------------------------------------

Related Non-Members Documentation
---------------------------------

    bool ma::Any::operator!= ( const  Any  &  lhs ,  const  Any  &  rhs ) noexcept

Inequal operator. Returns the opposite of equal operator.

------------------------------------------------------------------------

    bool ma::Any::operator!= ( const  A  &  lhs ,  const  U  &  rhs ) noexcept [inline]

Convenient inequal operator to compare an [Any](classma_1_1_any.html) object (`lhs`) with another object of type `U` (`rhs`). Internally this operator take the opposite of the equal operator.

------------------------------------------------------------------------

    bool ma::Any::operator!= ( const  U  &  lhs ,  const  A  &  rhs ) noexcept [inline]

Convenient inequal operator to compare an object of type `U` (`lhs`) with an [Any](classma_1_1_any.html) object (`rhs`). Internally this operator take the opposite of the equal operator.

------------------------------------------------------------------------

    bool ma::Any::operator== ( const  Any  &  lhs ,  const  Any  &  rhs ) noexcept

Equal operator. Compare the content of two [Any](classma_1_1_any.html) objects.

------------------------------------------------------------------------

    bool ma::Any::operator== ( const  A  &  lhs ,  const  U  &  rhs ) noexcept [inline]

Convenient equal operator to compare an [Any](classma_1_1_any.html) object (`lhs`) with another object of type `U` (`rhs`).

------------------------------------------------------------------------

    bool ma::Any::operator== ( const  U  &  lhs ,  const  A  &  rhs ) noexcept [inline]

Convenient equal operator to compare an object of type `U` (`lhs`) with an [Any](classma_1_1_any.html) object (`rhs`). Internally this operator does (rhs == lhs).

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


