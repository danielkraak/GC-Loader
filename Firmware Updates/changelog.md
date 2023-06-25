2.0.1.BETA:\
	- Add additional recovery options\
 	- Free up resources\
 	- Improve architecture\
2.0.0:\
	- Added write support\
	- New implementation for fragmented file handling\
	- Improved SD Card compatibility:\
		- Fixed issue with PNY cards\
		- Support for standard capacity cards\
	- Several small optimizations\
1.1.2:\
	- Fixed stability issues encountered on certain boards (introduced in 1.1.1)\
1.1.1:\
	- Fixed random corrupted audiostreaming sound\
	- Added some small optimizations\
	- Cleaned up codebase\
1.1.0:\
	- Added safe firmware updates (recovery firmware image is written)\
	- Workaround for hidden filenames (boot.iso.iso, boot.gcm.gcm are also detected at boot)\
1.0.1:\
    - Fixed some stability issues\
    - Decreased FPGA boot time\
1.0.0:\
    - Fragmentation issues when loading through Swiss should be fixed now\
    - Added multi-disc support. Disc swapping is performed automatically\
0.9.0:\
    - Lower disc speed emulation can be forced by turning DIP switch 4 on\
    Currently speed is throttled at ~3MB/s only. Eventually, it will be\
    emulated more accurately\
0.10.0:\
    - 'no disc' is simulated, when SD Card is not inserted or 'boot.iso' is\
    missing
