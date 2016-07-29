ma::io::Buffer
==============

[Device](classma_1_1io_1_1_device.html) to read/write data from/to a file.

Detailed Description
--------------------

Internally this class uses automatically a buffer mapped into computer's memory (see [https://en.wikipedia.org/wiki/Memory-mapped\_file](https://en.wikipedia.org/wiki/Memory-mapped_file.html)).

Warning: Currently the Mode Append has no effect on this device.

Member Function Documentation
-----------------------------

    ma::io::Buffer::Buffer ( )

Default constructor. You must use the method Open after the use of this constructor

------------------------------------------------------------------------

    const  std::vector< size_t >  & ma::io::Buffer::chunkIDs ( ) const noexcept

Returns the ID associated with each chunk. This could be usefull in case the buffer is not contigous but by part.

------------------------------------------------------------------------

    size_t ma::io::Buffer::chunkSize ( ) const noexcept

Returns the size for each chunk

------------------------------------------------------------------------

    void ma::io::Buffer::close ( ) [virtual]

The use of this method without any file associated will set the [State::Fail](classma_1_1io_1_1_device.html#1ac8945a81e16b04ee2a4a349f7241b17baceaa0734f0b3c738120c67344d8f3ec1) to true.

------------------------------------------------------------------------

    const  char * ma::io::Buffer::data ( ) const noexcept [virtual]

Return the data mapped in the memory

------------------------------------------------------------------------

    bool ma::io::Buffer::isOpen ( ) const noexcept [virtual]

Returns true if a file was successfuly opened, otherwise false.

------------------------------------------------------------------------

    bool ma::io::Buffer::isSequential ( ) const noexcept [virtual]

Returns false as the [Buffer](classma_1_1io_1_1_buffer.html) class represents a random access device.

------------------------------------------------------------------------

    void ma::io::Buffer::open ( const  char *  data ,  size_t  dataSize ,  bool  owned  = false )

Convenient method to open a buffer in read-inly mode. If *owned* is set to true, the *data* will be deleted by the destructor of the buffer.

------------------------------------------------------------------------

    void ma::io::Buffer::open ( char *  data ,  size_t  dataSize ,  Mode  mode  =  ,  bool  owned  = false )

Open a buffer with the given *mode* based on a contigous array of data. If *owned* is set to true, the *data* will be deleted by the destructor of the buffer.

------------------------------------------------------------------------

    void ma::io::Buffer::open ( char *  data ,  size_t  dataSize ,  const  std::vector< size_t >  &  chunkIds ,  size_t  chunkSize ,  Mode  mode  =  ,  bool  owned  = false )

Open a buffer with the given *mode* based on a set of chunks (i.e. non-contigous array of data) If *owned* is set to true, the *data* will be deleted by the destructor of the buffer.

------------------------------------------------------------------------

    Size ma::io::Buffer::peek ( char *  s ,  Size  n ) const [virtual]

Similar to the [read()](#1a88b1ccbe8c915a4f795b4752a49ca3e5) method but does not modify the position of the read indicator. Returns the number of characters read. No exception or error flag is triggered when an error occurs.

------------------------------------------------------------------------

    void ma::io::Buffer::read ( char *  s ,  Size  n ) [virtual]

Gets from the device a sequence of characters of size *n* and store it in *s*. The [State::Fail](classma_1_1io_1_1_device.html#1ac8945a81e16b04ee2a4a349f7241b17baceaa0734f0b3c738120c67344d8f3ec1) state flag is set if any issue happens during the reading operation. In case the number or characters read does not correspond to the number of characters to read *n*, the State::End state flag is also set.

------------------------------------------------------------------------

    void ma::io::Buffer::seek ( Offset  offset ,  Origin  whence ) [virtual]

Moves the internal pointer of the given *offset* in the given direction *dir*.

------------------------------------------------------------------------

    void ma::io::Buffer::setChunks ( const  std::vector< size_t >  &  ids ,  size_t  size )

Sets the chunks.

Note: Because this method resets the content of the internal buffer, it resets also the position of the internal pointer to the beginning. :

------------------------------------------------------------------------

    Size ma::io::Buffer::size ( ) const noexcept [virtual]

Return the size of the data in the buffer

------------------------------------------------------------------------

    Position ma::io::Buffer::tell ( ) const noexcept [virtual]

Returns the position of the internal pointer.

------------------------------------------------------------------------

    void ma::io::Buffer::write ( const  char *  s ,  Size  n ) [virtual]

Puts the sequence of characters *s* of size *n* to the device. The [State::Error](classma_1_1io_1_1_device.html#1ac8945a81e16b04ee2a4a349f7241b17ba902b0d55fddef6f8d651fe1035b7d4bd) state flag is set if any issue happens during the wrting operation. In case you attempt to write on the device while it is open in read-only mode, the [State::Fail](classma_1_1io_1_1_device.html#1ac8945a81e16b04ee2a4a349f7241b17baceaa0734f0b3c738120c67344d8f3ec1) state flag will be set.

------------------------------------------------------------------------

    ma::io::Buffer::~Buffer ( ) noexcept

Destructor (default).

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


