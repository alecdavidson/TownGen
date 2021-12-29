Randomly Generate details for a fictional civilizations using the civilizations name as a seed.
Currently only runs in CLI

To Do: 
* Figure out how existing Civs affect randomizer
* Create Application with TKinter

Summary of CivGen.py Class(es) and Functions using comments:

DBs
resources (Static DB)
civdb (Dynamic DB)

Class and Class Functions
class Civilization()
Define Civilization class
Initialize the class with variables matching the table headers from the DB

READ_DB(self)
Read the DB for existing Civilization
Format and execute SQL command to Civilization DB
Parse variable and extract values to store in self
Lists are more complex, store to temp variable
The main table stores the ID of the list, but not the values
Make a new connection and query the additional tables

SAVE_DB(self)
Save Generated town to the DB for future References
Save Racial Features to a seperate table on the DB
Get the ID of the entry we just created by making a query to sqlite_sequence table
Rinse and Repete with Proficiencies
And Again with Subclasses
Finally, for Civilization we do the same as above, but with the ID references stored instead of the actual data for the lists

UPDATE_DB(self)
If an existing entry was found, update that one instead of creating something new
Get ids for other tables
Starting with Racial Features, Update the table
You know the drill... Proficiencies
Yup... Subclasses
Finally... Civilization
Note, we store the IDs of the other tables instead of the full lists.

PRINT_CIV(self)
Organized Print out of the Civilization
It prints

GET_DB_RANDOM(self, table)
Get a single random entry from DB
Just need to know what table to use for the lookup
Get the total size of the table
Format for funcitonality
Grab Random entry
Most of these lists use name as their key
I decided it was a good idea to do Class/Subclass differently

BUILD_RANDOM_LIST(self, table, total)
Sometimes we need more than one entry for a field
Use for/while loops to check for duplicates

GEN_CIV(self)
Generate a Civilization using GET_DB_RANDOM and BUILD_RANDOM_LIST functions
Use the name of the Civilization as a seed for random
Set each single field using GET_DB_RANDOM
Set lists using BUILD_RANDOM_LIST
For better formatting, break up the returned Class/Subclass's

BUILD_CIVILIZATION(self)
Main function of the class
Store current values, they may contain manually entered values
Create a second Civ object with the same civ_name and execute GEN_CIV()
READ_DB() overwrites the values in self with anything stored in the DB
If this is a new generation (id==-1) or user requests a RESET, overwrite self with base
Now check for anything else manually entered
For the lists, we overwrite in order.
If RESET was entered, use base
If nothing was entered, use self
Both ifs will fail if something other than RESET is manually entered, and that value will be used

Global Functions
READ_LIST()
Get a list of all saved Civilizations
Connect to Civilizations DB and grab all civ_names
Parse through the returned data and restore for easier use

Execute
Parse the CLI for manually entered entities
Append nothing to the lists in order to match desired length

loop()
This loop funciton will be used to loop generation in the CLI
Display a list of all saved Civs
Grab Civ Name, all other fields will be generated randomly
Initialize object and build
Print out results
Set args.read to true to prevent additional generation

while False: loop()
If True run loop(), if False generate one Civ using any/all manually entered values
If args.read==True, display saved Civs and do nothing, else generate
Create object with CLI Arguments and Build
Print out results and ask to save/update