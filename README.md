yavta
====

Yet Another V4L2 Test Application

    make

FSR172X
----

    width=2048
    height=128
    size=${width}x${height}
    frames=8
    skip=0
    yavta -c$frames -p -F --skip $skip -f SGRBG12 -s $size $(./media-ctl -e 'OMAP3 ISP CCDC output')


GumStix Example with Caspa
--------------------------
    
    `
    media-ctl -r
    media-ctl -v -l '"mt9v032 3-005c":0->"OMAP3 ISP CCDC":0[1]'
    media-ctl -v -l '"OMAP3 ISP CCDC":1->"OMAP3 ISP CCDC output":0[1]'
    media-ctl -v -V '"mt9v032 3-005c":0 [SGRBG10 752x480]'
    media-ctl -v -V '"OMAP3 ISP CCDC":1 [SGRBG10 752x480]'

    ./yavta -f SGRBG10 -s 752x480 -n 4 --capture=200 --skip=1000 $(media-ctl -e "OMAP3 ISP CCDC output") --host-ip 10.1.4.115 --host-port=3490
    `






Cross-Compiling
----

    export ARCH=arm
    export CROSS_COMPILE=${HOME}/overo-oe/tmp/sysroots/i686-linux/usr/armv7a/bin/arm-angstrom-linux-gnueabi-
    make

Usage
====

    -c, --capture[=nframes]   Capture frames
    -d, --delay     Delay (in ms) before requeuing buffers
    -f, --format format   Set the video format
    -F, --file[=prefix]   Read/write frames from/to disk
    -h, --help      Show this help screen
    -i, --input input   Select the video input
    -l, --list-controls   List available controls
    -n, --nbufs n     Set the number of video buffers
    -p, --pause     Pause before starting the video stream
    -q, --quality n     MJPEG quality (0-100)
    -r, --get-control ctrl    Get control 'ctrl'
    -s, --size WxH      Set the frame size
    -t, --time-per-frame num/denom  Set the time per frame (eg. 1/25 = 25 fps)
    -u, --userptr     Use the user pointers streaming method
    -w, --set-control 'ctrl value'  Set control 'ctrl' to 'value'
        --enum-formats    Enumerate formats
        --enum-inputs   Enumerate inputs
        --no-query      Don't query capabilities on open
        --offset      User pointer buffer offset from page start
        --requeue-last    Requeue the last buffers before streamoff
        --skip n      Skip the first n frames
        --sleep-forever   Sleep forever after configuring the device
        --host-ip       IP of host to send image packets to
        --host-port     Port of host to send image packets to

