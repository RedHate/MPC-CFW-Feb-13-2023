                                                        HAKAI
                                                 Ultros / Jay Ray-One
                                                      FEB 14 2023
                                               MPC 2.11.8 / FORCE 3.2.3

            *** PLEASE READ THE ENTIRE DOCUMENT BEFORE PROCEEDING WITH USAGE IT WILL SAVE YOU AND US LOTS OF PAIN ***
                  *** LOTS OF CHANGES TO HOW HAKAI INITIALIZES THE DIFFERENT UNIT MODES AND SCANS FOR CARDS ***


---------------------------------
    FEATURES:
---------------------------------

    -MPC 2.11.8
    -FORCE 3.2.3
    -Will now install on MPC Key 61 (September 4th)
    -Now with Jack! (September 4th)
    -CDROM/DVDROM support (August 13th)
    -NTFS file system support (August 13th)
    -Various unix / mac / windows file systems support (August 13th)
    -Wireless / Bluetooth dongle modules (August 13th)
    -Loopback and Virtual Raw Midi devices (August 13th)
    -Darkice, the icecast2 client for live streaming to internet (August 13th)
    -SSH (Secure Shell Host)
    -Netcat (for routing data streams over ethernet)
    -MPC / FORCE Mode Developer Mode
    -Support for 3 matrix types (Akai APC, Novation Launchpad and the Ablueton Push)
    
---------------------------------
    KNOWN ISSUES:
---------------------------------

    -The control surfaces do not work on the Akai MPC Live II in FORCE mode. (I forget why and havent worried about it much)
    -Serial number not present in force mode, may make using pruchased plugins impossible in force mode when it becomes available.
    
--------------------------------- 
    INSTALL HOW TO:
---------------------------------     

Step 1) Format and name an SD or USB card, then name it HAKAI in all capitals. (or just rename it to HAKAI).

Step 2) After your first run, power off the unit and edit the new "hakai.cfg" that resides on the root of your memory stick.

        There are only 5 options in the configuration.

        ## this option is for setting various unit modes
        # UNIT MODES: "ONE" "LIVE" "LIVE2" "X" "FORCE" "FORCE6"
        export HAKAI_UNIT_MODE="FORCE"

        ## this option is for enabling various kernel modules
        # KERNEL MODULES LEAVE IT ALONE IF YOU DONT KNOW (NAMES MUST BE SEPERATED BY SPACE)
        export HAKAI_LOAD_KMODS="snd-aloop snd-virmidi"

        ## this option starts the arecord / netcat server for streaming the loopback to pc.
        # LOOPBACK NETCAT SERVER
        export HAKAI_START_STREAM="0"

        # this option is the name of the midi config force mode
        # NAME OF MIDI CONFIGURATION FOUND ON SD OR USB
        export HAKAI_MIDI_CFG="midi.cfg"

        # this option enables akai's developer mode
        # DEV_MODE 1 or 0
        export HAKAI_DEV_MODE="0"

Step 3) Reinsert your SD or USB card back into the MPC and power it on, it should then boot into whatever unit mode you specified in the hakai.cfg that
        resides on the root of your SD or USB.


---------------------------------
    FORCE NOTES:
---------------------------------

Using FORCE mode)

        **YOU WILL NEED TO REMAKE YOURE MIDI.CFG FILE IF YOU USE A CUSTOM MAPPING**

        The best supported controllers are the APC Mini and the Launchpad MK 3. However 3 main controller types are supported: Akai APC, Novation Launchpad, and Ableton Push.

        New "hakai shift" button. instead of using "play start" which is also the "select" button by default. I have made the "TC" button the hakai shift button though pretty soon the hakai shift button will be obsolete all together.

        Using a properly mapped matrix controller the layout and control options should match that of the APC mini's factory layout, including all the extra feature layouts such as transforming the select row with:

        midi controller shift + launch 1 = clip stop
        midi controller shift + launch 2 = solo
        midi controller shift + launch 3 = rec arm
        midi controller shift + launch 4 = mute
        midi controller shift + launch 5 = select
        midi controller shift + launch 6 = navigate

        also, pressing the relating buttons suck as "select" will put the select row back into select mode, the same can be said for things like solo, record arm and mute (if you have those mapped, in particular on the MPC X with its dedicated buttons.

        double tapping bank buttons will switch you between the four quadrants of the matrix, since we are limited to 4 * 4 on MPC i had to figure out a way to access all 64 squares of the larger 16*16 matrix on the force.

        -----------------------------------------------
          Surface control (the mpc buttons and pads):
        -----------------------------------------------
        
            When holding erase, copy, select, or edit: tapping pads 1-8 will do the select row options from 1-8.
            When holding erase, copy, select, or edit: tapping pads 9-16 will do the launch row options from 9-16.

            The "master" button, set to TC acts as a special shift button, it used previously be play start (select) but it's uncoupling was required to enable all the features of the select button. Now TC is the "hakai shift" button, here are some co-responding buttons for TC.

            TC + MPC_PAD 1-8 = SELECT / ARM 1-8 depending on which mode you are in, (clip stop, solo, mute, rec arm or select the mode)

            TC + MPC_PAD 9-16 = QUADRANT SELECT (TOP LEFT FOUR) / SELECT ROW MODE BUTTONS (TOP RIGHT FOUR)

            (alternatively to the above, you can use:)

            BANK 1 = QUADRANT 1
            BANK B = QUADRANT 2
            BANK C = QUADRANT 3
            BANK D = QUADRANT 4

        reading about how the force software works on a proper force will give you greater insight into the operation of the program. you may be required to translate the buttons to our hacky modded set up at times to figure things out.





---------------------------------
    OTHER NOTES:
---------------------------------

        CDROM / DVDROM:
            DATA disc only!
            These should work as SCSI or ATAPI. Simply connect the drive to the unit via usb and insert a DATA disc then wait.
            Some drives may struggle as the USB port on the MPC unit doesn't supply enough power, it's advised to use a powered usb hub in conjunction with your optical drives.

        NTFS / LINUX / MAC FILE SYSTEMS:
            Some of us dont use windows, some of us do. A lot of people store their content on file systems that may be out of date so I've included a pile of kernel modules to help mount those old SCSI, and ATAPI devices via usb.

        JACK:
            Jack is an audio / MIDI server / client that provides audio and midi services to JACK based applications, more importantly it allows for low-latency audio / midi over network. Currently there is no user-ready application for this, as I am still studying the usage of jack myself. Perhaps one of the Hakai users are experienced and can help me sort this magic.

        ALSA:
            the alsa modules that have been compiled are plugged in the "hakai.cfg" that resides on your memory stick after the first run. Leave these alone if you dont know what they are for.

        SSH:
            use putty or ssh on linux to gain a remote commandline session on the MPC unit

        NETCAT:
            use to send data streams over ethernet

        DARKICE:
            Darkice is a network broadcasting client for icecast2 servers. It's by default configured to pick up sound from the "Internal Looopback" interface.

        
        DEVELOPER MODE:
            Toggling this on does relatively little other than splash a fancy "Developer mode" across the screen on load time and show some debug info on voices / output some extra info to stdout.

        WIRELESS / BLUETOOTH
            These are not fully implmented. I have compiled and included the modules but I've not investigated if there is a need to interface the devices with the software in any way.

        
Help)
        Having trouble mapping your midi controllers? refer to the hakai custom firmware for mpc group on facebook for more detailed information and instructions.
