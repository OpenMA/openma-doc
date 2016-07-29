ma::io::Handler::FormatError
============================

General exception to use when an error happens during the reading/writing of data. The internal implementation of a [Handler](classma_1_1io_1_1_handler.html) use exception to determine if something wrong happened. All kind of exceptions are catched, but it is strongly advise to use [FormatError](classma_1_1io_1_1_handler_1_1_format_error.html) for case managed by an handler.

Member Function Documentation
-----------------------------

    ma::io::Handler::FormatError::FormatError ( const  std::string  &  msg ) [inline]

Construct a [FormatError](classma_1_1io_1_1_handler_1_1_format_error.html) exception

------------------------------------------------------------------------

Documentation licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


