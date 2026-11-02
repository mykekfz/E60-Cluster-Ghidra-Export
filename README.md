BMW E60 KOMBI6 – Firmware Reverse Engineering

This is an independent reverse-engineering project documenting research into the BMW E60 KOMBI6 instrument cluster.

The analysis is based on the Siemens-VDO firmware file 7842584A.0pa and covers firmware structure, processor architecture, memory mapping, display data and CAN communication.

Disclaimer

This project is provided for educational, research and interoperability purposes only.

It is an independent project and is not affiliated with, endorsed by or associated with BMW AG, Siemens VDO or their subsidiaries.

All trademarks, product names and references belong to their respective owners.

No warranty is provided regarding the accuracy, completeness or suitability of the information published here. The material is provided "as is".

The project does not provide modified commercial firmware for vehicle use. Any experimentation is undertaken at the user's own risk. The author accepts no responsibility for damage to vehicles, electronic components, equipment or other property resulting from the use of this information.

Readers are responsible for ensuring that their activities comply with applicable laws, intellectual property rights and vehicle safety regulations.

Firmware Information
Cluster: BMW E60 KOMBI6
Firmware: 7842584A.0pa
Reference: 0101CV0F331S
Manufacturer: Siemens VDO Automotive AG
CPU: Fujitsu MB90F395HA (F2MC-16LX)
Architecture: 16-bit, 24-bit address space
Extracted image: 420,080 bytes
Decoded instructions: 134,914
Identified call targets: 1,389
Memory Layout
Address	Contents
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

Some identified display-related addresses:

Address	Finding
0xFD8EBD	String copy routine
0x1A19	RAM text buffer
0xF82AA4	Message dispatch table
0xFB1B30	Message dispatcher
Bootloader and Signature Verification

Testing indicates that the cluster performs firmware signature verification separately from the normal programming checks.

Modified firmware images are rejected with NG_SIGNATUR_PRUEFEN, even when the application-side verification routine is changed.

The available evidence points to RSA verification handled by the protected bootloader. Further investigation is ongoing.

CAN Analysis

The MSS60 message documentation was examined, covering 60 message definitions.

Some relevant messages:

Message	CAN ID	Cycle
ENGINE_1	0x1D0	100 ms
TORQUE_3	0x0AA	10 ms
STAT_KOMBI	0x1B4	100 ms

The analysis includes engine temperature, oil temperature, RPM, alive counters and message checksums.

Battery voltage and fuel level are handled through internal cluster hardware inputs rather than ordinary PT-CAN signals.

Project Status

The firmware has been extracted and analyzed, with substantial progress on instruction decoding, memory mapping and display-related functions.

Further work will focus on understanding the display system, identifying additional RAM variables and documenting the remaining firmware structures.

This project is a work in progress. Findings are published for technical documentation and research purposes.
