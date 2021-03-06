# AtlasMaker
![AtlasMaker](/media/atlasmaker-screen.jpg)

AtlasMaker is a Photoshop script for generating texture atlases and tile grids. In other words, it takes a directory full of images and arranges them into a single, larger image. It's intended primarily for game development, but can also be used to create CSS sprites for the web.

## Features
* Cross platform - tested in Photoshop CS3,CS4,CS5 on Windows and MacOSX.
* Open Source
* Several image sorting algorithms. Find the most efficient one for your textures.
* Add a margin to each image.
* Custom data file export
* Extendable - It's easy to add your own rectangle packing algorithms and sorting methods

## Installing AtlasMaker
There are two ways of running AtlasMaker in Photoshop.
Unzip atlasmaker to your photoshop scripts folder. On windows this is usually:
c:\Program Files\Adobe\Photoshop CSsomething\Presets\Scripts

On a Mac this folder is at:
Applications/Photoshop CSsomething/Presets/Scripts

When you next start Photoshop, AtlasMaker should appear in the File->Scripts menu.

Or you can run the script without installing by unzipping the AtlasMaker folder somewhere, selecting Scripts->Browse from the file menu and then selecting AtlasMaker.jsx

## Quick Start Guide
The first thing to do is select a directory of images by clicking "browse" at the top of the window. Once you have done this, AtlasMaker will scan through the images and collect size information about them.

You'll notice that some text will appear underneath "Number of Files". This is a notification from the Tile Grid Packer telling you how many rows and columns your images will take up given the default document size. Different packing methods provide different notification messages according to their nature.

Next, you want to select your packing method. If your images are texture maps of different sizes then you want to select the "Atlas Maker". If you are making a traditional 2d game where the sprites are all the same size, then you want to select the "Tile Grid"

Then you can optionally select a sorting method. Sorting the images in different ways can improve the efficiency of the texture atlas. Some packing methods do not allow sorting, and will disable this option if they are selected.

You can also add a margin here if you want a gap between your textures. Margins are added on to the width and height of each image just like CSS margins.

Next, click "Document Settings" and you will be able to set the size of the texture atlas you are going to create. You can also set the document name here, and choose if you want to flatten all the layers into one, once the atlas is complete.

Now click "Create Atlas" and you're done.

## AtlasMaker Reference Guide
* Interface Overview
 * File selection and notification area
 * Panel selection area
 * Atlas settings panel
 * Destination image panel
 * Export file panel
* Extending AtlasMaker

### Interface Overview
The AtlasMaker interface is split into three main parts. The source file selection and notification area is at the top of the window. Below that are the texture atlas options, which have been split into three panels to save space. You can flip between each panel by clicking on the items in the panel selection area on the left hand side.

At the very bottom of the window are three self explanatory buttons. About, Create Atlas and Cancel.

### File Selection and Notification Area
At the top of this area is the file selector. clicking "browse" will open a file requester that you can use to select the directory containing the images you want in your atlas. AtlasMaker will then scan through the images and make some initial calculations. AtlasMaker can load any images photoshop can. Any non-image files in the selected folder will be ignored.

Underneath the file selector is the notification area. It contains the following information:

Number of Images: How many image files are in the source directory.
Pages: How many pages, or individual texture atlases will be needed to hold them. 

The notification area can contain information provided by different packing methods. If you select the "Tile Grid" packer, you will see how many rows and columns the grid will be. The kind of notifications that appear here will depend entirely on the packing algorithm.

Items in the notification area may change when you edit atlas options.

### Atlas Settings Panel
Packing Method: This dropdown contains the available packing methods. By default there are 2: "Tile Grid" and "Texture Atlas"

Sorting Method: This dropdown lets you choose how images are sorted before being put in the atlas. Different settings can result in better atlas generation depending on your data.

Reverse Sort: Tick this checkbox to perform the selected sorting method in reverse.

Rotate: Not implemented yet. In the future, AtlasMaker will be able to rotate images for improved packing.

Margin: You can add a margin of any number of pixels around each image in the atlas. It works just like CSS margins.

### Destination Image Panel
Document Name: Set the Photoshop document name (not the filename) of the destination image. If you have multiple images, use the tag #n to substitute the page number into the text.

Width: The destination image width in pixels
Height: The destination image height in pixels

Merge Layers: By default, AtlasMaker will give each texture its own layer in the destination image. If this is checked, they will be merged down into a single layer.

Fill Background Layer with Background Color: This will create a filled background layer using whatever background color you have set in Photoshop.


### Export File Panel
If you tick the “Enable datafile export” checkbox, AtlasMaker will create a text file, containing a chunk of text for each texture. Each chunk is generated from the text in the "Line Template" box. Tags are used to substitute information about each image into the text:

**\#i** - Image index (0.. number of Images in directory)

**\#filename** – Filename of source image

**\#width** – Sprite width

**\#height** – Sprite height

**\#x** – X position of top left corner on spritesheet

**\#y** - Y position of top left corner on spritesheet

**\#p** – page number

Lets say your game engine loads textures or sprites like this: “TextureManager->GetSprite(x,y,width,height);” and you have 50 images to load. You can generate all 50 calls by entering the following into the line template box:

TextureManager->GetSprite(#x,#y,#width,#height);

AtlasMaker will then generate 50 lines containing the correct coordinates and dimensions for each Image.

You can enter multi-line text chunks, to create XML fragments for example, but you must use ctrl-enter for each newline.

Export File Name  - Browse: Use this to select the name and location of your export file

Reorder Export file: You can change the order of the images in the export file. This allows you to group related images together wherever they are on the atlas.

Clicking the button will open a window listing all the image files. You can select image files and move them around by clicking "up" or "down". You can shift-click to select multiple images and move them as a group.

