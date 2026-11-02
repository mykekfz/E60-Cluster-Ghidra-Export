BMW E60 KOMBI6 – Reverse Engineering

Independent hobby project exploring the firmware of the BMW E60 KOMBI6 instrument cluster.

The project focuses on understanding the firmware, processor architecture, memory layout, display system and CAN communication.

Disclaimer

This is a personal hobby project for educational and research purposes. It is not affiliated with or endorsed by BMW AG or Siemens VDO.

All trademarks belong to their respective owners. Information is provided as-is and used at your own risk.

No original firmware or proprietary files are intentionally distributed.

Firmware Details
Description	Value
Cluster	BMW E60 KOMBI6
Firmware	7842584A.0pa
Reference	0101CV0F331S
Manufacturer	Siemens VDO
Processor	Fujitsu MB90F395HA
Architecture	F2MC-16LX
Address space	24-bit
Extracted image	420,080 bytes
Decoded instructions	134,914
Identified call targets	1,389
Memory Layout
Address	Description
0xF80000–0xF8ABxx	Identification and calibration
0xF8B000–0xF9D5FF	Display graphics and fonts
0xFA0000–0xFFBxxx	Application code
0xFF8000–0xFFB780	Configuration and text tables
0xFFBF84–0xFFBFFF	Interrupt vectors
0xFFC000–0xFFFFFF	Bootloader

The bootloader is not included in the supplied firmware image.

Reverse Engineering

The following areas have been investigated:

F2MC-16LX instruction decoding
Function calls and application structure
Display fonts and graphics
OBC and check-control messages
Configuration and calibration data
Interrupt vectors
Display message handling
PT-CAN message definitions
Display-related addresses
Address	Description
0xFD8EBD	String copy routine
0x1A19	RAM text buffer
0xF82AA4	Message dispatch table
0xFB1B30	Message dispatcher
Bootloader

Testing indicates that firmware signature verification is separate from the normal programming checks.

Modified firmware images are rejected with NG_SIGNATUR_PRUEFEN, even when the application-side verification routine is changed.

Current findings point to RSA verification handled by the protected bootloader. Further research is ongoing.

CAN Communication

The MSS60 message documentation was examined, covering 60 message definitions.

Identified messages
Message	CAN ID	Cycle
ENGINE_1	0x1D0	100 ms
TORQUE_3	0x0AA	10 ms
STAT_KOMBI	0x1B4	100 ms

Research includes engine temperature, oil temperature, RPM, alive counters and message checksums.

Battery voltage and fuel level are handled internally by the cluster rather than through ordinary PT-CAN signals.

Project Status

Firmware extraction and instruction decoding are complete for the analyzed image.

Current work focuses on:

Improving function identification in Ghidra.
Understanding the display system.
Mapping additional RAM variables.
Investigating firmware structures and CAN communication.

More findings will be added as the project develops.
