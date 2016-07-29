ma::io::Device
==============

Interface to read and write on any type of device (e.g. [File](classma_1_1io_1_1_file.html), [Buffer](classma_1_1io_1_1_buffer.html), etc.).

Detailed Description
--------------------

There is two types of devices. The first one is called "random access" (e.g. [File](classma_1_1io_1_1_file.html), [Buffer](classma_1_1io_1_1_buffer.html)), while the second is called "sequential" (e.g. SerialPort). The use of a [Device](classma_1_1io_1_1_device.html) class should be used with a [BinaryStream](classma_1_1io_1_1_binary_stream.html) or TextStream which interact at a higher level to read/write data in a device.

This interface proposes also an exception mechanism in case the device fails to do some internal operation, or if there are error during I/O operations. You can use the method [setExceptions()](#1a23441c5b9b121601d9636f5a4602cd17) to set the states which can trigger an exception. The exception thrown by this class corresponds to a [Device::Failure](classma_1_1io_1_1_device_1_1_failure.html) exception.

To implement a new device, several methods must me implemented. To facilitate this implementation some protected methods are proposed like [verifyMode()](#1a37b55981900db31f57f893d2c3f2f251).

Member Type Documentation
-------------------------

    ma::io::Device::Mode

Details on the way to use the device.

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Constant</th>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>In</td>
<td>= 0x01</td>
<td><p>Use the device to read data from it.</p></td>
</tr>
<tr class="even">
<td>Out</td>
<td>= 0x02</td>
<td><p>Use the device to write data from it.</p></td>
</tr>
<tr class="odd">
<td>Append</td>
<td>= 0x04</td>
<td><p>Set the internal pointer used by the device at the end.</p></td>
</tr>
<tr class="even">
<td>Truncate</td>
<td>= 0x08</td>
<td><p>Erase the content of the device.</p></td>
</tr>
<tr class="odd">
<td>End</td>
<td>= 0x10</td>
<td><p>Set the internal pointer used by the device at the begining.</p>
<p>Start at the end of the internal buffer.</p>
<p>The device is at the end of its internal buffer.</p></td>
</tr>
</tbody>
</table>

------------------------------------------------------------------------

    ma::io::Device::Offset

Numerical type used to shift the position of the internal buffer pointer.

------------------------------------------------------------------------

    ma::io::Device::Origin

Used as anchor for the [seek()](classma_1_1io_1_1_device.html#1aa4b7fc5d53de4e9552bbbcc87cedd8dc) method.

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Constant</th>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Begin</td>
<td></td>
<td><p>Start at the beginning of the internal buffer.</p></td>
</tr>
<tr class="even">
<td>Current</td>
<td></td>
<td><p>Start at the current position in the internal buffer.</p></td>
</tr>
<tr class="odd">
<td>End</td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

------------------------------------------------------------------------

    ma::io::Device::Position

Numerical type used to inform on the position of internal buffer pointer.

------------------------------------------------------------------------

    ma::io::Device::Size

Numerical type used for the size of the internal buffer.

------------------------------------------------------------------------

    ma::io::Device::State

Internal state of the device. This

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Constant</th>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>End</td>
<td>= 0x01</td>
<td></td>
</tr>
<tr class="even">
<td>Fail</td>
<td>= 0x02</td>
<td><p>A failure happened within the device.</p></td>
</tr>
<tr class="odd">
<td>Error</td>
<td>= 0x04</td>
<td><p>An unexpected error happened within the device.</p></td>
</tr>
<tr class="even">
<td>Good</td>
<td>= 0x00</td>
<td><p>Everything is fine!</p></td>
</tr>
</tbody>
</table>

------------------------------------------------------------------------

Member Function Documentation
-----------------------------

    bool ma::io::Device::atEnd ( ) const noexcept

Returns true if the device's state contain the flag State::End.

------------------------------------------------------------------------

    void ma::io::Device::clear ( State  state  =  )

Sets the state of the device. If the given state *flags* meets some part of the exception's mask, then a [Failure](classma_1_1io_1_1_device_1_1_failure.html) exception is thrown.

Note: Setting the state to [](#1ac8945a81e16b04ee2a4a349f7241b17ba0c6ad70beb3a7e76c3fc7adab7c46acc) will reset the possible current failure/errors. :

------------------------------------------------------------------------

    void ma::io::Device::close ( ) [virtual]

Close the device.

Note: The inherited class should set the [](#1ac8945a81e16b04ee2a4a349f7241b17baceaa0734f0b3c738120c67344d8f3ec1) state flag if any failure happens during the closing of the device. :

------------------------------------------------------------------------

    const  char * ma::io::Device::data ( ) const noexcept [virtual]

Returns a pointer to the first byte stored in the device (or null if it is not possible to access to the data).

Note: The use of this method with a sequential device would set the flag [](#1ac8945a81e16b04ee2a4a349f7241b17baceaa0734f0b3c738120c67344d8f3ec1) to true. At least the output would be null. :

------------------------------------------------------------------------

    ma::io::Device::Device ( ) noexcept

Constructor. Set the device's state to [State::Good](#1ac8945a81e16b04ee2a4a349f7241b17ba0c6ad70beb3a7e76c3fc7adab7c46acc) without exception enabled.

------------------------------------------------------------------------

    ma::io::Device::Device ( DevicePrivate  &  pimpl ) noexcept

Constructor to be used by inherited device that need extra informations (static properties, members, etc) inside the private implementation.

------------------------------------------------------------------------

    State ma::io::Device::exceptions ( ) noexcept

Returns the mask used to possibly throws an exception.

------------------------------------------------------------------------

    bool ma::io::Device::hasError ( ) const noexcept

Returns true if the device's state contain the flag [State::Fail](#1ac8945a81e16b04ee2a4a349f7241b17baceaa0734f0b3c738120c67344d8f3ec1)

------------------------------------------------------------------------

    bool ma::io::Device::hasFailure ( ) const noexcept

Returns true if the device's state contain the flag [State::Fail](#1ac8945a81e16b04ee2a4a349f7241b17baceaa0734f0b3c738120c67344d8f3ec1) and/or [State::Error](#1ac8945a81e16b04ee2a4a349f7241b17ba902b0d55fddef6f8d651fe1035b7d4bd).

------------------------------------------------------------------------

    bool ma::io::Device::isGood ( ) const noexcept

Returns true if the device's state is set to [State::Good](#1ac8945a81e16b04ee2a4a349f7241b17ba0c6ad70beb3a7e76c3fc7adab7c46acc).

------------------------------------------------------------------------

    bool ma::io::Device::isOpen ( ) const noexcept [virtual]

Returns true if the device is opened otherwise returns false.

------------------------------------------------------------------------

    bool ma::io::Device::isSequential ( ) const noexcept [virtual]

Returns true if the device is sequential otherwise false.

------------------------------------------------------------------------

    const  char * ma::io::Device::name ( ) const noexcept

Returns the name associated with this device. The name of a device can be anything. For example for a file, it could be the full path of the filename read/write. For a serial port, it could be its identifiant. For a databse, it could the adress of the server.

------------------------------------------------------------------------

    Size ma::io::Device::peek ( char *  s ,  Size  n ) const [virtual]

Extract data without modifying the position of the internal pointer

------------------------------------------------------------------------

    void ma::io::Device::read ( char *  s ,  Size  n ) [virtual]

Gets from the device a sequence of characters of size *n* and store it in *s*. The [State::Error](#1ac8945a81e16b04ee2a4a349f7241b17ba902b0d55fddef6f8d651fe1035b7d4bd) state flag is set if any issue happens during the reading operation.

------------------------------------------------------------------------

    void ma::io::Device::seek ( Offset  offset ,  Origin  whence ) [virtual]

Moves the pointer associated with a random access device of the given *offset* in the given direction *dir*.

Note: The use of this method with a sequential device would set the flag [](#1ac8945a81e16b04ee2a4a349f7241b17baceaa0734f0b3c738120c67344d8f3ec1) to true. :

------------------------------------------------------------------------

    void ma::io::Device::setExceptions ( State  mask )

Sets the mask which will be used to throw an exceptions. Setting the mask to [State::Good](#1ac8945a81e16b04ee2a4a349f7241b17ba0c6ad70beb3a7e76c3fc7adab7c46acc) will cancel the use of exception with the device.

------------------------------------------------------------------------

    void ma::io::Device::setName ( const  char *  name  = nullptr )

Sets the name of the device. Internally, this method copy the given array of characters.

------------------------------------------------------------------------

    void ma::io::Device::setState ( State  state )

Sets the state of the device. The given *state* is added to the current state. Use the method Clear() if you want to reset the state of the device.

------------------------------------------------------------------------

    Size ma::io::Device::size ( ) const noexcept [virtual]

Returns the size of the stored data (or -1 in case it is not known)

Note: The use of this method with a sequential device would set the flag [](#1ac8945a81e16b04ee2a4a349f7241b17baceaa0734f0b3c738120c67344d8f3ec1) to true. At least the output would be equal to -1. :

------------------------------------------------------------------------

    State ma::io::Device::state ( ) const noexcept

Returns true current state of the device.

------------------------------------------------------------------------

    Position ma::io::Device::tell ( ) const noexcept [virtual]

Returns the position of the pointer associated with a random access device.

Note: The use of this method with a sequential device would set the flag [](#1ac8945a81e16b04ee2a4a349f7241b17baceaa0734f0b3c738120c67344d8f3ec1) to true. :

------------------------------------------------------------------------

    bool ma::io::Device::verifyMode ( Mode  mode )

Verify the coherency of the given open mode. This method should be used by every inherited class in their Open() method before trying to open the implemented device. Internally, this will set the flag [State::Fail](#1ac8945a81e16b04ee2a4a349f7241b17baceaa0734f0b3c738120c67344d8f3ec1) to true if one of the verification is not valid. The following checks are realized by this method:

-   The device is not already opened.
-   The modes Append and Truncate cannot be set at the same time.
-   The mode Truncate is set but not the mode Out.

------------------------------------------------------------------------

    void ma::io::Device::write ( const  char *  s ,  Size  n ) [virtual]

Puts the sequence of characters *s* of size *n* to the device. The [State::Error](#1ac8945a81e16b04ee2a4a349f7241b17ba902b0d55fddef6f8d651fe1035b7d4bd) state flag is set if any issue happens during the writing operation.

------------------------------------------------------------------------

    ma::io::Device::~Device ( ) noexcept [virtual]

Destructor. This methods does nothing. It is the responsability of the inherited class to decide if their destructor does something specific regarding the state of the device (like closing it).

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


