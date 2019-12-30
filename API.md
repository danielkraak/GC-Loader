# GC Loader API

## Commands

<table>
    <tr style="font-weight:bold">
        <td>CMD</td>
        <td>DICMDBUF0</td>
        <td>DICMDBUF1</td>
        <td>DICMDBUF2</td>
        <td>RET</td>
        <td>Description</td>
    </tr>
    <tr>
        <td>DI_INQUIRY</td>
        <td>0x12000000</td>
        <td>-</td>
        <td>-</td>
        <td>32 bytes:<br />
            - Bytes 0-3: 0x00000000;<br />
            - Bytes 4-7: 0x20196c64;<br />
            - Bytes 8-11: 0x61000000;<br />
            - Rest is zeros
        </td>
        <td>Normal inquiry command.<br /><br />
            This code can be used to uniquely identify GC Loader.
        </td>
    </tr>
    <tr>
        <td>DI_GCODE_READ_ID</td>
        <td>0xB0000000</td>
        <td>-</td>
        <td>-</td>
        <td>0xAAAAAAAA</td>
        <td>Get GCODE ID.</td>
    </tr>
    <tr>
        <td>DI_GCODE_GET_VERSION</td>
        <td>0xB10000yy</td>
        <td>-</td>
        <td>-</td>
        <td>
        If yy=1: length of version string (4 bytes) <br /><br />
        If yy=0: version string (arbitrary nr of bytes)
        </td>
        <td>Get GCODE firmware version.</td>
    </tr>
    <tr>
        <td>DI_GCODE_READ</td>
        <td>0xB2000000</td>
        <td>‘Start block’ to read from.</td>
        <td>nr of bytes to read</td>
        <td>-</td>
        <td>Read bytes from SD Card.</td>
    </tr>
    <tr>
        <td>DI_GCODE_SET_DISK_FRAGS</td>
        <td>0xB300000yy</td>
        <td>Disc number</td>
        <td>If yy=1: nr of frags<br /><br />
            If yy=2: unused
        </td>
        <td>If yy = 1: <br />
            - 0x00: ready to receive frag table <br />
            - 0x04: Error; Disc number too high <br />
            - 0x03: Error; too many fragments <br /><br />
            If yy=2: <br />
            - 0x00: Success; changed active disc<br />
            - 0x04: Error; Disc number too high <br />
        </td>
        <td>Set the disk frags or change active disc.<br /><br />
            yy=1: Initialize frag table transfer <br /><br />
            yy=2: set active disc
        </td>
    </tr>


</table>
 

### Further Details
<b>DI_GCODE_SET_DISK_FRAGS</b>

After initializing a fragment table transfer (DICMDBUF0=0xB3000001), GCLoader expects the actual fragments from the GameCube. In one single transfer, one fragment can be sent. Arguments should be as follows:
- DICMDBUF0: Offset in file (byte offset)
- DICMDBUF1: Size of the fragment (in bytes)
- DICMDBUF2: Sector of the fragment

After each fragment transfer, the GC Loader replies with one of the following values:
- 0x00000000: done; received all fragments.
- 0x00000002: expecting more fragments.
