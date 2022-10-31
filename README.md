# PyTFTPd
TFTP server and client in Python 3

Customized as per [this post](https://forum.openwrt.org/t/tftp-download-from-tp-link-archer-c2-does-not-work-properly/65531/30) to emulate the anticipation window parameter of [tftpd64](https://pjo2.github.io/tftpd64/), which several people have reported to be needed for the [tftp factory reset process of TP-Link Archer C7 routers](https://openwrt.org/toh/tp-link/archer_c7#if_tftp_flashing_fails) (and also [Archer C2](https://forum.openwrt.org/t/tftp-download-from-tp-link-archer-c2-does-not-work-properly/65531/23)).

Tested while resetting an Archer C7 v5 (EU) router, with a factory firmware of Openwrt 23.03.2, through Raspberry Pi connected directly to the LAN 1 port. You may need an ethernet switch between the two, to prevent network settings loss due to ethernet link training (as described [here](https://forum.openwrt.org/t/tftp-download-from-tp-link-archer-c2-does-not-work-properly/65531/2)).

## Supported features
* RFC 1350 - TFTP revision 2
  * Octet mode transfer (netascii and mail unsupported)
  * Read request (RRQ) only, no write capability
  * Limited error reporting (e.g. all file reading errors reported as FILE_NOT_FOUND, real reason in message string)
* RFC 2347 - TFTP option Extension
* RFC 2348 - TFTP Blocksize Option
* RFC 7440 - TFTP Windowsize Option

## Usage
### Server
Run tftpd.py [port_to_bind_to] [webroot_dir]

### Client
Run tftp.py [server] [port] [file to download]
Save filename, prefered window and block sizes are set using BLOCK_SIZE, WINDOW_SIZE, OUT_FILENAME constants in tftp.py
Logging verbosity can be changed in tftp_common using DEBUG and INFO flags.

## System requirements
Initially tested on Python 3.5 on Linux, then also 3.7. MS Windows is not supported due to usage of Unix signals.
