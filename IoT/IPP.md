# Internet Printing Protocol

IPP specialized for communication between client devices and printers runs on port 631.

> When an IPP port is open on the Internet, it is possible for anyone to print to the printer or even transfer malicious data. This can expose a lot of sensitive information such as printer name, location, model, firmware version or even the printer's Wi-Fi SSID.

Most of them appear to be running the CUPS server (which is a Common UNIX Printing System).

## Exploitation 

```sh
git clone https://github.com/RUB-NDS/PRET
```

1. ps (Postscript)
2. pjl (Printer Job Language)
3. pcl (Printer Command Language)

Try all three languages just to see which one will be understood by the printer.

```sh
python pret.py 192.168.x.x pjl
python pret.py laserjet.lan ps
python pret.py /dev/usb/lp0 pcl
```

> (The last option works if you already have a printer connected to your computer)
