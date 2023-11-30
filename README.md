# Antigen-Scanning-App
This is a custom-built python executable intended to drive a USB-connected barcode scanner that stimulates input.

To run properly, double click barcode-scanner-app.exe in file explorer, or run barcode-scanner-app.exe as a powershell command.

This executable was packaged with Pyinstaller. Pandas, Tkinter, Numpy, and pandastable libraries support my code, which is contained a separate private repository for increased security. 

The purpose of this app is to validate and manage an inventory of analyte-specifc reagents. This app requires a unique .xlxs file with the column headers 'Allergen','PartNumber','LotNumber','Concentration','96wellLocation','48wellLocation','DilutentmL','AllergenNeeded','CoatingConcentration','predilution','UniqueID', and 'quantity'.

Column headers are case sensitive variable names with no spaces or special characters. The app consumes data from the provided file as a pandas dataframe, and will fail to validate barcodes if the above column names are not included on the user input file. 

Once the user has selected an Excel file, they can then begin scanning. The USB Barcode scanner converts the scanned code into raw text, which is passed into the app as a pandas dataframe object. The app will search the 'UniqueID' column for a matching value in the frame. If the provided barcode is in the frame, the GUI will display a 'Match', and relevant data will appear. If the provided barcode is not in the frame, the GUI will display a 'Miss', and a placeholder row will appear containing the scanned ID. 

When a match is identified, the app will also adjust the 'quantity' column in the row containing the matching ID to track inventory. This is the only instance where the app changes the input file. 

When scanning is complete, the user may attempt to close the program. The GUI will prompt you to select an output file in .xlxs format that will contain the rows of specified data scanned during the session where the app is running. Failure to select an output file before closing file explorer will cause session-specific information to be lost. 

The app is designed to prevent you from over-writing the provided file so that critical information is not lost, but pre-existing files not used while the program is running can still be irrecoverably replaced, so be cautious when choosing your export destination. 

Errors encountered while the program is being run can be viewed in console-log.txt when the program is stopped. 
