---
layout: default
tags: realtime faq
---


# How should I get started with the FieldTrip realtime buffer?

The fastest and best way to get started is to try out something really simple. This does not require MATLAB. 

Navigate to the directory ''fieldtrip/realtime/bin/ARCH'' where ARCH is the architecture of your compute

 | Architecture | Description                                                             | 
 | ------------ | -----------                                                             | 
 | win32        | 32-bit Microsoft Windows                                                | 
 | mac          | 32-bit Mac OS X on [PPC](http://en.wikipedia.org/wiki/PowerPC) hardware | 
 | maci         | 32-bit Mac OS X                                                         | 
 | maci64       | 64-bit Mac OS X                                                         | 
 | glnx86       | 32 bit Linux                                                            | 
 | glnxa64      | 64 bit Linux                                                            | 
 | raspberrypi  | Debian Linux on the [Raspberry Pi](http://www.raspberrypi.org/)         | 

Unless otherwise specified, this assumes that you are using an Intel-compatible computer.

 1.  Start the ''buffer'' application.
 2.  Start the ''sine2ft'' application.
 3.  Start the ''viewer'' application.

The buffer application does not show anything, it only starts the buffer, which subsequently starts listening to network requests on port 1972 (the default port). On the DOS or Unix command line you are able to specify another port, but that is not required here.

The sine2ft and viewer initially looks like thi

![image](/media/faq/sine2ft.png@300)
![image](/media/faq/bufferviewer.png@400)



If you click "start" in the sine2ft window, and subsequently "connect" in the viewer window, you will see that data starts streaming from sine2ft->buffer->viewer.



![image](/media/faq/sine2ft_running.png@300)
![image](/media/faq/bufferviewer_running.png@400)



## Connect from MATLAB

Subsequently you could start MATLAB, while keeping the three programs running, and run the followin

    while true
    hdr = ft_read_header('buffer://localhost:1972')
    pause(1)
    end

which will show something like this, being updated every second.

    hdr = 
             Fs: 2000
         nChans: 16
       nSamples: 182784
    nSamplesPre: 0
        nTrials: 1
           orig: [1x1 struct]
          label: {16x1 cell}
       chantype: {16x1 cell}
       chanunit: {16x1 cell}

You should see hdr.nSamples increasing over time.

Subsequently you could do

    while true
    dat = ft_read_data('buffer://localhost:1972', 'begsample', 1, 'endsample', inf);
    plot(dat');
    pause(1)
    end

to see the amount of data in the buffer steadily increasing over time. Note that all channels have exactly the same value, hence you will only see a single sine wave. 

![image](/media/faq/screen_shot_2013-11-12_at_17.05.01.png@400)

After a certain amount of time, the [ring buffer](http://en.wikipedia.org/wiki/Circular_buffer) will fill up and start wrapping around. From that point onward you will not be able to read the data all the way back from sample 1. 

You can combine the **[ft_read_header](/reference/ft_read_header)** and **[ft_read_data](/reference/ft_read_data)** calls to plot only the data of interest. You can also use **[ft_read_event](/reference/ft_read_event)** to determine triggers, and based on those process certain pieces of data. 


## Suggested further reading

The [getting started with realtime analysis](/getting_started/realtime) documentation provides a more elaborate starting point. You might also want to click on the "realtime" tag at the top of this page, which will show you all other pages that share the same tag.

    