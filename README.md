PiFace Digital Daemon
=====================

Features:

1. daemon allows to communicate with IO ports using XML-RPC over the lan or the Internet;
2. daemon executes files in `/etc/pifacedigitald/event.d` on each input port state change.

Usage
-----

**pifacedigitald** starts by init.d script. Additional arguments can be added in `/etc/default/pifacedigitald`

```
usage: pifacedigitald [-h] [-v] [-E FILE] [-H HOST] [-p PORT] [-l FILE]
                      [-P FILE] [-o FILE] [-e FILE]

PiFace Digital daemon v0.1.1

optional arguments:
  -h, --help            show this help message and exit
  -v, --version         show program's version number and exit
  -E FILE, --on-event FILE
                        file to execute on input port state changes (default:
                        /etc/pifacedigitald/event)
  -H HOST, --host HOST  XML-RPC server host (default: localhost)
  -p PORT, --port PORT  XML-RPC server port (default: 8050)
  -l FILE, --log-file FILE
                        log file path (default: /var/log/pifacedigitald.log)
  -P FILE, --pid-file FILE
                        pid file path (default: /var/run/pifacedigitald.pid)
  -o FILE, --stdout FILE
                        redirect stdout to file
  -e FILE, --stderr FILE
                        redirect stderr to file
```

Put executable files into `/etc/pifacedigitald/event.d` and they will be executed on each input port state change. For additional information read `/etc/pifacedigitald/event`.

**pifacedigital-cli** can be executed on any computer which connected to the raspberry pi with pifacedigitald running.

```
usage: pifacedigital-cli [-h] [-v] [-u URL] [-a 0..3] [-w X] [-b] [-q]
                         i[nput]|o[utput] [0..7]

PiFaceDigital client v0.1.1

positional arguments:
  i[nput]|o[utput]      port
  0..7                  pin number (omit to read/write port)

optional arguments:
  -h, --help            show this help message and exit
  -v, --version         show program's version number and exit
  -u URL, --url URL     XML-RPC server url (default:
                        http://localhost:8050/RPC2)
  -a 0..3, --address 0..3
                        hardware address (default: 0)
  -w X, --write X       write value to pin or port
  -b, --binary          print result in binary format
  -q, --quite           do not print result

environment variables:
  PIFACEDIGITAL_SERVER  XML-RPC server url
```

Installation
------------

On any computer with latest stable debian or ubuntu (it can be raspberry pi):
```
$ git clone https://github.com/Shura1oplot/pifacedigitald
$ cp pifacedigitald pifacedigitald-0.1.1
$ cd pifacedigitald-0.1.1
$ debuild -uc -us -b
```

On raspberry pi with raspbian:
```
$ sudo dpkg -i pifacedigitald_0.1.1-1_all.deb
```
