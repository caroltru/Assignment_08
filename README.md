#------------------------------------------#
# Title: Assignmen08.py
# Desc: Assignnment 08 - Working with classes
# Change Log: (Who, When, What)
# DBiesinger, 2030-Jan-01, created file
# DBiesinger, 2030-Jan-01, added pseudocode to complete assignment 08
# Caroline Truong, 2021-Dec-05, updated assignment 08 tasks
# Caroline Truong, 2021-Dec-06, completing assignment 08, presentation section
#------------------------------------------#

# -- DATA -- #
strFileName = 'cdInventory.txt'
lstOfCDObjects = []

class CD(object):

    """Stores data about a CD:

    properties:
        cd_id: (int) with CD ID
        cd_title: (string) with the title of the CD
        cd_artist: (string) with the artist of the CD
    methods:

    """
    # TODOne Add Code to the CD class
    #--Fields--#
    cd_id = int()
    cd_title = ''
    cd_artist = ''
    
    #--Constructor & Attributes --#
    def __init__(self, ID, Title, Artist):
        self.__cd_id = ID
        self.__cd_title = Title
        self.__cd_artist = Artist
        
    #--Properties--#
    @property
    def cd_id(self):
        return self.__cd_id
    
    @cd_id.setter
    def cd_id(self, value):
        if str(value).isnumeric():
            self.__cd_id = value
        else:
            raise Exception('ID must be an integer.')

    def cd_title(self):
        return self.__cd_title
    
    @cd_title.setter
    def cd_title(self,value):
        if str(value).isnumeric():
            raise Exception('Please exclude numbers from CD title.')
        else:
            self.__cd_title = value
            
    def cd_artist(self):
        return self.__cd_artist
          
    @cd_artist.setter
    def cd_artist(self,value):
        if str(value).isnumeric():
            raise Exception('please exclude numbers from CD artist.')
        else:
            self.__cd_artist = value
    
    #--Methods--#
    pass
# -- PROCESSING -- #
class FileIO:
    """Processes data to and from file:

    properties:

    methods:
        save_inventory(file_name, lst_Inventory): -> None
        load_inventory(file_name): -> (a list of CD objects)

    """
    
    @staticmethod
    def add_inventory():
        """Asks user for new ID, CD Title and Artist
        
        Args: None.
        
        Returns: new ID, CD Title, Artist Name
        """
        strID = input('Enter ID:').strip()
        strTitle = input('What is the CD\'s title?').strip()
        strArtist = input('What is the Artist\'s name?').strip()
        return strID, strTitle, strArtist
                 
    
    # TODOne Add code to process data from a file
class DataProcessor:
    """Processing the data to and from text file"""

    @staticmethod
    def read_file(file_name, table):
        """Function to manage data ingestion from file to a list of dictionaries

        Reads the data from file identified by file_name into a 2D table
        (list of dicts) table one line in the file represents one dictionary row in table.

        Args:
            file_name (string): name of file used to read the data from
            table (list of dict): 2D data structure (list of dicts) that holds the data during runtime

        Returns:
            None.
        """
        table.clear()  # this clears existing data and allows to load data from file
        try:
            with open(file_name, 'r') as objFile:
               print(objFile)
            objFile.close()
        
        except FileNotFoundError:
            print('File not found.')
        
         
    @staticmethod
    def add_file(strID, strTitle, stArtist):
        """ Function to add new item to the table.
        
        Adds user provided information to the 2D table.
        
        Args:
            
            
        Returns:
            None.
        """
      
        try:
            intID = int(strID)
        except ValueError:
            print('\nID is invalid. Please enter an integer.')
            
        dicRow = {'ID': intID, 'Title': strTitle, 'Artist': stArtist}
        lstOfCDObjects.append(dicRow)

            
     # TODOne Add code to process data to a file
       
    @staticmethod
    def write_file(file_name, table):
        """Function to save data from list of dictionaries to file
        
        Writes the data from 2D table (list of dictionaries) per row and saves it to file.
        
        Args:
            file_name (string): name of file used to read the data from
            table (list of dict): 2D data structure (list of dicts) that holds the data during runtime

        Returns:
            None.
        """
        objFile = open(strFileName, 'w')
        for row in lstOfCDObjects:
            lstValues = list(row.values())
            lstValues[0] = str(lstValues[0])
            objFile.write(','.join(lstValues) + '\n')
        objFile.close()
        

