# CUPS

## Introduction

CUPS is the standard printing system for Unix and Linux. CUPS offers several ways to configure printers. We'll use the web interface and the command line to configure a printer and print a manpage using Ghostscript.

## Learning Objectives

*When you have successfully completed this assignment you will be able to:*

1. Install the CUPS printer server.
3. Add a printer using the CUPS web interface.
4. Add a printer from the command line.
5. Print a file from the command line.

## Terms You Should Know

- **CUPS:** Printing service for Linux and Apple.
- **/etc/cups/cupsd.conf:** Main CUPS configuration file.
- **IPP:** Internet Printing Protocol
- **lp:** Line Printer
- **lpq:** Line Printer Queue
- **lprm:** Remove a print job.
- **lpstat:** Check the status of printers. Use **-a** to list all.
- **lpadmin:** Configure CUPS from the command line.
- **lpinfo:** Lists the drivers CUPS supports.
- **ppd:** PostScript Printer Description
- **PostScript:** Page description language
- **Ghostscript:** A free implementation of PostScript

## Preparation

For this assignment you'll use the web interface to CUPS to install a network printer on Ubuntu and then use the command line to install the classroom printer on CentOS 7. Set networking in VirtualBox for both virtual machines to *Bridged* and refresh the MAC address before starting the virtual machines. Both virtual machines must be on the 192.168.201.0/24 network to reach the printer.

## Internet Printing Protocol

The HP LaserJet 4250 in the classroom supports direct printing over the network. You can access the printer from a web browser at this address.

    http://192.168.201.221

## Adding a Printer Through Firefox

CUPS listens on port 631 for connections from *localhost*. This makes it possible to administer CUPS from a web browser.

## Open the CUPS Administration Page

Connect to CUPS on port 631 from Firefox. Enter this URL in the address bar.

    http://localhost:631

Click the Administration link and enter tux's authentication.

## Add a Printer from the Web Interface

1. Select *Add a Printer*.
2. You should see the HP LaserJet 4250. (If not, See next section.)
2. Click *Continue* and enter a location for the printer, BA1E.
4. Click *Continue*.
5. From the Model list select HP LaserJet 4250 Foomatic/Postscript.
6. Click *Add Printer*
7. Click *Query Printer for Default Options.*
8. In the Administration drop-down menu on the next screen select *Set as Server Default.*
9. From the Maintenance drop-down menu select *Print Test Page*. 

### If Network Printer Isn't Detected

If the network printer isn't automatically detected select IPP Printing from the list and enter **socket://192.168.201.221:9100** as the printer URL.Then follow the instructions above.

## Configure CUPS From the Command Line (CentOS Minimal)

### Install the CUPS Print Server

Use Yum to install the CUPS print server and the PPD files for HP printers..

    # yum install cups hpijs

### Is the Service Running?

Open a terminal and as root check the status of the CUPS service.
  
    # systemctl status cups.service
    
If CUPS is *inactive* start the service.
  
    # systemctl start cups.service

### Set CUPS to be Enabled on Boot

Starting CUPS is not enough if you want to service active all the time. Use this command to set CUPS to start on boot.

	# systemctl enable cups.service

### Add a Printer
    
The `lpadmin` command is used to configure CUPS from the command line. You'll need to run `lpinfo` to find the proper **ppd** file for your make and model printer.

#### Find the Correct ppd File

	# lpinfo -m | grep 'LaserJet 4250'
    lsb/usr/HP/hp-laserjet_4250-ps.ppd.gz

#### Add the Print Queue

Use `lpadmin` to add the printer (print queue). At the end of each line type the backslash character and then **Return** for Bash to accept that line and start a new line. The Bash shell will place a new prompt **>** for you to continue. *Note:* Double check your quotes before pressing **Return.**

	# lpadmin -p "hp_laser" -E \  
    -v socket://192.168.201.221 \  
    -m "lsb/usr/HP/hp-laserjet_4250-ps.ppd.gz" \  
    -D "This line is for information only." \  
    -L "Set the location here"
    
Press **Return** after the last line wait a minute until the prompt returns.

#### Check that the printer is ready

	# lpstat -a
    hp_laser accepting requests since. 

#### Set the Default Printer

Set the printer as the default so you don't need to type the printer name each time you want to print.

    # lpadmin -d "hp_laser"
    
The output should say that the printer is accepting requests.

The `lpq` command confirms the printer is ready and set as default.

	# lpq
    hp_laser is ready
    no entries
    
## Print from the Command Line

### PostScript

PostScript is a page description programming language. It creates a plain text file that describes how to put the characters on the page based on the properties of the ppd file used. You can test this by creating a Postscript file (on the workstation not the virtual machine) and opening the text file with `less`.

	# man -t pwd > pwd.ps
	# less pwd.ps

### Print a Man Page

This command will send a PostScript file to the default printer.

    # man -t pwd | lp

<!--## Convert PostScript to PDF.

Portable Document Format or PDF is derived from PostScript. You can convert a PostScript file to a PDF with `ps2pdf`.

    $ ps2pdf pwd.ps
    $ epdfview pwd.pdf
-->

## Debug the Assignment

1. Plenty of chances for typos in this assignment.
2. If after running `lpstat -a` you get an error that the printer is not accepting requests you probably did not enable the printer by omitting `-E`.
3. The printer name should be one word, lower case                                                 

## What to Submit

Turn in the manpage *you* printed with your name on it.

## Resources

- [Remote Access to CUPS Web Interface][arch]
- [Postscript vs. PDF][ps]
- [Ghostscript][gs]

<!-- Links

This is [an example](http://example.com/ "Title") inline link.
This is [an example][id] reference-style link.
[id]: http://example.com/  "Optional Title Here"
![alt text](/path/img.jpg "Title")
![alt text][id]
-->
[firewall]: https://s3.amazonaws.com/CIS126DL/Images/firewall_ipp.png "Firewall"
[xkcd]: https://sslimgs.xkcd.com/comics/3d_printer.png
[arch]: https://wiki.archlinux.org/index.php/CUPS#Remote_access_to_web_interface "Remote Access to CUPS Web Interface"
[ps]: http://adobe.com/print/features/psvspdf/ "Postscript vs. PDF"
[gs]: http://www.ghostscript.com "Ghostscript"

> Written with [StackEdit](https://stackedit.io/).<!--se_discussion_list:{"5Ipq54IaAWrIyMkX9TVBHINU":{"selectionStart":25,"selectionEnd":29,"commentList":[{"content":"This assignment won't work unless done in the classroom. Can't be done at home over wiFi probably."}],"discussionIndex":"5Ipq54IaAWrIyMkX9TVBHINU"}}-->