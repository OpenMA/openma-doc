[**](https://github.com/openma/openma-doc/edit/api/nightly/c++/classma_1_1_event.md "Improve this documentation")
ma::Event
=========

Label a specific time.

Detailed Description
--------------------

An event is defined by:

-   a *name*;
-   a *time* (in seconds);
-   a *context* (e.g. "Right" side, "Left" side, or "General" context);
-   a *subject* associated with this event
-   a *description* which could give more details about the event

All these information can be accessed/modified by using dedicated accessor/mutator but also using the [property()](classma_1_1_node.html#1aa43a4b4b0844ea2d7d6207f89bf2a790) and [setProperty()](classma_1_1_node.html#1ac22e4aa3baa9ed33b887109922eba172) methods.

A time can be positive, null, or negative. The null time indicates the start of the recording, while a negative and postive time corresponds to an event before and after the beginning of the recording, respectively.

There is no standard for the definition of a context. However, it is common to use the following context for task analysis:

-   *Right:* Events associated with the right side of the (human) body
-   *Left:* Events associated with the left side of the (human) body
-   *General:* Other events that cannot be assigned to the left or the right side of the body

The role of the context may be important or not depending of your later data processing/analysis. For example, inside a clinical gait analysis you can have several "Foot Strike" and "Foot Off" events assigned to the "Right" and "Left" sides. You could want to retrieve the events by name or by context or both. Thus, choosing a common orthography could help you as well as other researchers. The previous example could be implemented like in the following code. The important thing to remind is the case used for any string assigned (name, context, subject, ...)

    // Several events are defined in the node "Events".
    // A algorithm could have generated the following events
    ma::Node* events = new ma::Node("Events");
    new ma::Event("Foot Strike",1.3,"Right","JDoe",&events);
    new ma::Event("Foot Off",2.4,"Right","JDoe",&events);
    new ma::Event("Foot Strike",1.8,"Left","JDoe",&events);
    new ma::Event("Foot Off",3.0,"Left","JDoe",&events);
    // Later in the code, you could retrive only:
    // Events with the context "Right"
    std::list rightEvents = events.findChild({},{{"context","Right"}});
    // Events with the name "Foot Strike"
    std::list footStrikeEvents = events.findChild("Foot Strike");

The subject's identification is used to distinguish events between subject which are in the same trial (if any).

Properties Documentation
------------------------

    context :  std::string 

This property holds the context (or side) associated with the [Event](classma_1_1_event.html). By default, this property contains an empty string.

See also [context()](#1afd4a09552410578ed4b1b53186e75a69), [setContext()](#1acac4cdec15afc07a4731045c6f84eac7)

------------------------------------------------------------------------

    subject :  std::string 

This property holds the subject identification associated with the [Event](classma_1_1_event.html). By default, this property contains an empty string.

See also [subject()](#1a9462f85b505808a335e9578381dafe24), [setSubject()](#1a9038a2255876d2399445a61d0840cb0c)

------------------------------------------------------------------------

    time :  double 

This property holds the time (in second) associated with the [Event](classma_1_1_event.html). By default, this property is set to 0.0.

See also [time()](#1a91a3ba88daf4b237e1a43c7e1e04878c), [setTime()](#1a5683c038aad32210b70a8772ac01f4c7)

------------------------------------------------------------------------

Member Function Documentation
-----------------------------

    ma::Event::Event ( const  std::string  &  name ,  double  time  = 0.0 ,  const  std::string  &  context  = std::string{} ,  const  std::string  &  subject  = std::string{} ,  Node  *  parent  = nullptr )

Constructor.

------------------------------------------------------------------------

    ma::Event::~Event ( ) noexcept

Destructor (default)

------------------------------------------------------------------------

    Event  * ma::Event::clone ( Node  *  parent  = nullptr ) const [virtual]

Create a deep copy of the object and return it as another object.

Note: Each subclass must override this method to correctly do the deep copy. :

------------------------------------------------------------------------

    const  std::string  & ma::Event::context ( ) const noexcept

Returns the context associated with this event. There is no standard for the definition of a context. However, it is common to use the following context for task analysis:

-   *Right:* Events associated with the right side of the (human) body
-   *Left:* Events associated with the left side of the (human) body
-   *General:* Other events which cannot be assigned to the left or the right side of the body

------------------------------------------------------------------------

    void ma::Event::copy ( const  Event  *  src ) noexcept

Do a deep copy of the the given *src*. The previous content is replaced.

Note: Each subclass must override this method to correctly do the deep copy. :

Note: This method does not copy the parent. If you need to copy the parent, you must use the method [](classma_1_1_node.html#1a9f6c38a01fa8921ca83fb3d129d4accd) afterwards. See the example in the desctription of the [](classma_1_1_node.html#1a1a4275e23c0ea7a1cae9d4f65a38938f) method. :

------------------------------------------------------------------------

    void ma::Event::setContext ( const  std::string  &  value ) noexcept

Sets the context associated with this event. There is no standard for the definition of a context. However, it is common to use the following context for task analysis:

-   *Right:* Events associated with the right side of the (human) body
-   *Left:* Events associated with the left side of the (human) body
-   *General:* Other events which cannot be assigned to the left or the right side of the body

------------------------------------------------------------------------

    void ma::Event::setSubject ( const  std::string  &  value ) noexcept

Sets the subject's identification.

------------------------------------------------------------------------

    void ma::Event::setTime ( double  value ) noexcept

Sets the time associated with an event. The time can be positive, null, or negative. The null time indicates the start of the recording, while a negative and postive time corresponds to an event before and after the beginning of the recording, respectively.

------------------------------------------------------------------------

    const  std::string  & ma::Event::subject ( ) const noexcept

Return the subject's identification.

------------------------------------------------------------------------

    double ma::Event::time ( ) const noexcept

Returns the time associated with this event. The time can be positive, null, or negative. The null time indicates the start of the recording, while a negative and postive time corresponds to an event before and after the beginning of the recording, respectively.

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


