ma::typeid\_t
=============

Unique identifier for each type without using runtime type identifier.

Detailed Description
--------------------

Internally, and compared to the RTTI mechanism, this class use the so-called one-definition rule (ODR).

> \[...\] If an identifier declared with external linkage is used in an expression \[...\], somewhere in the entire program there shall be exactly one external definition for the identifier; \[...\]

Largely inspired by [http://codereview.stackexchange.com/questions/48594/unique-type-id-no-rtti](http://codereview.stackexchange.com/questions/48594/unique-type-id-no-rtti.html)

Member Function Documentation
-----------------------------

    ma::typeid_t::typeid_t ( ) [inline]

Default constructor (nullptr id)

------------------------------------------------------------------------

    ma::typeid_t::typeid_t ( const  typeid_t  & )

Copy constructor

------------------------------------------------------------------------

    ma::typeid_t::typeid_t ( typeid_t  &&  other ) noexcept [inline]

Move constructor

------------------------------------------------------------------------

    ma::typeid_t::~typeid_t ( ) noexcept

Destructor

------------------------------------------------------------------------

    ma::typeid_t::operator size_t ( ) const noexcept [inline]

Explicit converter to the type `size_t`

------------------------------------------------------------------------

    typeid_t  & ma::typeid_t::operator= ( const  typeid_t  & )

Assignment operator

------------------------------------------------------------------------

    typeid_t  & ma::typeid_t::operator= ( typeid_t  &&  other ) noexcept [inline]

Assignment operator

------------------------------------------------------------------------

Related Non-Members Documentation
---------------------------------

    constexpr  bool ma::typeid_t::operator!= ( typeid_t  lhs ,  typeid_t  rhs ) noexcept [inline]

Inequality operator. Compare if the internal ID are not the same between both objects

------------------------------------------------------------------------

    constexpr  bool ma::typeid_t::operator== ( typeid_t  lhs ,  typeid_t  rhs ) noexcept [inline]

Equality operator. Compare if the internal ID are the same between both objects

------------------------------------------------------------------------

    friend constexpr  typeid_t ma::typeid_t::static_typeid ( ) noexcept

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


