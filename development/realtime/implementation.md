---
layout: default
tags: realtime development
---


#  Specific software implementations for realtime EEG/MEG/fMRI/NIRS

This page is part of the documentation series of the Fieldtrip buffer for realtime aquisition. The FieldTrip buffer is a standard that defines a central hub (the [FieldTrip buffer](/development/realtime)) that facilitates realtime exchange of neurophysiological data. The documentation is organized in five main sections, bein

1.  description and general [overview of the buffer](/development/realtime/buffer_overview),
2.  definition of the [buffer protocol](/development/realtime/buffer_protocol),
3.  the [ reference implementation](/development/realtime/reference_implementation ), and
4.  specific [implementations](/development/realtime/implementation) that interface with acquisition software, or software platforms.
5.  the [getting started](/getting_started/realtime) documentation which takes you through the first steps of real-time data streaming and analysis in MATLAB

This page deals with specific implemenations of the FieldTrip buffer protocol. This includes interfacing with specific hardware (e.g. TMSi, Biosemi, CTF), software platforms (e.g. BCI2000, BrainStream) and links to the implementation in specific programming languages (e.g. MATLAB, Java, C/C++, Python).

## Implementations for specific aquisition systems

*  [ANT NeuroSDK](/development/realtime/NeuroSDK)
*  [Artinis Medical Systems (NIRS)](/development/realtime/artinis)
*  [BrainVision Recorder](/development/realtime/rda)
*  [Biosemi](/development/realtime/Biosemi)
*  [CTF (MEG)](/development/realtime/CTF)
*  [Emotiv](/development/realtime/Emotiv)
*  [Elekta Neuromag (MEG)](/development/realtime/Neuromag)
*  [Jinga-Hi (LFP/EEG)](/development/realtime/jinga-hi)
*  [Micromed (ECoG)](/development/realtime/Micromed)
*  [ModularEEG/OpenEEG](/development/realtime/ModularEEG)
*  [Neuralynx (LFP)](/development/realtime/Neuralynx)
*  [Neurosky ThinkCap](/development/realtime/Neurosky)
*  [OpenBCI](/development/realtime/OpenBCI)
*  [Sound card input](/development/realtime/audio2ft)
*  [Siemens fMRI](/development/realtime/fmri)
*  [TMSI](/development/realtime/tmsi)
*  [TOBI](/development/realtime/tobi)

## Streaming data to other platforms

*  [Java](/development/realtime/buffer_java) client-side implementation
*  [Python](/development/realtime/buffer_python) client-side implementation
*  [development:realtime:Arduino](/development/realtime/Arduino) client-side implementation
*  [BCI2000](/development/realtime/bci2000) includes the FieldTripBuffer and the FieldTripBufferSource modules
*  [BrainVision RDA interface](/development/realtime/rda) allows streaming data in the RDA format
*  [development:realtime:BrainStream](/development/realtime/BrainStream) is directly supported through shared MATLAB code

## Additional useful tools

*  [development:realtime:serial_event](/development/realtime/serial_event) is a C application that turns incoming characters from a serial port into FieldTrip buffer events (used for translating TTL pulses in [realtime fMRI](/development/realtime/fmri))
*  [development:realtime:buffer_java#MidiToBuffer](/development/realtime/buffer_java#MidiToBuffer) is a Java application that turns MIDI messages into FieldTrip buffer events
*  [development:realtime:buffer_java#MarkerGUI](/development/realtime/buffer_java#MarkerGUI) is a graphical Java application that allows to write FieldTrip buffer events with a freely chosen *type* and *value* string.
*  [development:realtime:viewer](/development/realtime/viewer) is a graphical C++ application to visualize online signals from the FieldTrip buffer
*  [Testing with sine waves and pre-recorded EEG data](/development/realtime/eeg)
*  [Testing with pre-recorded fMRI data](/development/realtime/fmri#testing_with_pre-recorded_fmri_data)

### Recording and playing back online experiments

There are two applications, based on the FieldTrip buffer, that allow to record an online experiment for later playback at the original "speed", and thus help developers with debugging and testing different analysis schemes. WARNING: The file format used is not 100% finalised yet, so we advise
against using these tools for archiving your data.

The first application, **recording**, will act to the outside world as a normal FieldTrip buffer server. Internally, however, every incoming request is also handed to a callback function that stores all incoming data on disk. The program resides in ''fieldtrip/realtime/acquisition/general/'' and
is called like thi
    recording someDirectory [port=1972]
This will spawn the callback-enabled buffer server on the given port, create the given directory (which must NOT exist already), and write a plain text file ''contents.txt'' into that directory. This file is always the same and just contains a general description of the way the **recording** writes data.
Now, each time a header is written, a new subdirectory (starting with 0001) is created, the header is written there in binary and ASCII form, and all further samples and events are also written to binary files. The arrival time of incoming sample and event blocks is measured relative to the
arrival time of the header, and logged in an ASCII file called ''timing''. For stopping the operation, the user may safely press CTRL-C which will close down the server thread and close any open files.

The other application, **playback** in the ''fieldtrip/realtime/acquisition/general/'' directory, can be started like this
    playback someDirectory/0001 hostname port
This will replay the data recorded in the first "session" above, at almost exactly the original timing. In contrast to **recording**, this application will not spawn its own buffer server, but it can only stream data to a remote server. The design rational for this was that you might want to replay an experiment several times, but keep the buffer server running in a similar way as it's done with real acquisition systems.

To create a new buffer you can call this from MATLAB using ft_create_buffer

## Creating a new implementation that uses the buffer

 | Language | Client | Server | Notes                                                                                                                                      |
 | -------- | ------ | ------ | -----                                                                                                                                      |
 | C        | yes    | yes    | Reference implementation, please see [here](/development/realtime/buffer_c)                                                                |
 | C++      | yes    | yes    | Thin wrapper classes around the reference implementation for handling client requests, please see [here](/development/realtime/buffer_cpp) |
 | Matlab   | yes    | yes    | Full support via MEX files, please see [here](/development/realtime/buffer_matlab)                                                         |
 | Python   | yes    | no     | this depends on [Numpy](http://numpy.scipy.org), please see [here](/development/realtime/buffer_python)                                    |
 | Java     | yes    | no     | please see [here](/development/realtime/buffer_java)                                                                                       |

## Closing the loop

For a real-time BCI system, it is important that a control signal somehow can be used to close the loop towards the subject. [Here](/development/realtime/closing_the_loop) you can find a description on the options that you have for [development:realtime:closing the loop](/development/realtime/closing the loop) from within your Matlab-based BCI application.

Current plans and design considerations for building a general pipeline architecture can be found [here](/development/realtime/pipeline).