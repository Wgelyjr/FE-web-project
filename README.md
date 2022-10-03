# FE-web-project

The What:
___
This is a project I worked on at FarmersEdge, an application I developed mostly on my own.

At the lab, there's a central piece of software that we use for our Laboratory Information Management Software (LIMS). The LIMS handles sample tracking, managing the results of those samples, and employees and their permissions. The LIMS has an Access 2016 project front end over the top of an MsSQL backend, which allows for considerable extensibility, to the detriment of the software.

Some functions necessary for the operation of a laboratory are missing from the base software. These functions include (but are not limited to) the ability to generate a sequence of samples to be run on an analyzer, or to organize the tests of samples into batches for easier organization. To accomodate these shortcomings, a second application was built, called LabMacros. It handled sequencing and parsing analyzer-generated runfiles, but did not perform satisfactorily, nor was it able to be worked on in a collaborative manner. There was another application built in a similar manner for managing reports of orders.

To rectify these problems, I am constructing WebTools. It is accessible on the local network, and is a Flask application that will handle parsing and sequencing, and currently handles test batch tracking, report management, sample-checkin, and external order management. The scope of each of these functions is wide enough to not warrant description here, but since the apps are named cryptically, it will help navigation if I list their purposes:
___
The key:
___
Hyperion: Report Management/approval
BatchBack: Managing batch failures in the lab
FastSheet: Turns order information into a barcode. Used in tandem with TurboLog (Not included)
felutils: Handles log-in and homepage. Needs to be refactored
ChainLink: Communicates with FarmCommand API to manage external supply orders
___
The context:
___

This application runs on a Ubuntu Server VM that was already running Grafana-Server. I installed and configured Nginx, and created a process on the server that runs in a VENV on start, starts a Gunicorn HTTP server that listens on a socket file, and serves the Webtools app if the domain requested is webtools.local (need to change to webtools.lan.feapps.ca). It's deployed and working well.
___ 
Planned Features:
___
Sequencing and Parsing are next on the list - there are currently too many individual applications in use at the lab, and moving these from LabMacros will remove one. Next is Reagent Prep and Chemical Inventory tracking, then Maintenance Events. These are scoped for creation in 2023.
