# Software for the TEC-1G
We will collect software the community creates for the TEC-1G in this repo.
If you have created anything you are proud of, please submit it for inclusion.
The only thing we ask is that the software is Open Source. This means that all
software must come with the Assembler file and ideally will be commented/documented
so that others in the community can learn from and re-use the code you submit,
and thus allowing the growth of the software library.

## Usage
All software will be in both .Z80 (Z80 Assembler) and .HEX (Intel HEX) format.
Feel free to download the Assembler file, read it, learn from it and compile it yourself.
Or if you just went to get stuck into it, download the Intel HEX file. 
When loaded via the **MON3 Intel HEX** loader, the software will generally be placed
at address `4000H`.  There are some exceptions to this, and that is why you should check
the comments at the top of the .Z80 file, which will also give you instructions on
how to play the game or use the software.

## Categories

### Games
What else are computers for than for some down time, playing some absorbing game?
| File | Description | Author | Requirements |
|---|---|---|---|
| [Game of Life](Games/GOL.md) | Conway's Game of Life | Brian Chiha | 8x8 |
| [Invader](Games/Invader.md) | The original TEC Invaders game! | Cameron Sheppard / Brian Chiha | 8x8 |
| [Invaders](Games/Invaders.md) | Brian's adaption of TEC Invaders | Brian Chiha | 8x8 |
| [TEC Runnner](Games/LCDRun.md) | Load runner jumps!  | Brian Chiha | Standard LCD |
| [Magic Square](Games/MagicSq.md) | Create a Magic Square | Jim Robertson | 8x8 |
| [Maze](Games/Maze.md) | The original MAZE game! | Cameron Sheppard / Brian Chiha | 8x8 |
| [MazeMan](games/Mazemam.md) | A-Maze-ing | Brian Chiha | 8x8 |
| [Snake](Games/Snake.md) | Every computer needs a Snake game! | Brian Chiha | 8x8 |


### Applications & Languages
A collection of applications and alternate languages for the TEC-1G.
| File | Description | Author | Requirements |
|---|---|---|---|
| [Tiny Basic](Apps/TBASIC.md) | A compact BASIC for the TEC-1G. | Brian Chiha | Serial Terminal / GLCD + Matrix KB |
| [TMON](Apps/TMON.md) | A MONitor using a Serial Tewrminal | Craig Hart | Serial Terminal |


### Education
All the software from the Talking Electronics Magazine for the original TEC-1, updated and ported to the TEC-1G
(If you have ported any over, please help and contribute. Please have the code VERY WELL commented in assembler file.
| File | Description | Author | Requirements |
|---|---|---|---|
| [Name](file.md) | Placemarker! |  |  |


### Music & Sounds
Yes, the TEC can make music...
| File | Description | Author | Requirements |
|---|---|---|---|
| [Banger](Music/Banger.md) | Impressive beats from 26 bytes of code! |  | - |
| [1-Bit Tunes](Music/1Bit.md) | Several Tunes using the default 1-Bit speaker! | Brian Chiha | - |


### Cryptography & Communications
| File | Description | Author | Requirements |
|---|---|---|---|
| [Bitcoin](Cryptography/Bitcoin.md) | Mine Bitcoin on your TEC-1G! (Nah, JK) | Mark Jelic | Matrix Keyboard |

