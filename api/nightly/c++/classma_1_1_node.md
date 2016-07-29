ma::Node
========

Base class for the data structure.

Detailed Description
--------------------

The data struture in OpenMA is mostly a tree-like structure (more exactly it is a graph as a node can have several parents). The general idea is to store data in a dynamic structure without the need to modify the internal storage each time a new category of data is added (e.g. pressure, GPS, etc.). Thus, it would be simpler to integrate new kind of file formats as well as new models.

Children nodes are owned by their parents. Thus only the first parent(s) (e.g. the root' tree) has to be deleted. This one can be stored in a smart pointer (shared, unique pointer) to not manage its deletion. For example:

    ma::Node* root = new ma::Node("root");
    ma::Node* leafA = new ma::Node("leafA",&root); // Owned by the root
    ma::Node* leafB = new ma::Node("leafB",&root); // Owned by the root
    // ...
    delete leafB; // Early deletion. LeafB is removed from the root's children.
    // ...
    delete root; // End of the program/function, the root is deleted and leafA at the same time.

It is strongly adviced to create nodes on the heap (using the new operator). This is important for the child management when some of them might be replaced internally (for example using the method [replaceChild()](#1adc6a10a7ad65ba9468462eb26cc664f7)), otherwise your program might crash due to an undefined behaviour.

In case you want to use [Node](classma_1_1_node.html) objects only as a tree data structure without later modification (e.g. child replacement, child deletion), these ones can be created on the stack (using regular constructor), they must follow a specific order: the parent must be created before the children. For example:

    ma::Node root("root");
    ma::Node leafA("leafA",&root); // Owned by the root
    ma::Node leafB("leafB",&root); // Owned by the root
    // ...
    // end of the program/function. Nodes leafB, leafA, and root are destroyed in thid order.

In case this order is not respected, a runtime error (or crash) should occur like in the next example:

    ma::Node leafA("leafA");
    ma::Node root("root");
    ma::Node leafB("leafB",&root); // Owned by the root
    leafA.addParent(&root); // Owned by the root
    // ...
    // End of the program/function, leafB is destroyed, then root which destroys also its children. What about leafA?

In the previous example, the remaining child of root (pointer to leafA) is a local variable and calling its destructor is incorrect. Thus, when the variable leafA goes out of scope, its destructor is called again. The same memory is freed two times that should crash the program.

Finally, to declare a custom node type (i.e. a new inheriting class), several macros can be used:

-   [OPENMA\_NODE()](group__openma__base.html#1gad7dad27a69462c47cb5df1588056ff27)
-   [OPENMA\_DECLARE\_NODEID()](#1a5bcd03c98856473b51f4b8d63df7e7c9)
-   [OPENMA\_DECLARE\_STATIC\_PROPERTIES\_DERIVED()](#1aa640a3676effeed9efc2d1cdd15c861d)

For example if you want to add a class inside OpenMA, it is advised to do as following

    // Public API
    class OPENMA_NODE(OPENMA_BASE_EXPORT, MyNode) : public ma::Node
    {
      OPENMA_DECLARE_PIMPL_ACCESSOR(MyNode)
      OPENMA_DECLARE_NODEID(MyNode, Node)

    public:
      // ...
    }

    // PRIVATE API (declared for example in a private header file)
    class MyNode;

    class MyNodePrivate : public NodePrivate
    {
      OPENMA_DECLARE_PINT_ACCESSOR(MyNode)

      OPENMA_DECLARE_STATIC_PROPERTIES_DERIVED(MyNode, Node,
        Property{"time"}
      )

    public:
      // ...

For more details about properties you can read the documentation of the class [Property](structma_1_1_property.html).

Properties Documentation
------------------------

    description :  std::string 

This property holds the description of a [Node](classma_1_1_node.html). By default, this property contains an empty string.

See also [description()](#1a148126aa1173957a74993cb4528dedd9), [setDescription()](#1a02dbe58e333c9e07feb72258d1c2d8bf)

------------------------------------------------------------------------

    name :  std::string 

This property holds the name of a [Node](classma_1_1_node.html). By default, this property contains an empty string.

See also [name()](#1a124aca538ea5da6b8924088af226e7fd), [setName()](#1a59a3d8081ed3248c138ece25023842ee)

------------------------------------------------------------------------

Member Function Documentation
-----------------------------

    ma::Node::Node ( const  std::string  &  name ,  Node  *  parent  = nullptr )

Constructor. The *parent* node takes ownership of this object.

Note: It is adviced to have a unique **. This would simplify the research of specific nodes with the methods [](#1a6f9bd3dcec455f96d399f5569fcac5b0) and [](#1a551f8f8dac469dbddc7e50641f208f8d). :

------------------------------------------------------------------------

    ma::Node::Node ( NodePrivate  &  pimpl ,  Node  *  parent ) noexcept

Constructor to be used by inherited object which want to add informations (static properties, members, etc) to the private implementation.

------------------------------------------------------------------------

    ma::Node::~Node ( ) noexcept [virtual]

Destructor. Detach this object of these children. In case a child has no more parent, it is deleted. Detach also this object of these parents

------------------------------------------------------------------------

    void ma::Node::addParent ( Node  *  node ) noexcept

Appends a node if this one is not already a parent. In case this node is added, *node* is attached as parent and its state is set to modified.

------------------------------------------------------------------------

    U ma::Node::child ( unsigned  index ) const noexcept

Returns the node associated with the given *index* or null if out of range. By default the returned type is [Node](classma_1_1_node.html) but can be set to any inheriting class. If the set type does not correspond to the internal type for the given *index*, a null value is returned.

    auto root = ma::Node("root");
    auto ev1 = ma::Event("LHE");
    auto out_of_range = root.child(1); // nullptr returned as the index is out of range
    auto wrong_cast = root.child(0); // nullptr as the node at index #0 is a ma::Event object
    auto default_cast = root.child(0); // Return a pointer to a ma::Node object
    auto event_cast = root.child(0); // Return a pointer to a ma::Event object

------------------------------------------------------------------------

    const std::list<  Node  * > & ma::Node::children ( ) const noexcept

Returns the list of children attached with this node.

------------------------------------------------------------------------

    void ma::Node::clear ( ) noexcept

Removes all parents, children and properties If a child has no more parent, this one is deleted.

------------------------------------------------------------------------

    Node  * ma::Node::clone ( Node  *  parent  = nullptr ) const [virtual]

Create a deep copy of the object and return it as another object.

Note: Each subclass must override this method to correctly do the deep copy. :

------------------------------------------------------------------------

    void ma::Node::copy ( const  Node  *  src ) noexcept [virtual]

Do a deep copy of the the given *src*. The previous content is replaced.

Note: Each subclass must override this method to correctly do the deep copy. :

Note: This method does not copy the parent. If you need to copy the parent, you must use the method [](#1a9f6c38a01fa8921ca83fb3d129d4accd) afterwards. :

------------------------------------------------------------------------

    const  std::string  & ma::Node::description ( ) const noexcept

Returns the description of the node. By default the description is empty. You can also access to this information using the property 'description'.

------------------------------------------------------------------------

    U ma::Node::findChild ( const  std::string  &  name  = std::string{} ,  std::list< std::pair< std::string,  Any  >> &&  properties  = {} ,  bool  recursiveSearch  = true ) const noexcept

Returns the child with the given *name* and which can be casted to the type T. You can refine the search by adding *properties* to match. The search can be done recursively (by default) or only in direct children. The latter is available by setting *recursiveSearch* to false. There are three ways to use this methods.

You can explicitely define the type *T* and the *name*.

    ma::Event* = root.findChild("RHS2");

You can also only give the type *T*. Then the first node found with this type will be returned. In this case, no name is given as it is set to a null string (not empty)

    ma::ForcePlatform* = root.findChild();

By default, the default type is set to [ma::Node](classma_1_1_node.html)\*, so you can even search for a "node" without giving the type..

    ma::Node* foo = root.findChild(); // First child
    ma::Node* bar = root.findChild("bar"); // A node with the name "bar"

In addition, you can add properties to refine the research. Sometimes this could be usefull to distinguish events with the same name but different properties. As presented in the following examples, it is adviced to give matching properties in an initializer list using curly brackets due to the use of the move semantics in the method. Inside, each matching property is given as a pair {key, value} given also by an initializer list. So, for a single matching property, two pairs of curly brackets are used but this is correct.

    ma::Node events("Events");
    ma::Event evtA("Foo",0.0,"Right","JDoe",&events);
    ma::Event evtB("Bar",0.0,"Left","JDoe",&events);
    ma::Event evtC("Toto",1.1,"Left","JDoe",&events);
    ma::Event evtD("Toto",1.5,"Right","Babar",&events);
    events.findChild("Toto",{{"time",1.5}}); // pointer to evtD object
    events.findChild({},{{"time",0.0},{"context","Left"}}); // pointer to evtB object

In any case you can set the third argument to false for a search in the direct children only. If no properties are added, the second argument to give is an empty pair or curly brackets (i.e. {}).

    ma::Event* rhs2 = root.findChild("RHS2",{},false);
    ma::ForcePlatform* fp = root.findChild({},{},false); // {} and std::string() and "" are the same for the name.
    ma::Node* foo = root.findChild({},{},false);
    ma::Node* bar = root.findChild("bar",{},false);

------------------------------------------------------------------------

    std::list< U > ma::Node::findChildren ( const  std::string  &  name  = std::string{} ,  std::list< std::pair< std::string,  Any  >> &&  properties  = {} ,  bool  recursiveSearch  = true ) const noexcept

Returns the children with the given *name* and which can be casted to the type T. You can refine the search by adding *properties* to match. The search can be done recursively (by default) or only in direct children. The latter is available by setting *recursiveSearch* to false. As with the method [findChild()](#1a6f9bd3dcec455f96d399f5569fcac5b0), you can explicitely or implicitely give the type and/or the name of the children. For example:

    std::list events = root.findChildren(); // Find all events
    std::list footstrikes = root.findChildren("Foot Strike"); // Find all foot strike events
    std::list nodes = root.findChildren("Foot Strike"); // Find all node with the name "Foot Strike"

It is adviced to give matching properties by using an initializer list due to the use of the move semantics in the method.

    ma::Node events("Events");
    ma::Event evtA("Foo",0.0,"Right","JDoe",&events);
    ma::Event evtB("Bar",0.0,"Left","JDoe",&events);
    ma::Event evtC("Toto",1.1,"Left","JDoe",&events);
    ma::Event evtD("Toto",1.5,"Right","Babar",&events);
    events.findChildren({},{{"time",0.0}}); // evtA and evtB
    events.findChildren({},{{"context","Right"}}); // evtA and evtD
    events.findChildren({},{{"context","Left"}}); // evtB and evtC
    events.findChildren({},{{"subject","JDoe"}}); // evtA, evtB, and evtC

------------------------------------------------------------------------

    std::list< U > ma::Node::findChildren ( const  V  &  regexp ,  std::list< std::pair< std::string,  Any  >> &&  properties  = {} ,  bool  recursiveSearch  = true ) const noexcept

Convenient method to find children using a regular expression.

------------------------------------------------------------------------

    bool ma::Node::hasChildren ( ) const noexcept

Returns true if the node has at least one child, false otherwise

------------------------------------------------------------------------

    bool ma::Node::hasParents ( ) const noexcept

Returns true if the node has at least one parent, false otherwise.

------------------------------------------------------------------------

    bool ma::Node::isCastable ( typeid_t  id ) const noexcept [virtual]

Returns true if the current object is isCastable to another with the given ** value, false otherwise.

------------------------------------------------------------------------

    void ma::Node::modified ( ) noexcept [virtual]

Overload method which modify this object as well as all these parents.

------------------------------------------------------------------------

    const  std::string  & ma::Node::name ( ) const noexcept

Returns the name of the node. You can also access to this information using the property 'name'.

------------------------------------------------------------------------

    const std::list<  Node  * > & ma::Node::parents ( ) const noexcept

Returns the list of parents attached with this node.

------------------------------------------------------------------------

    Any ma::Node::property ( const  std::string  &  key ) const noexcept [virtual]

Returns the value's property associated to the given *key*. The value is a [Any](classma_1_1_any.html) object and can be converted to several types implicity. For example, the following code shows two ways to extract property's value.

    ma::Node node("node");
    node.setProperty("count","1");
    // First way: use a Any object
    ma::Any value = node.property("count");
    int count1 = value.cast();
     // Second way: implicit type conversion operator
    int count2 = node.property("count");

------------------------------------------------------------------------

    void ma::Node::removeParent ( Node  *  node ) noexcept

Remove the given *node* from the list of the parent.

Note: It is the responsability to the developer to delete this node if this one has no more parent. :

------------------------------------------------------------------------

    void ma::Node::replaceChild ( Node  *  current ,  Node  *  substitute )

Replace the child *current*, by a *substitute*. The node *current* will be deleted if it has no more parent.

------------------------------------------------------------------------

    std::list< const  Node  * > ma::Node::retrievePath ( const  Node  *  node ) const noexcept

Retrieves the first path existing between the current node and the given *node*. If no path exists between both, then an empty list is returned, The first node in the retrieved path is the current one, while the last is the node to search.

------------------------------------------------------------------------

    void ma::Node::setDescription ( const  std::string  &  value ) noexcept

Sets the description of the node. By default the description is empty. You can also modify this information using the property 'description'.

Note: The state of the node is not modified if the description is different. :

------------------------------------------------------------------------

    void ma::Node::setName ( const  std::string  &  value ) noexcept

Sets the name of the node. You can also modify this information using the property 'name'. In case the value is different, the state of the node is set to modified.

------------------------------------------------------------------------

    void ma::Node::setProperty ( const  std::string  &  key ,  const  Any  &  value ) [virtual]

Sets the property *key* with the given *value*. The *value* can be an [Any](classma_1_1_any.html) object or a type supported by it (e.g. int, double, std::string,). In case the property does not exist, or its value is different, or it is removed, the state of the node is set to modified.

------------------------------------------------------------------------

Macros Documentation
--------------------

    OPENMA_DECLARE_NODEID  ( derivedclass ,  baseclass  )

Define the public method [isCastable()](#1a8224478a527b0e01620ec44f5b165d78) used to determine if the object can be cast to the given type.

Note: This macro must be included by every inheriting [](classma_1_1_node.html) classes to be correctly recognised as suche. For example, the function node\_cast() needs the use of this macro to correctly work. :

------------------------------------------------------------------------

    OPENMA_DECLARE_STATIC_PROPERTIES_BASE  ( class ,  ...  )

Add a private StaticProperties structure and the methods staticProperty() and setStaticProperty(). The classes that can use this macro may need to derive of the class [ma::Node](classma_1_1_node.html) (or any inheriting class) but its private implementation must be a based one.

See also [Property](structma_1_1_property.html)

------------------------------------------------------------------------

    OPENMA_DECLARE_STATIC_PROPERTIES_DERIVED  ( derivedclass ,  baseclass ,  ...  )

Add a private StaticProperties structure and the methods staticProperty() and setStaticProperty(). Compared to the macro [OPENMA\_DECLARE\_STATIC\_PROPERTIES\_BASE()](#1a84ad3cb099b81c2c8e5c6776971e1a10), this one is for derived private implementation.

See also [Property](structma_1_1_property.html)

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