# -- PRESENTATION (Input/Output) -- #
class IO:
    # TODOne add docstring
    """IO represents input and output data processes."""
       
    # TODOne add code to show menu to user
    @staticmethod
    def print_menu():
        """Displays a menu of choices to the user

        Args:
            None.

        Returns:
            None.
        """

        print('Menu\n\n[l] load Inventory from file\n[a] Add CD')
        print('\n[s] Save Inventory to file\n[x] exit\n')    
    
    # TODOne add code to captures user's choice
    
    @staticmethod
    def menu_choice():
        """Gets user input for menu selection

        Args:
            None.

        Returns:
            choice (string): a lower case sting of the users input out of the choices l, a, i, d, s or x

        """
        choice = ' '
        while choice not in ['l', 'a', 's', 'x']:
            choice = input('Which operation would you like to perform? [l, a, s or x]: ').lower().strip()
        print()  # Add extra space for layout
        return choice
    
    # TODOne add code to display the current data on screen
    
    @staticmethod
    def show_inventory(table):
        """Displays current inventory table


        Args:
            table (list of dict): 2D data structure (list of dicts) that holds the data during runtime.

        Returns:
            None.

        """
        print('======= The Current Inventory: =======')
        print('ID\tCD Title (by: Artist)\n')
        for row in table:
            print('{}\t{} (by:{})'.format(*row.values()))
        print('======================================')

    # TODOne add code to get CD data from user
    
    @staticmethod
    def add_inventory():
        """Asks user for new ID,CD Title and Artist
        
        Args: None.
            
        Returns: new ID, CD Title, Artist Name
        
        """
        try:
            strID = (int(input('Enter ID: ').strip()))
            strTitle = input('What is the CD\'s title? ').strip()
            strArtist = input('What is the Artist\'s name? ').strip()
            return strID, strTitle, strArtist
        except ValueError:
            print('Please enter an integer.')
        
    
# -- Main Body of Script -- #
# TODOne Add Code to the main body
# Load data from file into a list of CD objects on script start

FileIO.read_file(strFileName, lstOfCDObjects)

# Display menu to user
while True:
    IO.print_menu()
    strChoice = IO.menu_choice()   
    
    # show user current inventory
    IO.show_inventory(lstOfCDObjects)
    
    # let user add data to the inventory
    if strChoice == 'a':
        strID, strTitle, stArtist = IO.add_inventory()
        DataProcessor.add_cd(strID, strTitle, stArtist)
        IO.show_inventory(lstOfCDObjects)
        continue  # start loop back at top.
      
    
    # let user save inventory to file
    elif strChoice == 's':
        IO.show_inventory(lstOfCDObjects)
        strYesNo = input('Save this inventory to file? [y/n] ').strip().lower()
        # 3.6.2 Process choice
        if strYesNo == 'y':
            # 3.6.2.1 save data
            FileIO.write_file(strFileName, lstOfCDObjects)
        else:
            input('The inventory was NOT saved to file. Press [ENTER] to return to the menu.')
            IO.show_inventory(lstOfCDObjects)
        continue  # start loop back at top.  
        
    # let user load inventory from file
    
    if strChoice == 'l':
        print('WARNING: If you continue, all unsaved data will be lost and the Inventory re-loaded from file.')
        strYesNo = input('type \'yes\' to continue and reload from file. otherwise reload will be canceled')
        if strYesNo.lower() == 'yes':
            print('reloading...')
            FileIO.read_file(strFileName, lstOfCDObjects)
        else:
            input('canceling... Inventory data NOT reloaded. Press [ENTER] to continue to the menu.')
            IO.show_inventory(lstOfCDObjects)
        continue  # start loop back at top.
        
    # let user exit program

    if strChoice == 'x':
        break

