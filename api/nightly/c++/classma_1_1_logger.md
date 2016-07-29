ma::Logger
==========

Class to centralize log messages and write them to a device.

Detailed Description
--------------------

Three categories are available and could be used as proposed below:

-   Message::Info: For users' information or debugging
-   Message::Warning: For incorrect inputs in algorithms but still adatable.
-   Message::Error: For undesired behaviour which can break algorithms' logic.

Each logging category has a dedicated static function:

-   info()
-   warning()
-   error()

These functions send the given message to a [Logger::Device](structma_1_1_logger_1_1_device.html) set. This device has the role to write the message (in a console, a file, etc.). By default, the message are sent into the standard cout/cerr streams. To set a device, you have to use the method [Logger::setDevice()](#1af2bf97e0045e1e5aaf00ef37fabf5e9b)

To disable the logger, you can use the method logger::mute().

Member Function Documentation
-----------------------------

    ma::Logger::~Logger ( ) noexcept

Destructor Delete the set device

------------------------------------------------------------------------

    Logger  & ma::Logger::instance ( ) [static]

Singleton

------------------------------------------------------------------------

    void ma::Logger::mute ( bool  active ) noexcept [static]

Active/unactive the logger. If the logger is set to mute, all the messages are eaten and destroyed.

------------------------------------------------------------------------

    void ma::Logger::prepareAndSendMessage ( Message  category ,  const  char *  msg ,  ... )

Send a message to the set device. If no device is set, a default one is created and send info messages to the std::cout stream and warning and error messages to the std::cerr stream. You can set a device using the method [Logger::setDevice()](#1af2bf97e0045e1e5aaf00ef37fabf5e9b).

Compared to the method [Logger::sendMessage()](#1a4477b48dce6c069438f60a1210c7de6a), this method creates also a string based on the given variadic arguments.

------------------------------------------------------------------------

    void ma::Logger::sendMessage ( Message  category ,  const  char *  msg )

Send a message to the set device. If no device is set, a default one is created and send info messages to the std::cout stream and warning and error messages to the std::cerr stream. You can set a device using the method [Logger::setDevice()](#1af2bf97e0045e1e5aaf00ef37fabf5e9b).

------------------------------------------------------------------------

    void ma::Logger::setDevice ( Device  *  output ) noexcept [static]

Set the device which will write the log messages. If a previous device was set, it will be deleted. The logger takes the ownership of the device.

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


