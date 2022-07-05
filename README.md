# PAL-Gnuradio-video2pal-
Gnuradio Flowgraph to generate a PAL signal out of a YUV stream.

This graph is a rebuild from the https://github.com/cyber-murmel/video2pal graph. It runs in Gnuradio 3.10.
The input file is a raw YUV stream. It can be created using ffmpeg

ffmpeg -i inputfile.mp4 \
-c:v rawvideo \
-vf 'scale=702:576:force_original_aspect_ratio=decrease,pad=702:576:(ow-iw)/2:(oh-ih)/2' \
-f rawvideo \
-pix_fmt yuv444p \
-r 50 \
yuv.bin

What the graph does is to split the input into odd and even Y-U-V fields, interlaces them, pads the Y fields with H- and V-Sync information.
The U and V fields are transformed into a complex signal with alternating phase and modulated on a 4.43MHz subcarrier. Also colorburst is added. Y and the transformed UV signals are added together resulting in a basedband signal ready for broadcast.

Additionally a FM subcarrier could be added to get sound aswell.
