ma::Property
============

Define a static propery used in [ma::Node](classma_1_1_node.html) class or inheriting classes.

Detailed Description
--------------------

A [Property](structma_1_1_property.html) object define a static property. Compared to a dynamic one, a static property is linked with a accessor and optionaly a mutator declared in the same class than the property.

Because a [Node](classma_1_1_node.html) object can store properties with any string as key, a user could decide to call a property with a key corresponding to an existing member (for example, [Node](classma_1_1_node.html)'s name). What should be the behaviour of this property? Instead of having a possible ambiguity between properties and other members known at compile time (or even data duplication), it was decided to implement a mechanism of static and dynamic properties transparent to the user. The static properties would reflect some members known at compile time, while dynamic properties are created during run time.

Note: the type ** must be exactly the same than the type returned/required by the accessor/mutator with all the qualifiers. For example, if the accessor is const std::string& name() const, and the mutator is void setName(const std::string& name), then ** as to be set to const std::string& (i.e. const reference to a std::string).

A static property is defined only by its constructor. All the other methods are used only internaly. Moreover, this constructor has to be used in the macro [OPENMA\_DECLARE\_STATIC\_PROPERTIES\_BASE()](classma_1_1_node.html#1a84ad3cb099b81c2c8e5c6776971e1a10) or [OPENMA\_DECLARE\_STATIC\_PROPERTIES\_DERIVED()](classma_1_1_node.html#1aa640a3676effeed9efc2d1cdd15c861d) which itself must be included in the declaration of the private implementation part. The difference between the macros [OPENMA\_DECLARE\_STATIC\_PROPERTIES\_BASE()](classma_1_1_node.html#1a84ad3cb099b81c2c8e5c6776971e1a10) and [OPENMA\_DECLARE\_STATIC\_PROPERTIES\_DERIVED()](classma_1_1_node.html#1aa640a3676effeed9efc2d1cdd15c861d) is about the inheriting of a class or not. Code using OpenMA as a third party library should not have access to the private implementation (i.e. \*Private classes). So a base private implementation must be firstly done. The first macro must be used in this case. For example:
    class TestNodePrivate;

    class TestNode : public ma::Node
    {
      OPENMA_DECLARE_PIMPL_ACCESSOR(TestNode) // For the private implementation (pimpl)
      
    public:
      TestNode(const std::string& name, Node* parent = nullptr);
      
      int version() const;
      void setVersion(int value);

    protected:
      TestNode(TestNodePrivate& pimpl, const std::string& name, Node* parent);

    private:
      std::unique_ptr mp_Pimpl; // This is the way to store the private implementation
    };

    class TestNodePrivate
    {
      OPENMA_DECLARE_PINT_ACCESSOR(TestNode) // To have access to the public interface (pint) from the private implementation
      
      // Declare property(ies) for a base class
      OPENMA_DECLARE_STATIC_PROPERTIES_BASE(TestNode
        ma::Property("version")
      )
      
    public:
      TestNodePrivate(TestNode* pint, int version) : Version(version), mp_Pint(pint) {};
      int Version;

    protected:
      TestNode* mp_Pint; // Storage of the public interface.
    };

    class TestNode2Private;

    class TestNode2 : public TestNode
    {
      OPENMA_DECLARE_PIMPL_ACCESSOR(TestNode2) // For the private implementation (pimpl)
      
    public:
      TestNode2(const std::string& name, int version, Node* parent = nullptr);
    };

    class TestNode2Private
    {
      OPENMA_DECLARE_PINT_ACCESSOR(TestNode2) // To have access to the public interface (pint) from the private implementation
      
      // Declare property(ies) for a derived class
      OPENMA_DECLARE_STATIC_PROPERTIES_DERIVED(TestNode2, TestNode
        ma::Property("version2")
      )
      
    public:
      TestNode2Private(TestNode* pint, int version) : TestNodePrivate(pint, version) {};
    };

In this example, The class TestNode will have a new property name "version" which is associated with the accessor TestNode::version and the mutator TestNode::setVersion. Internally, these methods rely on the member TestNodePrivate::Version. If the member is read-only the pointer to the mutation must be set to nullptr (e.g. in the definition of the propoerty version2 for the class TestNode2).

Member Type Documentation
-------------------------

    ma::Property::ValueType

Type of the value associated with the property

------------------------------------------------------------------------

Member Function Documentation
-----------------------------

    constexpr ma::Property::Property ( const  char( & )  [N]  l ) [inline]

Constructor.

------------------------------------------------------------------------

    U ma::Property::get ( const  T *  obj ) const noexcept [inline]

Returns a value from the given object *obj* using the accessor set in the 3rd template argument `(U (T::*A)() const)`.

------------------------------------------------------------------------

    void ma::Property::set ( T *  obj ,  U  value ) const noexcept [inline]

Sets the given *value* to the given object *obj* using the mutator set in the 4rd template argument `void (T::*M)(U)`.

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


