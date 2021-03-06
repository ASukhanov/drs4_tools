# drs4-tools
Set of tools to process data, generated by DRS4 eval board and similar devices.

1) Root analysis

  Features
    Fast timing calibration. ~100 faster than DRS.cpp 

  Analysys options
    a) matched filtering, not recommended.
    b) fitting the pulse using spline-approximated function of the predefined piecewise signal shape.
    The predefined piecewise signal shape can be constructed from the first event, 
    this is default behavior, or from a profile histogram using 
    get_shape_from_saved_profile.C macro. 
    The profile histogram file can be generated using write_profile.C.

  To compile:
    make

  To run:
    root -l -c Init.C

  Analyze 1000 events:
    root> int ii;
    root> for( ii=0; ii<1000; ii++) d4r->Next_event();

  For adjusting parameters see init.C

2) drs4_analyzer: standalone program to analyze binary files, produced by drsosc program 
  Standalone program to process binary files saved by DRSOsc program.
  The drs4_analyzer is much fatster than the read_binary.
  
  Features:
    Fast calibration,
    Baseline subtraction,
    FIR filtering. Note the FIR filtering does not improve the time resolution as expected, 
                   the reason: the jitter of signal shape, the tail of the shape is useless
                   for time resolution.

  Usage: drs4_analyzer file.drs options

  OPTIONS:
    -nN  negative pulse processing of channel N.
    -c   disable timing calibration.
    -tV  set LED threshold to V {0.0:1.0].
    -fSN enable FIR filtering, S is filter shape (a:first event, r:rectangular, t:triangle), N is filter length.
    -bN  N-point baseline subtraction (N>1), single cell noise is calculated when N>0.
    -r   regularization of cell intervals (make it equidistant), not yet commissioned.
    -eN  process V events.
    -vN  verbosity level.

  Compile it:
       gcc drs4_analyzer.cpp mfilter.cpp -o drs4_analyzer -lm

drs4root: Simple ROOT analysis of binary data from DRS4 eval board.

