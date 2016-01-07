The purpose of the Shared Memory Transport (or SMT) is to solve the problem of sharing data between multiple processes on the same processor.  The concept is to have a central naming service (called smtcore) where processes can register shared memory objects by name.  Once registered, other processes can get access to these memory objects by asking smtcore for a piece of data by that same name.  While smtcore can support arbitrarily complex data structures, in-practice, most pieces of data registered to smtcore are typical basic data-types (int, float, etc).  Because a 64-bit system will access these simple data atomically, there has been no evidence of data corruption due to simultaneous access by two processes (i.e. one process writing to a float and another process reading a float).  However, it is quite possible to have a race condition (the read happening before the write, or vice versa), but such issues are outside the scope of this transport mechanism.  While simple data types are "safe", large data types may not be.  For performance reasons, SMT does not employ any type of lock on the data.  Therefore, large data-types (a large struct of floats and int, for example) could have issues with data synchronicity.

## Command-line Tools:
* smtcore - SMT name service
* smttopic - list | echo | info - List, print, and get info on current SMT topics
* smtlogger - Command-line tool to log SMT topics to HDF5
* smtrelay_client -
* smtrelay_proxy
* smtrelay_pub
* smtrelay_sub
* smtsinewave - Command-line tool to generate a sinewave on an arbitrary SMT topic

## GUI Tools:
* smtlogviewer - PyQt gui to display data contained in an HDF5 data file generated from smtlogger or smtrecorder
* smtrecorder - PyQt gui to record smt data to an HDF5 data file
* smtscope - PyQt gui to look at smt data in real-time
* smttopicviewer - PyQt gui tree display that shows all current smt topic names
* shared_memory_transport_sliderboard - GUI that interfaces a Berringer BCF2000 Midi board to SMT topics

## Build/Generator utilities:
* api_builder - Generates an API to interact with SMT using an xml file
* register_builder - Generates an API to interact with registers