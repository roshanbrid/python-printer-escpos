Introduction
============

Complete set of documentation at https://pythonhosted.org/python-printer-escpos/

python-printer-escpos is a package to directly print to ESCPOS specification(http://content.epson.de/fileadmin/content/files/RSD/downloads/escpos.pdf) compliant POS printers directly over Serial, USB, Network or UNIX device file connections.

This package supports most of the escpos specification functionality and allows you to print QR codes, logo images, barcode in the default mode. The package may be extended by adding your own escpos.commandset.* module instead of the default escpos.commandset.generic package. If you extend the functionality for this package for a specific printer, do publish your code on PyPi and email to provide a link for your commandset in this package's documentation.


Installation
============

Get some prerequisites first for image printing etc.

::

  pip install Pillow

Install python-printer-escpos

::

  pip install python-printer-escpos

Examples
========

USB Printer
-----------

Advanced Usage
''''''''''''''

See https://pythonhosted.org/python-printer-escpos/manual/connections/usb.hyml

Synopsis
''''''''

.. code:: python

  from escpos.connections import getUSBPrinter


  printer = getUSBPrinter()(idVendor=0x1504,
                            idProduct=0x0006
                            inputEndPoint=0x82,
                            outputEndPoint=0x01) # Create the printer object with the connection params

  printer.text("Hello World")
  printer.lf()


Network Printer
---------------

Advanced Usage
''''''''''''''

See https://pythonhosted.org/python-printer-escpos/manual/connections/network.html

Synposis
''''''''

.. code:: python

  from escpos.connections import getNetworkPrinter


  printer = getNetworkPrinter()(host='192.168.0.20', port=9100)

  printer.text("Hello World")
  printer.lf()

Serial Printer
--------------

Advanced Usage
''''''''''''''

See https://pythonhosted.org/python-printer-escpos/manual/connections/serial.html

Synposis
''''''''

.. code:: python

  from escpos.connections import getSerialPrinter


  printer = getSerialPrinter()(dev='/dev/ttyS0',
                            baudrate=9600)

  printer.text("Hello World")
  printer.lf()

Device File Printer
-------------------

Advanced Usage
''''''''''''''

See https://pythonhosted.org/python-printer-escpos/manual/connections/file.html

Synposis
''''''''

.. code:: python

  from escpos.connections import getFilePrinter


  printer = getFilePrinter()(dev='/dev/ttys2')

  printer.text("Hello World")
  printer.lf()

Generic example code
--------------------

See the full list of available default commands at https://pythonhosted.org/python-printer-escpos/modules/escpos.commandset.html

.. code:: python

  from escpos.connections import getUSBPrinter


  printer = getUSBPrinter()(idVendor=0x1504,
                            idProduct=0x0006
                            inputEndPoint=0x82,
                            outputEndPoint=0x01) # Create the printer object with the connection params

  # Print a image
  printer.image('/home/shantanu/companylogo.gif')

  printer.text("Hello World")
  printer.lf()

  printer.align('center')
  printer.text('This text is center aligned')

  # Print a barcode
  printer.barcode(text='Shantanu', textPosition='below', font='b', height=100, width=2, system='CODE93')
  printer.lf()

  printer.bold()
  printer.text('This text is bold text')
  printer.lf()
  printer.bold(False)
  printer.text('This text is not bold')
  printer.lf()

  printer.charSpacing(1)
  printer.text('This text has normal right char spacing')
  printer.lf()
  printer.charSpacing(5)
  printer.text('This text has 5 right char spacing')
  printer.lf()

  printer.color()
  printer.text('This text is in primary color')
  printer.lf()
  printer.color(1)
  printer.text('This text is in color 1')
  printer.lf()

  printer.doubleHeight()
  printer.text('This text is double height text')
  printer.lf()
  printer.doubleHeight(False)
  printer.text('This text is not double height')
  printer.lf()

  printer.doubleStrike()
  printer.text('This text is double strike text')
  printer.lf()
  printer.doubleStrike(False)
  printer.text('This text is not double strike')
  printer.lf()

  printer.doubleWidth()
  printer.text('This text is double width text')
  printer.lf()
  printer.doubleWidth(False)
  printer.text('This text is not double width')
  printer.lf()

  printer.font('b')
  printer.text('This text is in font b')
  printer.lf()
  printer.font('a')
  printer.text('This text is in font a')
  printer.lf()

  printer.invert()
  printer.text('This text is in inverted colors')
  printer.lf()
  printer.invert(False)
  printer.text('This text is not in inverted colors')
  printer.lf()

  printer.leftMargin(30)
  printer.text('This text has left Margin of 30')
  printer.lf()

  printer.lineSpacing()
  printer.text('This text has 1/6 inch line spacing')
  printer.lf()
  printer.lineSpacing(5)
  printer.text('This text has 5/60 inch line spacing')
  printer.lf()

  printer.printAreaWidth(200)
  printer.text('Set print area width to 200')
  printer.lf()
  printer.text('1234567890123456789012345678901234567890123456789012345678901234567890')
  printer.printAreaWidth()
  printer.lf()

  # Print QR Code
  printer.qr('My name is Shantanu Bhadoria')
  printer.qr('WIFI:T:WPA;S:ShantanusWifi;P:wifipasswordhere;;')  # Create a QR code for connecting to a Wifi
  printer.lf()

  printer.rotate90(100)
  printer.text('This text is rotated 90 degrees')

  printer.tabPositions([3, 32])
  for plu in plus:
      printer.text(plu.quantity)
      printer.tab()
      printer.text(' x ' + plu.name)
      printer.tab()
      printer.text('$' + plu.price)

  printer.underline()
  printer.text('This text is underlined text')
  printer.lf()
  printer.underline(True,True)
  printer.text('This text is double dot width underlined text')
  printer.lf()
  printer.underline(False)
  printer.text('This text is not underlined')
  printer.lf()

  printer.upsideDown()
  printer.text('This text is upside down')
  printer.lf()
  printer.upsideDown(False)
  printer.text('This text is not upside down')
  printer.lf()

  printer.horizontalPosition(100)
  printer.text('This text starts at 1/6inches from left margin')

  printer.cutPaper()

  printer.drawerKickPulse()
