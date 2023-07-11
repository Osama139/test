# RAD_DD-INS

## Description
RAD_DD-INS is a Python module that uses Selenium to interact with a website. It downloads and stores document and payment information from the "My Documents" and "My Payments" sections of the web portal, checks for duplicates, and logs activities in a MySQL database.

## Module Type
This module is a frontend web scraping tool, utilizing Selenium for web interactions.

## Module Architecture
RAD_DD-INS performs the following sequence of actions:

1. Establishes a connection with a MySQL database using credentials from a conn.txt file.
2. Uses Selenium's ChromeDriver to access and log into a specific web portal.
3. Verifies successful or unsuccessful login by checking for specific URLs.
4. Initiates a thread to check for specific web elements every three seconds and handle potential portal errors.
5. On the function being called, it navigates to the "My Documents" sections of the portal.
6. Filters and downloads relevant PDF files based on a given date range, passed as a parameter.
7. In the "My Documents" section, only two types of documents are targeted for download. The files are downloaded to a temp_folder. The module extracts data from downloaded files, checks for file duplication in the database, and deletes or moves files to downloads/stores files accordingly. Data for each downloaded file is also logged into the database.
8. On the function being called, it navigates to the "My Payments" sections of the portal.
9. In the "My Payments" section, required data is scraped from the webpage. Files are downloaded based on this information, and checked for duplication before storing in the database. File details are also logged.
10. At the end of each process, a message is printed specifying the number of files found and downloaded.
11. Finally, the temporary folder created is deleted.

## Usage Instructions

### Running with a Software
This module is intended to be run by a RAD service. The RAD service monitors the status of the module in the `ddb_processor` database. If the status of this module is "queue", the RAD service initiates the execution of the module, passing the required parameters for its execution.

### Running Locally
To run the module locally, ensure the virtual environment is set up with all necessary dependencies. 

Two important files are required:

1. `conn.txt` - A text file that contains the database connection details.
2. `.bat file` - A batch file that should include all necessary parameters to run the module. 

Following are the parameters needed to be passed:

- User name
- Password
- Location ID
- Facility ID
- Folder address
- Customer name
- Group name
- Location name
- fkprocID
- Nameclature
- Date difference
- NPI
- Insurance URL
- Debug
- API timeout
- API tries
