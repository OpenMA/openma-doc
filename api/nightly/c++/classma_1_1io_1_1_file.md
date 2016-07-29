[**](https://github.com/openma/openma-doc/edit/api/nightly/c++/classma_1_1io_1_1_file.md "Improve this documentation")
ma::io::File
============

[Device](classma_1_1io_1_1_device.html) to read/write data from/to a file.

Detailed Description
--------------------

Internally this class uses automatically a buffer mapped into computer's memory (see [https://en.wikipedia.org/wiki/Memory-mapped\_file](https://en.wikipedia.org/wiki/Memory-mapped_file.html)).

Warning: Currently the Mode Append has no effect on this device.

Member Function Documentation
-----------------------------

    void ma::io::File::close ( ) [virtual]

The use of this method without any file associated will set the [State::Fail](classma_1_1io_1_1_device.html#1ac8945a81e16b04ee2a4a349f7241b17baceaa0734f0b3c738120c67344d8f3ec1) to true.

------------------------------------------------------------------------

    const  char * ma::io::File::data ( ) const noexcept [virtual]

Return the data mapped in the memory

------------------------------------------------------------------------

    ma::io::File::File ( )

Default constructor. You must use the method Open after the use of this constructor

------------------------------------------------------------------------

    bool ma::io::File::isOpen ( ) const noexcept [virtual]

Returns true if a file was successfuly opened, otherwise false.

------------------------------------------------------------------------

    bool ma::io::File::isSequential ( ) const noexcept [virtual]

Returns false as the [File](classma_1_1io_1_1_file.html) class represents a random access device.

------------------------------------------------------------------------

    void ma::io::File::open ( const  char *  filename ,  Mode  mode )

Open the given *filename* with the specified *mode*.

Note: To open a file, the device has to be first closed if a previous file was already opened. :

------------------------------------------------------------------------

    Size ma::io::File::peek ( char *  s ,  Size  n ) const [virtual]

Similar to the [read()](#1a761af5faae79014836abb612b6730be4) method but does not modify the position of the read indicator. Returns the number of characters read. No exception or error flag is triggered when an error occurs.

------------------------------------------------------------------------

    void ma::io::File::read ( char *  s ,  Size  n ) [virtual]

Gets from the device a sequence of characters of size *n* and store it in *s*. The [State::Fail](classma_1_1io_1_1_device.html#1ac8945a81e16b04ee2a4a349f7241b17baceaa0734f0b3c738120c67344d8f3ec1) state flag is set if any issue happens during the reading operation. In case the number or characters read does not correspond to the number of characters to read *n*, the State::End state flag is also set.

------------------------------------------------------------------------

    void ma::io::File::seek ( Offset  offset ,  Origin  whence ) [virtual]

Moves the internal pointer of the given *offset* in the given direction *dir*.

------------------------------------------------------------------------

    Size ma::io::File::size ( ) const noexcept [virtual]

Return the size of the data mapped in the memory

------------------------------------------------------------------------

    Position ma::io::File::tell ( ) const noexcept [virtual]

Returns the position of the internal pointer.

------------------------------------------------------------------------

    void ma::io::File::write ( const  char *  s ,  Size  n ) [virtual]

Puts the sequence of characters *s* of size *n* to the device. The [State::Error](classma_1_1io_1_1_device.html#1ac8945a81e16b04ee2a4a349f7241b17ba902b0d55fddef6f8d651fe1035b7d4bd) state flag is set if any issue happens during the wrting operation. In case you attempt to write on the device while it is open in read-only mode, the [State::Fail](classma_1_1io_1_1_device.html#1ac8945a81e16b04ee2a4a349f7241b17baceaa0734f0b3c738120c67344d8f3ec1) state flag will be set.

------------------------------------------------------------------------

    ma::io::File::~File ( ) noexcept

Destructor (default).

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


