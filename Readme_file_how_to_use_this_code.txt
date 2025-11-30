Overview of the Script Purpose
This script imports data from a source sheet in a possibly different spreadsheet, merges additional remarks tied to each unique lead ID, and writes the combined data into a main sheet. It also stores and updates remarks separately in a hidden sheet ("RemarksDB"). The script includes a custom menu item "ImportSync" with a "Sync Now" command to run the sync process manually.

Step-by-Step Usage Instructions
Set up Configurations:
Update only the top portion of the script:

SOURCE_SPREADSHEET_ID: The ID of the spreadsheet containing the source data.

SOURCE_SHEET_NAME: The sheet name in the source spreadsheet where data resides.

MAIN_SHEET_NAME: The sheet name in the current spreadsheet where merged data and remarks will be stored.

STORE_SHEET_NAME: The sheet where remarks data will be saved (usually hidden).

leadIdColumn: The column number (e.g., 1 for column A) that contains the unique identifier (lead ID).

remarksColumns: Number of remark columns to maintain for each lead.

Add the Script to Your Spreadsheet:
Open your Google Sheet, go to Tools > Script Editor, paste the entire code, and save it.

Trigger the Script Menu:
When you open the spreadsheet, the onOpen simple trigger adds a custom menu called "ImportSync" in the Google Sheets UI. This menu contains the item "Sync Now" which calls the main sync function.

Run the Sync Process:
Click the "ImportSync" menu and select "Sync Now" to execute syncDataWithRemarks(). The script will:

Load source data from the configured source sheet.

Load existing remarks from the hidden "RemarksDB" sheet.

Also load any current remarks from the main sheet (to preserve recent edits).

Merge the source data with the remarks.

Write the combined data back into the main sheet.

Update the remarks database sheet with the latest remarks.

Show an alert when synchronization is completed.

Data Flow Explained:

The script retrieves rows from the source sheet.

It gathers remarks keyed by the lead ID from the "RemarksDB" store and the main sheet (latest edits).

It merges remarks next to corresponding source data rows.

Writes this merged dataset to the main sheet, retaining all data plus remarks.

Saves the updated remarks back in the hidden store sheet for future syncs.

Important Notes
The onOpen() function automatically loads the custom menu on spreadsheet open, enabling manual sync.

The safe() helper function ensures invalid or error values do not interfere during data processing.

The remarks stay persistent even when the source data changes because they are stored separately and merged back each time.

The script clears the main sheet contents before rewriting all data safely.

This setup ensures that your source data can be regularly imported and synced with additional remark columns you maintain manually, without losing those remarks after sync.

The onOpen function creates a custom menu when the spreadsheet opens, which lets you run this sync process conveniently.​​