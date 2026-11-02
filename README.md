BMW E60 KOMBI6 – Firmware Reverse Engineering

An independent hobby project documenting the reverse engineering of the BMW E60 KOMBI6 instrument cluster.

The research is based on the Siemens-VDO firmware 7842584A.0pa and covers firmware structure, processor architecture, memory mapping, display data and CAN communication.

Disclaimer

This is an independent hobby project for educational and research purposes. It is not affiliated with or endorsed by BMW AG or Siemens VDO.

All trademarks belong to their respective owners. Information is provided as-is, and any use is at your own risk.

No original firmware or proprietary files are intentionally distributed.

Firmware Information
Property	Value
Cluster	BMW E60 KOMBI6
Firmware	7842584A.0pa
Reference	0101CV0F331S
Manufacturer	Siemens VDO Automotive AG
CPU	Fujitsu MB90F395HA
Architecture	F2MC-16LX, 16-bit
Address space	24-bit
Extracted image	420,080 bytes
Decoded instructions	134,914
Identified call targets	1,389
Memory Layout
Address Range	Contents
0xF80000–0xF8ABxx	Identification and calibration
0xF8B000–0xF9D5FF	Display graphics and fonts
0xFA0000–0xFFBxxx	Application code
0xFF8000–0xFFB780	Configuration and text tables
0xFFBF84–0xFFBFFF	Interrupt vectors
0xFFC000–0xFFFFFF	Bootloader

The bootloader is not included in the supplied firmware image.

Reverse Engineering Findings

The investigation has identified several interesting areas:

F2MC-16LX processor instructions and function calls.
Display fonts, graphics and text tables.
OBC and check-control messages.
Configuration and calibration data.
Interrupt vectors and application entry points.
Display message dispatch routines.
PT-CAN message definitions based on MSS60 documentation.
Display-related addresses
Address	Finding
0xFD8EBD	String copy routine
0x1A19	RAM text buffer
0xF82AA4	Message dispatch table
0xFB1B30	Message dispatcher
Bootloader and Signature Verification

Testing indicates that firmware signature verification is handled separately from the normal programming checks.

Modified firmware images are rejected with NG_SIGNATUR_PRUEFEN, even when the application-side verification routine is changed.

The available evidence points to RSA verification handled by the protected bootloader. Further investigation is ongoing.

CAN Analysis

The MSS60 message documentation was examined, covering 60 message definitions.

Identified messages
Message	CAN ID	Cycle
ENGINE_1	0x1D0	100 ms
TORQUE_3	0x0AA	10 ms
STAT_KOMBI	`0x
