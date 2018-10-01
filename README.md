check_sap
=========

This plugin communicates with the SAP CCMS via the RFC Protocol.

It supports unicode (use a UTF-8 Locale for best results).

Tested with V7.0 of the 64bit RFC Unicode SDK (RFC_SDK_70_redhat_64bit_UNICODE.SAR),
but it should work with the 32bit version as well.

Also tested with Netweaver

### Usage

See --help for usage information


Examples:

    ./check_sap --client 000 --sysnr 00 --user SAPUSER --pass PASSWD --dest ABC --host 192.168.1.2 -m listsets 
     lists all monitor sets
    
    ./check_sap ...options... -m listmonitors 'SAP CCMS Monitor Templates'
     lists the monitors in a set
    
    ./check_sap ...options... -m listtree 'SAP CCMS Monitor Templates' 'Dialog Overview'
     shows the complete tree for a monitor
    
    ./check_sap ...options... 'SAP CCMS Monitor Templates' 'Dialog Overview' 'Response'
     shows the status of all objects matching the Regex
    
    ./check_sap ...options... --fullpath 'SAP CCMS Monitor Templates' 'Dialog Overview' 'Standard.*\ResponseTime'
     As above, but the path to the object is also used


### Installation

Download and extract the tarball release from https://github.com/NETWAYS/check_sap/releases

You will need autoconf to generate the configure script, and a SAP SDK needs to be installed.
N.B. the SDK must be downloaded directly from SAP.

    autoconf
    ./configure
    make

Pay attention to the messages generated by configure - they should help you check you have
all the files installed that you need.

Make sure to install the libraries where the system can find them
e.g. 

    cp RFC_SDK_70_redhat_64bit_UNICODE/lib/* /usr/local/lib
    ldconfig


The include files in the bapi subdirectory can be regenerated using the genh command
included with the classic SDK.

Example:

    bin/genh ashost=... sysnr=.. user=... passwd=... BAPITNDEXT > bapi/bapitndext.h


For further options see ./configure --help
