# Introduction 
This is a simple console application built for sending files to GDB (VINN or KRITA) at Statistics Sweden. It's main purpose is to show how files can be sent using the M2M-api.
Please read the entire documentation at:
https://www.scb.se/vinn
or
https://www.scb.se/krita

# Getting Started
The application is pretty simple. Point out your read directory and run the application. When you add a new file to the read directory it will post the file. It uses the directory structure to define the meta data. A certificate is used for authentication. Please contact VINN- or KRITA-support regarding the certificate.

1. Install the certificate on the machine, (as the same user running the application) - i.e. in the installation guide, choose active user, NOT local machine. 
2. Make sure that your `app.config` is correct. _(More information in the __Configuration__-section below)_
3. Create your folder structure. _(More information in the __Directory structure__-section below)_
4. Build the project.
5. Run the project.
6. Put the file you wish to send in _read directory_.
7. The application will send the file.

# Directory structure
The application is built to run on one server, but support differerent reportees/information providers. This is solved by using a strict directory structure to define which information provider the file belongs to. The structure is defined as such: `[read-diretory]\[organisationsnummer]\[fileformat]`

In reality it could translate to this: `C:\Temp\999000-0045\V40`

When running the application and you put a file in the directory above it will send the file as `999000-0045` and define the fileformat as `V40`. If you put the file in `C:\Temp` it will use the values in app.config instead.



# Configuration
All necessary configurations should be applied to `app.config`, mainly the `requestConfiguration`-section. The different parameters is described below:

* __ReadDirectory__ - This is the directory the application will scan for new files (including sub directories)
* __DoneDirectory__ - Sent files will be placed here after a successful post
* __CertificateSerialNumber__ - Serial number for the installed certificate. Note that the application will try to fetch the certificate as the user running the application. Currently as `new X509Store(StoreName.My, StoreLocation.CurrentUser)`. It's convenient when testing, but probably not suitable for production.
* __BaseUrl__ - Url for GDB M2M-api. Probably one of these:
 https://test.m2m.gdb.scb.se/m2m/v1
https://m2m.gdb.scb.se/m2m/v1
* __PingInterval__ - Used when you want to ping the api on a regular basis. Convenient when testing, but probably not suitable for production.
* __OrganisationNumber__ - Swedish Organisationnummer for the reportee. Eg. 9990000045. Not needed when using directory structure.
* __StatisticalProgram__ - Statististical program (Sv. undersökning). Either _VINN_ or _KRITA_. Not needed when using directory structure.
* __FileFormat__ - Type of form. Eg V40, V10, KRITA_MONTHLY. Not needed when using directory structure.
* __Version__ - Version of the form. Eg 1, 3, 5. Usually not needed at all, but the API supports it.

# Build and Test
Currently tests are not included in distributed solution.
