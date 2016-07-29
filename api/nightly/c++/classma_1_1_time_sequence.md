ma::TimeSequence
================

Multidimensional time series container.

Detailed Description
--------------------

There is lots of way to store time series data (i.e. data recorded at a fixed sample rate). In OpenMA, recorded data can be markers' trajectories, analog signals, pressure insole, orientation, pose, etc. For example, for each sample, a trajectory has 3 coordinates and one residual, while for an analog channel, a sample is equal to a single value. Instead of distinguish each kind of data series by several subclasses (and add specific members and methods each time), it was decided to create a multidimensionnal time series container. Combined with static and dynamic propertie (see [Property](structma_1_1_property.html)), this would give the possibility to store any kind of time series (or should be) wit any kind of sample (in terms of dimensions and components).

To go futher, reconstructed data (e.g. acquired by a sterephotogrammetric system) and raw data (e.g. acquired by a digital-to-analog converter: ADC) are stored in the same way. Howver, the former has (at least) a supplementary component to store associated residual. This is the responsability of the developer to add this/these extra components when the [TimeSequence](classma_1_1_time_sequence.html) object is created. To possibliy know if a [TimeSequence](classma_1_1_time_sequence.html) object has residual compoents, the [type()](#1acb8464f3b4a467888aa513b98241d79f) of the object can be tested against the enum value Reconstructed (see the example below). Of course, this methods works only if the given Type use the flag Reconstructed.

    // The following code creates a time sequence:
    // - named LHEE
    // - where each sample has 1 dimension with 4 components (X, Y, Z, residual)
    // - with 1000 samples
    // - sampled at 100.0Hz
    // - starting at 0.0 second of the beginning of the acqusition
    // - typed as a Marker
    // - where the main unit (i.e. for the coordinates) is the millimeter.
    auto marker = ma::TimeSequence("LHEE",4,1000,100.0,0.0,ma::TimeSequence::Marker,"mm");
    // Check if the object stores reconstructed data
    std::cout << marker.type() & ma::TimeSequence::Reconstructed << std::endl;

For ADC data, some members were added to give supplementary information that could be used useful when exporting the [TimeSequence](classma_1_1_time_sequence.html) into a file. You can pass to the constructor 3 ADC parameters: *scale*, *offset*, and *range*. By default, the ADC resolution is not stored as it is assumed that all [TimeSequence](classma_1_1_time_sequence.html) objects use the same converter. However, you could add a dynamic property (e.g. *resolution*) using [setProperty()](classma_1_1_node.html#1ac22e4aa3baa9ed33b887109922eba172) to store this information. In general the file formats proposed in OpenMAto to read/write ADC data use only the three stored ADC parameter (scale, offset, range). You should read their dedicated documentation for more details.

    // The last three arguments are for:
    //  - The ADC scale: 1.0
    //  - The ADC offset: 0.0
    //  - The ADC range: [-10,10]
    auto analog = ma::TimeSequence("RRF",1,10000,1000.0,0.0,ma::TimeSequence::Analog,"V",1.0,0.0,{-10.0,10.0});
    // Store supplementary information
    analog.setProperty("resolution",16);
    // Extract it
    std::cout << analog.property("resolution").cast()

Properties Documentation
------------------------

    samples :  unsigned 

This property holds the number of samples of a Timesequnce. By default, this property is set to 0.

See also [samples()](#1a65f4ec19067fa191d80f25712e6b4f9b) setSamples()

------------------------------------------------------------------------

    sampleRate :  double 

This property holds the sample rate of a Timesequnce. By default, this property is set to 0.

See also [sampleRate()](#1a16af29f738532e0773d6fb642a64934b), [setSampleRate()](#1aeafdc767622bb96dfc3c44de6da8f41b)

------------------------------------------------------------------------

    startTime :  double 

This property holds the start time of a Timesequnce. By default, this property is set to 0.0.

See also [startTime()](#1a7b88703b6155f3b36b696d33ed0a60e1), [setStartTime()](#1a4e65fa7051ccb8f134eee3c90d938100)

------------------------------------------------------------------------

    type :  int 

This property holds the type of a Timesequnce. By default, this property is set to [TimeSequence::Unknown](#1a8e5ba2425b030c3b7726203c1efbdac2a56812a8c085f6970d9505e9e081eca25).

See also [type()](#1acb8464f3b4a467888aa513b98241d79f), [setType()](#1adb5ae37fb7459c7034324dc362e435b3)

------------------------------------------------------------------------

    unit :  std::string 

This property holds the unit of a Timesequnce. By default, this property contains an empty string.

Note: The modification of this property does not influence the data. This is only for information purpose :

See also [unit()](#1a962f685ff880375486384cd8a5e28c37), [setUnit()](#1ae0f719f21d2fe5c0d4b2ce191a97150a)

------------------------------------------------------------------------

    scale :  double 

This property holds the scale of a Timesequnce. By default, this property is set to 1.0.

Note: The modification of this property does not influence the data. This is only for information purpose :

See also [scale()](#1aa57fc84ed194a17e866f1dca2430b45a), [setScale()](#1a4d3d45564d970146b51ecc8d724f408e)

------------------------------------------------------------------------

    offset :  double 

This property holds the offset of a Timesequnce. By default, this property is set to 0.

Note: The modification of this property does not influence the data. This is only for information purpose :

See also [offset()](#1a151f1eb170c0799178e9aabcf84c82db), [setOffset()](#1a103884db670aa45d794adb5a713d8f76)

------------------------------------------------------------------------

    range :  std::array< double, 2 > 

This property holds the range of a Timesequnce. By default, this property is set to \[-infinity, +infinity\].

Note: The modification of this property does not influence the data. This is only for information purpose :

See also [range()](#1adbaf277d78948f5f06dee0edf84a169e), [setRange()](#1a6986c283e30514c8c21b269428b7b6ca)

------------------------------------------------------------------------

Member Type Documentation
-------------------------

    ma::TimeSequence::Type

Contextual information about the kind of data stored in the time sequence.

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
<td>Unknown</td>
<td>= 0x00</td>
<td><p>Unknown type. This is the default type if none is given to a constructor</p></td>
</tr>
<tr class="even">
<td>Reconstructed</td>
<td>= 0x01</td>
<td><p>Internal flag to indicated if these data are reconstructed data. The usage of this flag shall mean that some components are resevred for reconstruction residuals. For example if a <a href="classma_1_1_time_sequence.html">TimeSequence</a> is set to the Type Marker (predefined value included the Reconstructed flag), the given dimension should be set to 4. Three of them are for the coordinates and the later is for the reconstruction residuals.</p></td>
</tr>
<tr class="odd">
<td>Marker</td>
<td>= 0x02 | Reconstructed</td>
<td><p>Should be used to represent a reconstructed/computed 3D trajectory. Data sample shall be represented by an 1D array with 4 components: X, Y, Z coordinates and valid/reconstruction residuals. The associated unit shall be millimeter (&quot;mm&quot;).</p></td>
</tr>
<tr class="even">
<td>Angle</td>
<td>= 0x04 | Reconstructed</td>
<td><p>Should be used to represent a reconstructed/computed 3D angle. Data sample shall be represented by an 1D signal with 4 components: X, Y, Z values and valid/reconstruction residuals. The associated unit shall be radian (&quot;rad&quot;).</p></td>
</tr>
<tr class="odd">
<td>Force</td>
<td>= 0x08 | Reconstructed</td>
<td><p>Should be used to represent a reconstructed/computed 3D force. Data sample shall be represented by an 1D signal with 4 components: X, Y, Z values and valid/reconstruction residuals. The associated unit shall be newton (&quot;N&quot;).</p></td>
</tr>
<tr class="even">
<td>Moment</td>
<td>= 0x10 | Reconstructed</td>
<td><p>Should be used to represent a reconstructed/computed 3D moment. Data sample shall be represented by an 1D signal with 4 components: X, Y, Z values and valid/reconstruction residuals. The associated unit shall be newton-millimeter (&quot;Nmm&quot;).</p></td>
</tr>
<tr class="odd">
<td>Power</td>
<td>= 0x20 | Reconstructed</td>
<td><p>Should be used to represent a reconstructed/computed 1D-2D-3D power. Data sample shall be represented by an 1D signal with 2-3-4 components: X, Y, Z values and valid/reconstruction residuals. The associated unit shall be watt (&quot;W&quot;).</p></td>
</tr>
<tr class="even">
<td>Scalar</td>
<td>= 0x40 | Reconstructed</td>
<td><p>Should be used to represent a reconstructed/computed 1D-2D-3D values. Data sample shall be represented by an 1D signal with 2-3-4 components: X, Y, Z values and valid/reconstruction residuals.</p></td>
</tr>
<tr class="odd">
<td>Pose</td>
<td>= 0x80 | Reconstructed</td>
<td><p>Should be used to represent a reconstructed/computed 3D pose (3D orientation and 3D position). Data sample shall be represented by an 1D signal with 13 components: R11, R21, R31, R12, R22, R32, R31, R23, R33, pX, pY, pZ values and valid/reconstruction residuals. No unit (empty string) shall bet set.</p></td>
</tr>
<tr class="even">
<td>Analog</td>
<td>= 0x100</td>
<td><p>Should be used to represent a measured 1D signal. Data sample shall be represented by an 1D signal with 1 component. The associated unit shall be volt (&quot;V&quot;) or any other acquired unit.</p></td>
</tr>
<tr class="odd">
<td>Other</td>
<td>= 0x10000</td>
<td><p>To be used to extend predefined type. This could be usefull to extract all the node with a specific type.</p></td>
</tr>
</tbody>
</table>

------------------------------------------------------------------------

Member Function Documentation
-----------------------------

    ma::TimeSequence::TimeSequence ( const  std::string  &  name ,  unsigned  components ,  unsigned  samples ,  double  rate ,  double  start ,  int  type ,  const  std::string  &  unit ,  double  scale ,  double  offset ,  const  std::array< double, 2 >  &  range ,  Node  *  parent  = nullptr )

Complete constructor for time series signal with 1D data sample. This constructor can be usefull for Analog signal recorded by a digital-to-analog converter (DAC).

Note: The given ** should be based on the enum Type. :

------------------------------------------------------------------------

    ma::TimeSequence::TimeSequence ( const  std::string  &  name ,  unsigned  components ,  unsigned  samples ,  double  rate ,  double  start ,  int  type ,  const  std::string  &  unit ,  Node  *  parent  = nullptr )

Simplified constructor for time series signal with 1D data sample. Lots of predefined type (Marker, Angle, Force, Moment, etc.) should use this constructor.

Note: The given ** should be based on the enum Type. :

------------------------------------------------------------------------

    ma::TimeSequence::TimeSequence ( const  std::string  &  name ,  const  std::vector< unsigned >  &  components ,  unsigned  samples ,  double  rate ,  double  start ,  int  type ,  const  std::string  &  unit ,  double  scale ,  double  offset ,  const  std::array< double, 2 >  &  range ,  Node  *  parent  = nullptr )

Complete constructor for time series signal with xD data sample. The number of data sample dimensions is determined by the number of *components* given. This constructor can be usefull for pressure matrix or any measuring system with 2D (or more) data sample dimension.

Note: The given ** should be based on the enum Type. :

------------------------------------------------------------------------

    ma::TimeSequence::TimeSequence ( const  std::string  &  name ,  const  std::vector< unsigned >  &  components ,  unsigned  samples ,  double  rate ,  double  start ,  int  type ,  const  std::string  &  unit ,  Node  *  parent  = nullptr )

Simplified constructor for time series signal with xD data sample. The number of data sample dimensions is determined by the number of *components* given. This constructor can be usefull for pressure matrix or any measuring system with 2D (or more) data sample dimension.

Note: The given ** should be based on the enum Type. :

------------------------------------------------------------------------

    ma::TimeSequence::~TimeSequence ( ) noexcept

------------------------------------------------------------------------

    unsigned ma::TimeSequence::components ( ) const noexcept

Returns the total number of components for one data sample. This method multiplies each dimensions together to compute the total number of component. It can be usefull to convert a xD signal into a 1D signal.

------------------------------------------------------------------------

    const  double * ma::TimeSequence::data ( ) const noexcept

Return the pointer storing the internal data

------------------------------------------------------------------------

    double * ma::TimeSequence::data ( ) noexcept

Return the pointer storing the internal data. These data are stored by column.

Warning: You should used this method very carefully. It is recommended to call the method [](classma_1_1_node.html#1abd701c6cf53bf95aba1ea79d28e42f16) manually if you apply modifications on the data. :

------------------------------------------------------------------------

    double ma::TimeSequence::data ( unsigned  sample ,  Is...  indices ) const noexcept [inline]

Extract a read-only element of the time sequence for the given *sample* index and dimensions *indices*. In case the the number of *indices* is not consistent with the number of dimension, ths missing ones are set to 0.

------------------------------------------------------------------------

    double  & ma::TimeSequence::data ( unsigned  sample ,  Is...  indices ) noexcept [inline]

Extract a reference to a read-only element of the time sequence for the given *sample* index and dimensions *indices*. In case the the number of *indices* is not consistent with the number of dimension, ths missing ones are set to 0. If the data are modified by this method, it is adviced to call [modified()](classma_1_1_node.html#1abd701c6cf53bf95aba1ea79d28e42f16) manually

------------------------------------------------------------------------

    const  std::vector< unsigned >  & ma::TimeSequence::dimensions ( ) const noexcept

Returns the data sample dimensions.

------------------------------------------------------------------------

    double ma::TimeSequence::duration ( ) const noexcept

Returns the duration of the time sequence. This corresponds to the division of the number of samples by the sample rate.

------------------------------------------------------------------------

    size_t ma::TimeSequence::elements ( ) const noexcept

Returns the total number of elements. This corresponds to computation of the number of samples by the total number of components.

------------------------------------------------------------------------

    double ma::TimeSequence::offset ( ) const noexcept

Returns the offset value that was possibly used to transform raw data to stored measurement

------------------------------------------------------------------------

    const  std::array< double, 2 >  & ma::TimeSequence::range ( ) const noexcept

Returns the range of measurement of a possible digital-to-analog converter used to record stored data. For example \[-10V, 10V\].

------------------------------------------------------------------------

    void ma::TimeSequence::resize ( unsigned  samples )

Resize the data to fit the number of *samples*. Internally a new buffer is created and previous data are copied. Afterwards, the method deletes the previous data.

------------------------------------------------------------------------

    double ma::TimeSequence::sampleRate ( ) const noexcept

Returns the sample rate

------------------------------------------------------------------------

    unsigned ma::TimeSequence::samples ( ) const noexcept

Returns the number of data samples stored in the time sequence.

------------------------------------------------------------------------

    double ma::TimeSequence::scale ( ) const noexcept

Returns the scaling factor used to record the signal and possibly transform it from raw data to stored measurement

------------------------------------------------------------------------

    void ma::TimeSequence::setOffset ( double  value ) noexcept

Sets the offset value that was possibly used to transform raw data to stored measurement

------------------------------------------------------------------------

    void ma::TimeSequence::setRange ( const  std::array< double, 2 >  &  value ) noexcept

Sets the range of measurement of a possible digital-to-analog converter used to record stored data. For example \[-10V, 10V\].

------------------------------------------------------------------------

    void ma::TimeSequence::setSampleRate ( double  value ) noexcept

Sets the sample rate. This method triggers the [modified()](classma_1_1_node.html#1abd701c6cf53bf95aba1ea79d28e42f16) method if the given value is different of the stored one.

------------------------------------------------------------------------

    void ma::TimeSequence::setScale ( double  value ) noexcept

Sets the scaling factor that was possibly used to transform raw data to stored measurement

------------------------------------------------------------------------

    void ma::TimeSequence::setStartTime ( double  value ) noexcept

Sets the starting time associated with this time sequence. This method triggers the [modified()](classma_1_1_node.html#1abd701c6cf53bf95aba1ea79d28e42f16) method if the given value is different of the stored one.

------------------------------------------------------------------------

    void ma::TimeSequence::setType ( int  value ) noexcept

Sets the type associated with this time sequence. This method triggers the [modified()](classma_1_1_node.html#1abd701c6cf53bf95aba1ea79d28e42f16) method if the given value is different of the stored one.

------------------------------------------------------------------------

    void ma::TimeSequence::setUnit ( const  std::string  &  value ) noexcept

Sets the unit associated with this time sequence. This method triggers the [modified()](classma_1_1_node.html#1abd701c6cf53bf95aba1ea79d28e42f16) method if the given value is different of the stored one.

------------------------------------------------------------------------

    double ma::TimeSequence::startTime ( ) const noexcept

Returns the starting time associated with this time sequence.

------------------------------------------------------------------------

    int ma::TimeSequence::type ( ) const noexcept

Returns the type assocaited with the time sequence.

------------------------------------------------------------------------

    const  std::string  & ma::TimeSequence::unit ( ) const noexcept

Returns the unit associated with this time sequence.

------------------------------------------------------------------------

Member Data Documentation
-------------------------

    ma::TimeSequence::InfinityRange[static]

Constant array to represent an infinity range: \[-infinity, +infinity\].

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


