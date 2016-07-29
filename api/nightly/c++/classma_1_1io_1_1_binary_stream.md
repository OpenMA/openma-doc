ma::io::BinaryStream
====================

Read/write binary data from any [Device](classma_1_1io_1_1_device.html).

Detailed Description
--------------------

Be sure that the lifetime of the device is longer than the stream. There is no check inside the stream to verify the existence of the device.

Member Function Documentation
-----------------------------

    ma::io::BinaryStream::BinaryStream ( Device  *  device  = 0 )

Constructor which uses the native byte order format (Endianness) of the current machine. In case no device is given, you must use the method [setDevice()](#1af88be18cb77327a787e6e3e2c309e370), otherwise the stream will try to read/write data from/to a null device.

------------------------------------------------------------------------

    ma::io::BinaryStream::BinaryStream ( Device  *  device ,  ByteOrder  format )

Constructor which uses the given endian format and return extracted values adapted to the endiannes of the machine.

------------------------------------------------------------------------

    ByteOrder ma::io::BinaryStream::byteOrder ( ) const noexcept

Return the endian format used by the stream.

------------------------------------------------------------------------

    Device  * ma::io::BinaryStream::device ( ) const noexcept

Returns the device associated to this stream.

------------------------------------------------------------------------

    char ma::io::BinaryStream::readChar ( )

Extracts one character from the stream.

------------------------------------------------------------------------

    void ma::io::BinaryStream::readChar ( size_t  n ,  char *  values )

Extracts *n* characters and assign them into the array *values*.

Note: The array ** must be already created with at least ** elements allocated; :

------------------------------------------------------------------------

    double ma::io::BinaryStream::readDouble ( )

Extracts one double.

------------------------------------------------------------------------

    void ma::io::BinaryStream::readDouble ( size_t  n ,  double *  values )

Extracts *n* doubles and assign them into the array *values*.

Note: The array ** must be already created with at least ** elements allocated; :

------------------------------------------------------------------------

    float ma::io::BinaryStream::readFloat ( )

Extracts one float.

------------------------------------------------------------------------

    void ma::io::BinaryStream::readFloat ( size_t  n ,  float *  values )

Extracts *n* floats and assign them into the array *values*.

Note: The array ** must be already created with at least ** elements allocated; :

------------------------------------------------------------------------

    int16_t ma::io::BinaryStream::readI16 ( )

Extracts one signed 16-bit integer.

------------------------------------------------------------------------

    void ma::io::BinaryStream::readI16 ( size_t  n ,  int16_t *  values )

Extracts *n* signed 16-bit integers and assign them into the array *values*.

Note: The array ** must be already created with at least ** elements allocated; :

------------------------------------------------------------------------

    int32_t ma::io::BinaryStream::readI32 ( )

Extracts one signed 32-bit integer.

------------------------------------------------------------------------

    void ma::io::BinaryStream::readI32 ( size_t  n ,  int32_t *  values )

Extracts *n* signed 32-bit integers and assign them into the array *values*.

Note: The array ** must be already created with at least ** elements allocated; :

------------------------------------------------------------------------

    int64_t ma::io::BinaryStream::readI64 ( )

Extracts one signed 64-bit integer.

------------------------------------------------------------------------

    void ma::io::BinaryStream::readI64 ( size_t  n ,  int64_t *  values )

Extracts *n* signed 64-bit integers and assign them into the array *values*.

Note: The array ** must be already created with at least ** elements allocated; :

------------------------------------------------------------------------

    int8_t ma::io::BinaryStream::readI8 ( )

Extracts one signed 8-bit integer.

------------------------------------------------------------------------

    void ma::io::BinaryStream::readI8 ( size_t  n ,  int8_t *  values )

Extracts *n* signed 8-bit integers and assign them into the array *values*.

Note: The array ** must be already created with at least ** elements allocated; :

------------------------------------------------------------------------

    std::string ma::io::BinaryStream::readString ( size_t  len )

Extracts one string.

------------------------------------------------------------------------

    void ma::io::BinaryStream::readString ( size_t  len ,  size_t  n ,  std::string *  values )

Extracts *n* unsigned 8-bit integers and assign them into the array *values*.

Note: The array ** must be already created with at least ** elements allocated; :

------------------------------------------------------------------------

    uint16_t ma::io::BinaryStream::readU16 ( )

Extracts one unsigned 16-bit integer.

------------------------------------------------------------------------

    void ma::io::BinaryStream::readU16 ( size_t  n ,  uint16_t *  values )

Extracts *n* unsigned 16-bit integers and assign them into the array *values*.

Note: The array ** must be already created with at least ** elements allocated; :

------------------------------------------------------------------------

    uint32_t ma::io::BinaryStream::readU32 ( )

Extracts one unsigned 32-bit integer.

------------------------------------------------------------------------

    void ma::io::BinaryStream::readU32 ( size_t  n ,  uint32_t *  values )

Extracts *n* unsigned 32-bit integers and assign them into the array *values*.

Note: The array ** must be already created with at least ** elements allocated; :

------------------------------------------------------------------------

    uint64_t ma::io::BinaryStream::readU64 ( )

Extracts one unsigned 64-bit integer.

------------------------------------------------------------------------

    void ma::io::BinaryStream::readU64 ( size_t  n ,  uint64_t *  values )

Extracts *n* unsigned 64-bit integers and assign them into the array *values*.

Note: The array ** must be already created with at least ** elements allocated; :

------------------------------------------------------------------------

    uint8_t ma::io::BinaryStream::readU8 ( )

Extracts one unsigned 8-bit integer.

------------------------------------------------------------------------

    void ma::io::BinaryStream::readU8 ( size_t  n ,  uint8_t *  values )

Extracts *n* unsigned 8-bit integers and assign them into the array *values*.

Note: The array ** must be already created with at least ** elements allocated; :

------------------------------------------------------------------------

    void ma::io::BinaryStream::setByteOrder ( ByteOrder  format )

Sets the endian format used by the stream.

Note: You can use the enum value ByteOrder::NotApplicable. This deletes the format and set it to null. However, it is not recommended to do that as the stream would crash when trying to read/write data from/to a device. :

------------------------------------------------------------------------

    void ma::io::BinaryStream::setDevice ( Device  *  device ) noexcept

Sets the device associated to this stream. Trying to assign a null device will print an error message and returns.

------------------------------------------------------------------------

    size_t ma::io::BinaryStream::writeChar ( char  value )

Writes the character *value* in the stream an return its size.

------------------------------------------------------------------------

    size_t ma::io::BinaryStream::writeChar ( size_t  n ,  const  char *  values )

Writes the array of characters *values* in the stream an return its size.

Note: The array ** must contain at least ** elements initialized; :

------------------------------------------------------------------------

    size_t ma::io::BinaryStream::writeFloat ( float  value )

Writes the float *f* in the stream an return its size.

------------------------------------------------------------------------

    size_t ma::io::BinaryStream::writeFloat ( size_t  n ,  const  float *  values )

Writes the array of floats *values* in the stream an return its size.

Note: The array ** must contain at least ** elements initialized; :

------------------------------------------------------------------------

    size_t ma::io::BinaryStream::writeI16 ( int16_t  value )

Writes the signed 16-bit integer *i16* in the stream an return its size.

------------------------------------------------------------------------

    size_t ma::io::BinaryStream::writeI16 ( size_t  n ,  const  int16_t *  values )

Writes the array of signed 16-bit integers *values* in the stream an return its size.

Note: The array ** must contain at least ** elements initialized; :

------------------------------------------------------------------------

    size_t ma::io::BinaryStream::writeI32 ( int32_t  value )

Write the 32-bit signed integer *i32* and return its size.

------------------------------------------------------------------------

    size_t ma::io::BinaryStream::writeI32 ( size_t  n ,  const  int32_t *  values )

Writes the array of signed 32-bit integers *values* in the stream an return its size.

Note: The array ** must contain at least ** elements initialized; :

------------------------------------------------------------------------

    size_t ma::io::BinaryStream::writeI8 ( int8_t  value )

Writes the signed 8-bit integer *value* in the stream an return its size.

------------------------------------------------------------------------

    size_t ma::io::BinaryStream::writeI8 ( size_t  n ,  const  int8_t *  values )

Writes the array of signed 8-bit integers *values* in the stream an return its size.

Note: The array ** must contain at least ** elements initialized; :

------------------------------------------------------------------------

    size_t ma::io::BinaryStream::writeString ( const  std::string  &  value )

Writes the string *rString* in the stream an return its size.

------------------------------------------------------------------------

    size_t ma::io::BinaryStream::writeString ( size_t  n ,  const  std::string *  values )

Writes the array of strings *values* in the stream an return its size.

Note: The array ** must contain at least ** elements initialized; :

------------------------------------------------------------------------

    size_t ma::io::BinaryStream::writeU16 ( uint16_t  value )

Writes the unsigned 16-bit integer *u16* in the stream an return its size.

------------------------------------------------------------------------

    size_t ma::io::BinaryStream::writeU16 ( size_t  n ,  const  uint16_t *  values )

Writes the array of unsigned 16-bit integers *values* in the stream an return its size.

Note: The array ** must contain at least ** elements initialized; :

------------------------------------------------------------------------

    size_t ma::io::BinaryStream::writeU32 ( uint32_t  value )

Write the 32-bit unsigned integer *u32* and return its size

------------------------------------------------------------------------

    size_t ma::io::BinaryStream::writeU32 ( size_t  n ,  const  uint32_t *  values )

Writes the array of unsigned 32-bit integers *values* in the stream an return its size.

Note: The array ** must contain at least ** elements initialized; :

------------------------------------------------------------------------

    size_t ma::io::BinaryStream::writeU8 ( uint8_t  value )

Writes the unsigned 8-bit integer *value* in the stream an return its size.

------------------------------------------------------------------------

    size_t ma::io::BinaryStream::writeU8 ( size_t  n ,  const  uint8_t *  values )

Writes the array of unsigned 8-bit integers *values* in the stream an return its size.

Note: The array ** must contain at least ** elements initialized; :

------------------------------------------------------------------------

    ma::io::BinaryStream::~BinaryStream ( ) noexcept

Destructor. Delete the endian format associated with the stream

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


