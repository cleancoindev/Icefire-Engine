# Icicle-Engine v0.1
A non-programmer-friendly game engine for creating Quest-like, cross-platform Text Adventure games.

## Features
* Both the Editor and the resulting Game run in the browser, so they're truly cross-platform: if your device can run Chrome or Firefox, it can run the Icicle Engine.
* Non-programmer-friendly: The engine includes code templates. If you've ever used software like GDevelop, Construct 2 etc. you should feel right at home - it's just a tiny step-up.
* Lightweight: An empty game is only about 40KB!
* Powerful: You can extend the built-in functionality with your own JavaScript, so there's no limits to what you can do!

## Known Issues
* Quotes cannot be used in the text of hyperlinks. Instead of ", please use \&quot; for now (if you use the code templates, you don't have to worry about that - they're all replaced automatically for you).
* Room names cannot be changed dynamically - you can name a room immediately when the player enters it, but don't trigger this function after any sort of click (e.g. player clicks on hyperlink or interacts with an object) as it will break the game.

## Planned Additional Features
* Support for Audio
* Support for Images
* Support for Timers
(All the above can be used right now only if you're familiar with HTML and JavaScript.)

# How to Run the Program
Download and extract the ZIP file of the latest release or the repository itself. Open the file "Editor/Icicle Editor.html" in either Chrome or Firefox - no other browsers have been tested. This will bring up the game editor - it runs in your browser, fully offline.

# How to Use the Editor
The editor is made up of 3 tabs - the "Map" tab, the "Room Script" tab and the "Publish Game" tab.

## Map
This is the map view of the game. Here, all you do is simply click on the room you wish to edit and then go to the "Room Script" tab to make changes to the room.

The following buttons are available to use to help you do this:
* Go to: Lets you enter (x,y,z) coordinates of the room you wish to go to.
* Up: Increases the current z-coordinate by 1 to let you see the layer above the current one.
* Down: Decreases the current z-coordinate by 1 to let you see the layer below the current one.
* Delete: Deletes the currently selected room. If the room is linked to other rooms, these will remain unaffected. If other rooms link to this one, they too will remain unaffected.
* Zoom in/Zoom out: Lets you zoom in/out on the map.

## Room Script
This is the Script View of the currently selected room. Any JavaScript entered here will be executed each time the player enters this room.

The following buttons are available to help you script your game:
* Add action: This button contains the code templates for everything you need to make a game. This will automate the scripting process for you and so is useful if you are not a programmer, are unfamiliar with JavaScript, want to avoid syntax errors or simply can't be bothered to learn any of the in-built functions. Using these templates will also make your life easier - the PRINT command, for example, lets you type in the scene description using Markdown rather than raw HTML. More on scripting later.
* Edit: Lets you edit a PRINT command that's already been added to the code editor. Just put the cursor on the line containing the command you wish to edit, click the button and the HTML will be rendered back to Markdown for you to edit. Once you're finished, press OK and the command will be updated accordingly. WARNING: The PRINT command must be the only command on the line. You will get an error if there are other commands on this line.
* Check syntax: This will carry out some checks to make sure the syntax of your JavaScript is valid, and tell you where there is an error if there is one.
* Increase/Decrease font size: Self-explanatory.

## Publish Game

This tab contains 4 options:
* SAVE PROJECT: This option allows you to export your project as a JSON file and save it locally on your machine.
* OPEN PROJECT: This option allows you to open a saved project on your machine. Accepts JSON format.
* EXPORT GAMESCRIPT: This is only to be used if you are an experienced programmer and wish to make changes to the Runtime Engine. More on this later.
* PUBLISH GAME: Exports your game as a single, ready-to-play HTML file.

# Scripting your Game

Click on any room on the map which you wish to edit and script what is to happen in the room in the "Room Script" tab. Any JavaScript entered there will be run whenever the user enters that room. To insert an action into the room's script, press the plus button in the top left corner of the "Room Script" tab.

Below we will go through all the available actions:

## Text
* PRINT TEXT: This action will print text into the console. Use this to show scene descriptions and, in general, communicate with the player. There should ideally be a PRINT command executed after every user interaction so that they know what's going on.
* CLEAR ALL TEXT: Clears the console of all text. Use this to clean up a bit when, for example, the player gets to another level in the game. Clearing the console can also speed the game up a bit if the user has been playing it for a while and it has become cluttered.

## Hyperlinks
* PRINT HYPERLINK: Prints a hyperlink onto the screen. You can customize what happens when the player clicks on it.
* DISABLE ALL PRINTED HYPERLINKS: Disables all hyperlinks currently in the console. Any hyperlinks added in the future are not affected.

## Map
* ROOM NAME: Changes the name of the room on the map. This is visible to the player, but is also rendered onto the map in the Icicle Editor itself to help you keep track of what is where.

## Exits
* ADD EXITS: Whenever a player enters a room, all exits are locked. This command lets you unlock any exits you wish so that the player can exit the room through them.
* REMOVE EXITS: Locks any exits you wish so that the player cannot exit the room through them.
* TELEPORT TO: Teleport the player to any room in the game.

## Surroundings
* ADD OBJECT TO SURROUNDINGS: Adds an object (e.g. banana) to the current room. Objects in the room are deleted automatically when the player leaves the room, i.e. the game doesn't keep track of the objects; if you want the player to be able to take an object, you must store this info in a variable and only add this object to the room if the player hasn't taken it.
* REMOVE OBJECT FROM SURROUNDINGS: Removes an object from the current room.
* ADD ACTION TO OBJECT: Adds a custom action to an object in the current room (e.g. eat). Fully customizable.
* REMOVE ACTION FROM OBJECT: Removes an action from an object in the room.

## Inventory
* ADD OBJECT TO INVENTORY: Adds an object (e.g. banana) to the player's inventory. If it already exists in the player's inventory, it increases the count of the object in the player's inventory.
* REMOVE OBJECT FROM INVENTORY: Removes an object from the player's inventory. If there's more than one of these objects there, it simply reduces the count by 1.
* ADD ACTION TO OBJECT: Adds a custom action to an object in the player's inventory. Fully customizable.
* REMOVE ACTION FROM OBJECT: Removes an action from an object in the player's inventory.

## Statistics
* ADD PLAYER STATISTIC: Makes a variable visible to the user. You can also add a unit to display the variable with (e.g. %);
* REMOVE PLAYER STATISTIC: Hides a variable from the user. All variables are hidden by default.

## Game
* END GAME: Kills the current game so that the player cannot do anything anymore, only restart the game or load a game.

## Variables
This is intended only for non-programmers. If you are familiar with JavaScript, you won't have to use this. But remember - all variables you use must be assigned to the global 'pl' object, otherwise they won't be saved by the in-built game-saving mechanism. Local variables can still be defined with 'var' if you plan on using them only in one room.

## If Statements
Again, these are only intended for non-programmers. These allow you to execute commands only if certain conditions are met.
* IF...: If certain conditions are met, then do (whatever you wish).
* ELSE IF...: Must only be used after an IF... statement. Allows you to define an alternative scenario.
* ELSE...: Must only be used after either an IF... or an ELSE IF... statement. This will get executed if any previous IF... and ELSE IF... statements fail to execute (i.e. if their conditions are not met).

# Customizing the Game
If you wish to customize the final game (e.g. change the default colours), navigate over to the folder called Runtime Engine. The files "engine.html", "engine.css" and "engine.js" all together form the (unminified) runtime engine. The other file, "definitions.js", contains the gamescript. So all you need to do is export your game from the Editor using the "EXPORT GAMESCRIPT" option and overwrite the "definitions.js" file with the output. Then, if you open "engine.html" in a browser, you'll have a working game. You can customize the other three files to your heart's desire.
