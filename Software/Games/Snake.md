# Snake
| File | Description |
|---|---|
| [Snake.z80](GOL.z80) | Assembly File |
| [Snake.hex](GOL.hex) | Intel HEX File |

## Description
Snake is a genre of action video games where the player maneuvers the end of a growing line, often themed as a snake. The player must keep the snake from colliding with both other obstacles and itself, which gets harder as the snake lengthens. 

## Requirements
You will need the **RGB 8x8 Matrix Display**

## How to Play
Use the Keys to move the Snake in the direction you want:
- Left:     0
- Right:    2
- Up:       5
- Down:     1

## Loading Instructions
[Download the Intel HEX File](Snake.hex) to your PC, then use a **Serial Terminal Program** like *CoolTerm* to download the HEX file to your TEC-1G via a **USB Cable**.
Use the **MON3 Intel HEX Load** to load the program. After loading, exit the Main Menu by pressing **AD** on the Hexpad or **ESC** on the Matrix Keyboard, which will take you to the address ``4000H``. Press the **GO** button, or the **ENTER** key on the Matrix keyboard to start the program.

## Code
[Download the Assembly Language File](Snake.z80) and examine or change the code and compile your own flavour. If you make any significant changes, consider providing an update to this repo.

### Suggested Modifications
- Length Counter:  Count how many Apples the Snake eats.
- Coloured Display:  Have the Apple in a solid Red

### High Score
Take a photo of of how many Apples your snake has eaten.
We will post results here!
