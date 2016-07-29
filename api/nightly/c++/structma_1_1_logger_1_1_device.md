ma::Logger::Device
==================

Interface class used to write message sent by the logger.

Detailed Description
--------------------

To be effective, the [Logger](classma_1_1_logger.html) class needs a device. This device is used to write log messages.

A default implementation used to print messages on the standard std::cout and std::cerr streams is proposed and correspond to the following lines.

    struct Console : Logger::Device
    {
      virtual void write(Logger::Category category, const char* msg) _OPENMA_NOEXCEPT override
      {
        if (category == Logger::Info)
          std::cout << "INFO: " << msg << std::endl;
        else if (category == Logger::Warning)
          std::cout << "WARNING: " << msg << std::endl;
        else if (category == Logger::Error)
          std::cout << "ERROR: " << msg << std::endl;
      }
    };

Only one device can be used at a time. To create your custom device you only need to inherit from the class [Logger::Device](structma_1_1_logger_1_1_device.html) and override the method [Logger::Device::write()](#1abb518c12a3f84184d5635ab5696b7e30). To use this custom device with the logger, you have to use the method Device::setDevice().

Member Function Documentation
-----------------------------

    ma::Logger::Device::Device ( ) noexcept

Default (empty) constructor

------------------------------------------------------------------------

    void ma::Logger::Device::write ( Message  category ,  const  char *  msg ) noexcept [virtual]

The logger seng message to this method. The *category* input specifies if the message is for an information, a warning, or an error. The *msg* input is directly the string given to the functions info(), warning(), or error().

------------------------------------------------------------------------

    ma::Logger::Device::~Device ( ) noexcept [virtual]

Default (empty) destructor

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


