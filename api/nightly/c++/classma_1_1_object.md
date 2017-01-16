ma::Object
==========

Base for all objects which need to keep track of modified time.

Detailed Description
--------------------

This class uses the private implementation (pimpl) idiom to keep an ABI compatibility between the different releases of the project.

Two macros are provided to simplify the implementation of the pimpl idiom. Both of them are defined in the file "openma/base/opaque.h".

-   [OPENMA\_DECLARE\_PIMPL\_ACCESSOR()](#1a42d82423cf13709e1df5131d21de2640): Creates pimpl() methods in the public interface to access to the private part (opaque pointer)
-   [OPENMA\_DECLARE\_PINT\_ACCESSOR()](#1a0a5b1a81a45138d9a99cb01c6e1fc6b5): Creates pint() methods in the private implementation to access to the public part

For example, the following header file create a new class which contains an accessor and mutator for a member 'Version' in the (opaque) private implementation. The macro [OPENMA\_DECLARE\_PIMPL\_ACCESSOR()](#1a42d82423cf13709e1df5131d21de2640) declares private pimpl() methods used to access to the mp\_Pimpl member. The methods are able to downcast to the given classname. This is useful when the implemented class inherits from a class that already uses the pimpl idiom.

To use the macros for custom development you can follow the next examples. The first and second introduce the macros while the third introduces their use to inherit from the class openma::Object

First the public interface is defined in a header file.

    class MyObject
    {
      OPENMA_DECLARE_PIMPL_ACCESSOR(MyObject) // pimpl() methods
      
    public:
      MyObject();
      int version() const _OPENMA_NOEXCEPT;
      void setVersion() const _OPENMA_NOEXCEPT:

      void print() const;
     
    private:
      struct Private; // Forward declaration
      std::unique_ptr mp_Pimpl; // RAII storage
    };

The associated implementation file can be presented as in the following example. The MyObject::Private data structure is defined as well as the needed methods for the class MyObject.

    struct MyObject::Private
    {
      Private();
      int Version;
    };

    MyObject::Private::Private()
    : Version(1)
    {};

    MyObject::MyObject()
    : mp_Pimpl(new Private(this))
    {};

    int MyObject::version() const
    {
      auto optr = this->pimpl();
      return optr->Version;
    };

    void MyObject::setVersion(int value)
    {
      auto optr = this->pimpl();
      optr->Version = value;
    };

    void MyObject::print() const
    {
      std::cout << this->version() << std::endl;
    };

In the following example, the macro defining the accessors of the public interface in the private implementation is used. It is also important to declare a member *mp\_Pint* and a constructor with a pointer to the public interface to be useable.

    struct MyObject::Private
    {
      OPENMA_DECLARE_PINT_ACCESSOR(MyObject) // pint() methods
      Private(MyObject* pint); // Constructor with a pointer associated to the public interface object
      MyObject* mp_Pint;
      int Version;
      void foo(); // internal method
    };

    MyObject::Private::Private(MyObject* pint)
    : mp_Pint(pint), Version(1)
    {};

    MyObject::Private::foo()
    {
      this->pint()->print(); // Call a method of the public interface.
    }

    MyObject::MyObject()
    : mp_Pimpl(new Private(this))
    {};

    int MyObject::version() const
    {
      auto optr = this->pimpl();
      return optr->Version;
    };

    void MyObject::setVersion(int value)
    {
      auto optr = this->pimpl();
      optr->Version = value;
    };

    void MyObject::print() const
    {
      std::cout << this->version() << std::endl;
    };

Finally, to extend OpenMA with a new class, you can inherit from the class openma::Object (or other inherited classes). Thus it is even simpler to use the pimpl idiom. Indeed, the member mp\_Pimpl is already declared in the class openma::Object. You only need to inherit from the public and private part. Note that, to inherit from the private part, this one is defined in its own private header file (with the suffix \_p) to not have it visible and possible break the ABI compatibilty.

    class MyObjectPrivate; // Defined outside in case it can be reused

    class MyObject : public Object
    {
      OPENMA_DECLARE_PIMPL_ACCESSOR(MyObject)
      
    public:
      MyObject();
      int version() const _OPENMA_NOEXCEPT;
      void setVersion() const _OPENMA_NOEXCEPT:

    protected:
      MyObject(MyObjectPrivate& pimpl) _OPENMA_NOEXCEPT; // Only needed if this class could be inherited
    };

The private header file (e.g. MyObject\_p.h) could be like this:

    struct MyObjectPrivate : public ObjectPrivate
    {
      MyObjectPrivate()
      int Version;
    };

And the implementation file:

    MyObject::MyObject()
    : openma::Object(*new MyObjectPrivate())
    {};

    int MyObject::version() const
    {
      auto optr = this->pimpl();
      return optr->Version;
    };

    void MyObject::setVersion(int val)
    {
      auto optr = this->pimpl();
      if (optr->Version != val)
      {
        optr->Version = val;
        this->modified();
      }
    };

    MyObject::MyObject(MyObjectPrivate& pimpl) _OPENMA_NOEXCEPT
    : Object(pimpl)
    {};

Member Function Documentation
-----------------------------

    ma::Object::Object ( )

Constructor. Initialize the timestamp to 0

------------------------------------------------------------------------

    ma::Object::Object ( ObjectPrivate  &  pimpl ) noexcept

Constructor for inherited class with a custom private implementation (i.e. with new properties)

------------------------------------------------------------------------

    ma::Object::~Object ( ) noexcept [virtual]

Destructor

Note: The opaque pointer representing the private implementation is automatically deleted as it is contained in a std::unique\_ptr object. :

------------------------------------------------------------------------

    Object  * ma::Object::clone ( ) const [virtual]

Create a deep copy of the object and return it as another object.

Note: Each subclass must override this method to correctly do the deep copy. :

------------------------------------------------------------------------

    void ma::Object::copy ( const  Object  *  src ) noexcept [virtual]

Do a deep copy of the the given *src*. The previous content is replaced.

Note: Each subclass must override this method to correctly do the deep copy. :

------------------------------------------------------------------------

    void ma::Object::modified ( ) noexcept [virtual]

Sets the object as modified (its timestamp is updated). It is important to use this method each time a member of the object is modified.

------------------------------------------------------------------------

    unsigned long ma::Object::timestamp ( ) const noexcept

Returns the timestamp of the object.

------------------------------------------------------------------------

Macros Documentation
--------------------

    OPENMA_DECLARE_PIMPL_ACCESSOR  ( classname  )

Creates pimpl() methods in the public interface to access to the private part (opaque pointer)

------------------------------------------------------------------------

    OPENMA_DECLARE_PINT_ACCESSOR  ( classname  )

Creates pint() methods in the private implementation to access to the public part

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


