### Using HL-2250DN on Fedora 25

```
$ sudo sh linux-brprinter-installer-2.1.1-1
Input model name ->HL-2250DN

You are going to install following packages.
   hl2250dnlpr-2.1.0-1.i386.rpm
   cupswrapperHL2250DN-2.0.4-2.i386.rpm
OK? [y/N] ->y

rpm -ihv --nodeps --replacefiles --replacepkgs hl2250dnlpr-2.1.0-1.i386.rpm
Preparing...                          ################################# [100%]
Updating / installing...
   1:hl2250dnlpr-2.1.0-1              ################################# [100%]
rpm -ihv --nodeps --replacefiles --replacepkgs cupswrapperHL2250DN-2.0.4-2.i386.rpm
Preparing...                          ########################################
Updating / installing...
cupswrapperHL2250DN-2.0.4-2           ########################################
#
semanage fcontext -a -t cupsd_rw_etc_t /usr/local/Brother/Printer/(.*/)?inf(/.*)?
restorecon -R /usr/local/Brother/Printer
semanage fcontext -a -t bin_t /usr/local/Brother/Printer/(.*/)?inf/brprintconf(.*)?
restorecon -R /usr/local/Brother/Printer
semanage fcontext -a -t bin_t /usr/local/Brother/Printer/(.*/)?lpd(/.*)?
restorecon -R /usr/local/Brother/Printer
semanage fcontext -a -t bin_t /usr/local/Brother/Printer/(.*/)?cupswrapper(/.*)?
restorecon -R /usr/local/Brother/Printer
semanage fcontext -a -t bin_t /usr/local/Brother
restorecon -R /usr/local/Brother
restorecon -RFv /usr/lib/cups/filter
restorecon reset /usr/lib/cups/filter/brlpdwrapperHL2250DN context unconfined_u:object_r:bin_t:s0->system_u:object_r:bin_t:s0
setsebool -P cups_execmem 1
Will you specify the Device URI? [Y/n] ->Y


0: socket
1: ipps
2: serial:/dev/ttyS4?baud=115200
3: http
4: beh
5: https
6: lpd
7: ipp
8: smb
...
...
11 (I): Specify IP address.
12 (A): Auto. (dnssd://XYZ/)

select the number of destination Device URI. ->11

 enter IP address ->192.168.1.42
lpadmin -p HL2250DN -v socket://192.168.1.42 -E
Test Print? [y/N] ->y

wait 5s.
lpr -P HL2250DN /usr/share/cups/data/testprint
Hit Enter/Return key.
```
