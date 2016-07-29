ma::io::Handler
===============

To read/write data from/to an I/O device in a specific format.

Detailed Description
--------------------

This interface is the core to implement data reader/writer (e.g. trials, models). Several methods and mecanisms are already implemented to facilitate the inclusion of new formats. For example, it is not necessary to manage exception as this is done internaly. Some methods are available to set errors and retrieve them. The extraction of handler's class is implemented. In fact, only four (or five) methods must be implemented for inherting handler:

-   [readDevice()](#1ac9cd15b0885211499ba42c44666907ac) method: extract data from a device and set it into a node
-   [writeDevice()](#1aa604e4c01b0e437c827abbf4fea1147f) method: write data to a given device
-   [validateSignature()](#1a37f57241f601dcc9738dd33b3bd25ca2) method: test if the read device has a signature valid for this handler.
-   [canRead()](#1ad95d7cd526fee3adc981d30a400b0946) method: to inform on the capability of the handler to read data from a device
-   [canWrite()](#1a008895dc4ee6fbf6cf2612ee280f4a23) method: to inform on the capability of the handler to write data to a device

Todo
Give an example for the implementation of a handler.

Member Function Documentation
-----------------------------

    bool ma::io::Handler::canRead ( ) const noexcept [virtual]

Returns the capability of the handler to read data from a device. By default this method returns false.

------------------------------------------------------------------------

    bool ma::io::Handler::canWrite ( ) const noexcept [virtual]

Returns the capability of the handler to write data to a device. By default this method returns false.

------------------------------------------------------------------------

    Signature ma::io::Handler::detectSignature ( ) const noexcept

Try to detect the signature of the handler in the given device. A signature is generaly a keyword at the beginning of the data that help to determine the content. For example, if the device is a [File](classma_1_1io_1_1_file.html), this way is safer than relying on the file extension. Internaly this methods use [validateSignature()](#1a37f57241f601dcc9738dd33b3bd25ca2). Each inheriting handler must overload the method [validateSignature()](#1a37f57241f601dcc9738dd33b3bd25ca2).

------------------------------------------------------------------------

    Device  * ma::io::Handler::device ( ) const noexcept

Returns the current device associated with this handler.

------------------------------------------------------------------------

    Error ma::io::Handler::errorCode ( ) const noexcept

Returns the current error code.

------------------------------------------------------------------------

    const  std::string  & ma::io::Handler::errorMessage ( ) const noexcept

Returns the current error message.

------------------------------------------------------------------------

    ma::io::Handler::Handler ( HandlerPrivate  &  pimpl ) noexcept

Constructor for inheriting class with extended private implementation

------------------------------------------------------------------------

    bool ma::io::Handler::read ( Node  *  output )

Read the content of the current set device and fill the given *output*. If an exception is thrown during the reading of the device, no content is added to the output and false is returned. In case this method returns false, you can use the methods [errorCode()](#1ab177d58175b643e9481cfb3ed43da5bb) and [errorMessage()](#1a7c7252a391e1aa99f58e8c29c13385d9) to retrieve the error. Internally this methods call [readDevice()](#1ac9cd15b0885211499ba42c44666907ac) to extract data. Each inheriting handler must overload the method [readDevice()](#1ac9cd15b0885211499ba42c44666907ac).

------------------------------------------------------------------------

    void ma::io::Handler::readDevice ( Node  *  output ) [virtual]

Method to overload to read data from the current set device.

------------------------------------------------------------------------

    void ma::io::Handler::setDevice ( Device  *  device ) noexcept

Sets the current device associated with this handler.

------------------------------------------------------------------------

    void ma::io::Handler::setError ( Error  code  = Error::None ,  const  std::string  &  msg  = "" ) noexcept

Set a code and a detailed message for an error which happened during the reading or writing of a device.

------------------------------------------------------------------------

    Signature ma::io::Handler::validateSignature ( ) const noexcept [virtual]

Method to overload to determine if the associated device is compatible with the handler.

------------------------------------------------------------------------

    bool ma::io::Handler::write ( const  Node  *  input )

Write the content of the *input* to the current set device. If an exception is thrown during the writing of the device, false is returned. In case this method returns false, you can use the methods [errorCode()](#1ab177d58175b643e9481cfb3ed43da5bb) and [errorMessage()](#1a7c7252a391e1aa99f58e8c29c13385d9) to retrieve the error. Internally this methods call [writeDevice()](#1aa604e4c01b0e437c827abbf4fea1147f) to extract data. Each inheriting handler must overload the method [writeDevice()](#1aa604e4c01b0e437c827abbf4fea1147f).

------------------------------------------------------------------------

    void ma::io::Handler::writeDevice ( const  Node  *  input ) [virtual]

Method to overload to write data to the current set device.

------------------------------------------------------------------------

    ma::io::Handler::~Handler ( ) noexcept [virtual]

Destructor (default)

------------------------------------------------------------------------

Related Non-Members Documentation
---------------------------------

    constexpr  Capability ma::io::Handler::operator& ( Capability  lhs ,  Capability  rhs ) [inline]

Bitwise and operator for Capability

------------------------------------------------------------------------

    constexpr  Capability ma::io::Handler::operator| ( Capability  lhs ,  Capability  rhs ) [inline]

Bitwise or operator for Capability

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


