# File Mapper
> An easy way to copy/move/symlink files from one directory to the other!

### Intended Purpose

This program is designed to help users to copy, move, symlink files from one directory to another using a JSON file. The key values being the source of the files and the value to the keys being the desired destination. This program has been designed to move important files from a large dataset and would be applicable in several of the BIDS datasets. The file_mapper GUI makes the mapping process easier by allowing users to check off what files/directories they want mapped and browse the file system to pick a directory for the destination.  

### Installation

* Make sure python 3 is installed.
* Clone file_mapper repo

### Usage of GUI

1. Call the ***`file_mapper_gui`*** using the command ***`python file_mapper_gui`*** 
2. A popup window should emerge and the window prompts the user to select a folder to either copy, move, or symlink files

![Initial Window](img/window1.png)

3. Once the folder is selected, the open button should be pressed to move to the next stage of the GUI
4. A second window will emerge prompting the user to select individual files in the selected folder to add to the JSON.

![Checkbox Window](img/window2.png)

5. Once desired files/folders are selected and the OK button has been pressed, another window will pop up

![Checkbox Window 2](img/window2check.png)

6. The final window prompts the user to name the JSON file that will be interpreted by the file_mapper_script

![Final Window](img/window3.png)

    Note; when naming if "**.json**" is not added to the end of the name it will automatically be added by the file_mapper_gui
   
   
7. Once naming is complete, press the save button and a popup will notify the user that ***`JSON created successfully`***
   
    ![Success](img/creation.png)
 
    * If the JSON exists and is being overwritten then another popup will be displayed. 
 
    ![Replacement](img/replace.png)
 
    * If an error arises, the GUI will display ***`JSON creation process was not successful. Please try again.`****

### Usage of Script

1. Make sure that the JSON file that is being interpreted takes paths as its keys and values  

  * If the keys/values are relative paths, make sure a SOURCE key and a DESTINATION key so that their full paths can be provided.
  * If the keys/values are absolute paths the file will run normally.

2. To run the file, call ***`python file_mapper_script.py [absolute path to the JSON file] -a [The choice of 3 actions copy/move/symlink]`***  

  * The absolute path to the JSON file needs to be provided without a tag so the program can locate the file to process.
  * The -a (--action) tag allows the user to choose between moving, copying, or symlinking.  
      - The default is to copy
  * If the path has already been made, and an overwrite is needed, add the -o (--overwrite) tag.
  * If the overwrite is not provided and the file already exists then the console wil display ***`Destination file already exists [absolute path to the file]`***  
  * If overwrite is successfull then the console will display ***`file has been overwritten`***
  * If errors are to be skipped, the -s (--skip-errors) tag will skip errors and proceed to run the program.  
  * If a custom SOURCE or DESTINATION for the JSON file and its contents is required:

      - The -sp (--sourcepath) tag and the -dp (--destpath) tag allows the user to input a custom SOURCE or DESTINATION
      - The provided roots will overwrite the given roots in the JSON file and provide this message: `'Optional DESTINATION argument: 'path of the provided dest +' overrules destination: ' + initial given dest`

  * A verbose tag (-vb (--verbose)) can be used to display the print statements when the program is run.

      - Without the -vb tag the program will run without displaying any messages to the console

  * The testdebug tag (-td (--testdebug)) can be used to display to the console what the code does without executing it

      - The -td tag works with overwrite statements as well, displaying ***`overwrite_string + action + ': ' + src + ' -> ' + dest`***

  * If the keys/values are absolute paths the file will run normally.

3. If the file runs without error, the console will display a message for each path made: ***`Path has been made: (absolute path of file created)`***

  * If the JSON is not properly written the console will display an error message: ***`Invalid json: error`***


### Example

```
# Call function with relative path to json and action for mapping along verbose mode to show print statements
user@server:~/file-mapper$ ./file_mapper_script.py ./testing.json -a copy -vb

# The SOURCE is included in the json as a key: value path
Source already exists in json data
DESTINATION not provided, using prexisting values in JSON

# Message to show that the path has been made
Path has been made: /example/mapped/path
Source already exists in json data
DESTINATION not provided, using prexisting values in JSON
Source already exists in json data
DESTINATION not provided, using prexisting values in JSON
```
