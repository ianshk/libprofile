LibProfile
----------

LibProfile is a very light weight code profiler which aims to support a wide range of video game consoles and embedded devices. Currently LibProfile supports the Nintendo Wii & Gamecube platforms. It is currently a very basic profiler but useful for optimizing and finding bottlenecks.

LibProfile allows for an unlimited number of profile jobs to be run at any time and 'currently' outputs results in Number of Clock cycles taken and Microseconds (us). Profile jobs will also record the minimum and maximum execution time spent in your code and the total duration.

The code is written in C with a few lines of inline assembly language to read the time base registers of the CPU.

Instructions
------------

Create a Profile Job
--------------------

include the the following 2 files in your code. 

#include "timer.h"
#include "profiler.h"

To start profiling code you first have to create a profile job with a given name:

profiler_t myjob;

profiler_create(&myjob,"Any profile name");

Recording
---------

To start recording you need a start and end point for your Profile job, and your code must be placed inside these points like shown below:

profiler_start(&myjob);

// Your code here

profiler_stop(&myjob);

An example of inserting a job inside a loop is shown below. The Job in this case will log the number of iterations, and the minimum and maximum time it took for your code to run inside the loop.

For(i=0;i<10;i++)
{
	profiler_start(&myjob);
	// Code
	profiler_stop(&myjob);
}

Output
------

To output information on a profile job you just call the following function:

profiler_output(&myjob);

The function just calls printf to display to the screen, you will need to change this to suit your needs, i.e to debug console, texture font print routine etc.

Notes:
------

A profile job will keep logging until its reset, to reset you just call profiler_reset(&myjob); and it will reset all variables back to 0.

Todo:
-----

Cache Profiling & Cache Miss reporting
ARM support (iPhone etc)
MIPS Support (PSP etc)
64 Bit device support (PS3 Linux)

Feedback / Suggestions are most welcome.