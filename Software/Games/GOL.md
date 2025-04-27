# Game of Life
| File | Description |
|---|---|
| [GOL.z80](GOL.z80) | Assembly File |
| [GOL.hex](GOL.hex) | Intel HEX File |

## Description
The Game of Life is not your typical computer game. It is a cellular automaton, and was invented by Cambridge mathematician John Conway.

This game became widely known when it was mentioned in an article published by Scientific American in 1970. It consists of a grid of cells which, based on a few mathematical rules, can live, die or multiply. Depending on the initial conditions, the cells form various patterns throughout the course of the game. 

## Requirements
You will need the **RGB 8x8 Matrix Display** to see the Life patterns play out.

## How to Play
Different starting patterns can be selected by pressing different keys on the keypad. Key 0 will generated a random starting pattern.

**Rules**

*For a space that is populated:*
- Each cell with one or no neighbors dies, as if by solitude.
- Each cell with four or more neighbors dies, as if by overpopulation.
- Each cell with two or three neighbors survives.

*For a space that is empty or unpopulated:*
- Each cell with three neighbors becomes populated.

## Loading Instructions
[Download the Intel HEX File](GOL.hex) to your PC, then use a **Serial Terminal Program** like *CoolTerm* to download the HEX file to your TEC-1G via a **USB Cable**.
Use the **MON3 Intel HEX Load** to load the program. After loading, exit the Main Menu by pressing **AD** on the Hexpad or **ESC** on the Matrix Keyboard, which will take you to the address ``4000H``. Press the **GO** button, or the **ENTER** key on the Matrix keyboard to start the program.

## Code
[Download the Assembly Language File](GOL.z80) and examine or change the code and compile your own flavour. If you make any significant changes, consider providing an update to this repo.

### Suggested Modifications
- Life Counter:  Count how many cycles a "civilisation" lives before going extinct or becoming stable.
- Coloured Display:  Show which lives are going to die of Overcrowding (Red) or Loneliness (Blue)
- Editor:  Allow the player to edit the start screen, being sure to save the data and recall it so they can tweak a design.

### High Score
Take a photo of the Setup of your Civilisation and how many Life Cycles it survived.
We will post results here!
