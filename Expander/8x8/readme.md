# 8x8 RGB LED Matrix Display

It's HERE!

Watch the Demo video:  https://youtu.be/IrcrIdf2KzY

The schematic is in the Files List, above.

Demo code and an update to the MON3 APIs will be released shortly to help everyone develop software for the device.

## Sample Code
This section will be broken out to its own file, but to get people up and running quickly, here are a few snipets of code you can try with your RGB 8x8. Or download the HEX file to run the Demo that was shown in the video. (Hidden off camera was me pressing 0 (zero) to turn all colours on, and then 1, 2 or 3 to toggle the colour ports on or off.)

### Includes
; Port Defines
Y8x8:       .equ $05        ; Standard 8x8 Row (Y) select
Rx8x8:      .equ $06        ; RGB 8x8 (Red) column (X) select
Gx8x8:      .equ $F8        ; RGB 8x8 (Green) column (X) select
Bx8x8       .equ $F9        ; RGB 8x8 (Blue) column (X) select

.ORG $2000                  ; All the 8x8 data
buff8x8:
left8x8:        ds 8        ; This is an "off screen" buffer to the left, used for scrolling right
blue8x8:        ds 8        ; the 8x8 display actually shows these 3 buggers
green8x8        ds 8        ; the 8x8 display actually shows these 3 buggers
red8x8:         ds 8        ; the 8x8 display actually shows these 3 buggers
right8x8:       ds 8        ; The is an "off screen" buffer to the right, used from scrolling left
colour8x8:      ds 1        ; used to contain Bit switches for which colour is to be turned on or shown

.ORG $4000              ; setup menu & system state
    ld HL, colour8x8        ; Reset Color selection to Just RED
    ld A, $01               ; Set colour bits to 001 = RED, 010 = GREEN, 100 = BLUE
    ld (HL), a

; Set up a menu here, or simply call each "demo" one at a time
    call VBar
    ret


VBar:               ; Vertical bar going left & right
    ld B,$FF        ; Vertical Bar bit pattern. $FF = Solid line
    ld C,$01        ; Horizontal location of Bar (RED). $01 = Rightmost column
loopV1:
    ld D,C          ; Copy bar location to (GREEN)
    ld E,C          ; Copy bar location to (BLUE)
    call outC8x8
    sla C
    jr nc,loopV1
    ld C,$80        ; Set column to leftmost column
loopV2:
    ld D,C
    ld E,C
    call outC8x8
    srl C
    jr nc,loopV2
    ld C,$01        ; Set column to rightmost column
loopV3:
    ld D,C
    ld E,C
    call outC8x8
    sla C
    jr nc,loopV3

    call clr8x8
    ret

HBar:               ; Horizontal bar going up and down
    ld B,$01        ; Vertical location of Bar. $01 = Top row
    ld C,$FF        ; Horizontal Bar bit pattern. $FF = Solid line
    ld D,C          ; Copy bar to GREEN Register D
    ld E,C          ; Copy bar to BLUE Register E
loopH1:
    call outC8x8
    sla B
    jr nc,loopH1
    ld B,$80
loopH2:
    call outC8x8
    srl B
    jr nc,loopH2
    ld B,$01
loopH3:
    call outC8x8
    sla B
    jr nc,loopH3

    call clr8x8
    ret

Blinky:                 ; strobe on and off
    ld B,$03            ; Number of ON flashes
    ld C,$FF            ; Bit patter to flash on RED
    ld D,$FF            ; Bit patter to flash on GREEN
    ld E,$FF            ; Bit patter to flash on BLUE
loopB:
    push bc
    ld B,$00
    call outC8x8
    call barDly
    call barDly
    dec b
    call outC8x8
    call barDly
    call barDly
    pop bc
    djnz loopB

    call clr8x8
    ret

Fanny:                      ; Fan out then In
    ld HL, colour8x8        ; Colour control byte
    ld C,(HL)               ; Load C with current Colour Control value
    push BC                 ; Save it to be restored at end

    ld B,$03                ; Count of how many Fans to do
    ld C, $01               ; RED Colour to start
    ld (HL),C               ; Save it to the colour control byte
loopF:                      ; set up Fanout
    push bc
    ld B,$80
    ld C,B
    ld D,B
    ld E,B
loopO:                      ; Fanout Loop
    call outC8x8
    sra b
    ld C,B
    ld D,B
    ld E,B
    jr nc, loopO
    sla b
loopI:                      ; Fanin loop
    ld C,B
    ld D,B
    ld E,B
    call outC8x8
    sla b
    cp 0
    jr nz, loopI

    pop bc                  ; Restore the counter (b) and the colour (c)
    rlc c                   ; Rotate to next colour
    ld (HL),C               ; Save it to the colour control byte
    djnz loopF

    pop BC                  ; Restore prior Colour Control byte
    ld (HL),C
    call clr8x8
    ret

Boxy:                       ; Coloured boxes
    ld B,$03                ; Number of box cycles
loopX:
    push BC
    ld B,$18
    ld C,B
    ld D,B
    ld E,B
    call outC8x8
    ld B,$3C
    ld C,B
    ld D,B
    ld E,B
    call outC8x8
    ld B,$7E
    ld C,B
    ld D,B
    ld E,B
    call outC8x8
    ld B,$FF
    ld C,B
    ld D,B
    ld E,B
    call outC8x8
    ld B,$7E
    ld C,B
    ld D,B
    ld E,B
    call outC8x8
    ld B,$3C
    ld C,B
    ld D,B
    ld E,B
    call outC8x8
    ld B,$18
    ld C,B
    ld D,B
    ld E,B
    call outC8x8
    ld B,$00
    ld C,B
    ld D,B
    ld E,B
    call outC8x8

    pop BC
    djnz loopX

    call clr8x8
    ret


Lines:                     ; Colourfull lines from centre out
    ld B,$03
    ld C,$00
    ld D,$00
    ld E,$00
loopL:
    push bc
    ld B,$FF
    ld C,$18
    call outC8x8
    call barDly
    ld E,d
    ld D,C
    ld C,$24
    call outC8x8
    call barDly
    ld E,d
    ld D,C
    ld C,$42
    call outC8x8
    call barDly
    ld E,d
    ld D,C
    ld C,$81
    call outC8x8
    call barDly
    ld E,d
    ld D,C
    ld C,$00
    call outC8x8
    call barDly
    ld E,d
    ld D,C
    ld C,$00
    call outC8x8
    call barDly
    ld E,d
    ld D,C
    ld C,$00
    call outC8x8
    call barDly

    pop bc
    djnz loopL

    call clr8x8
    ret

; Show 8x8 Icons in full colour
showIcon:
    ld HL, rgbMario1 
    ld DE, 24                ; Number of bytes to add to HL to get next Icon
showIt:
    push HL
    pop IX                  ; Load IX with the address in HL
    call RGB8x8
    ld C, scanKeys_
    RST $10
    jr nc, showIt
    cp $13                  ; ESC (AD) Key pressed
    jr z, showExit
    cp $11                  ; MINUS key pressed
    jr z, showMinus
    cp $10                  ; PLUS key pressed
    jr z, showPlus
    cp $00                  ; ZERO key press
    jr z, showIcon
    jr showIt

showPlus:
    add HL, DE
    jr showIt
showMinus:
    ld A,l
    cp $00
    jr z, showIt
    sub $18
    ld L,A
    jr showIt
showExit:
    ret


;*****************************************************************
.ORG $4400
; Text scrolling across 3 modules.
; Leftmost module is configured as Blue (to Red)
; Middle module configured as Green (to Red)
; Right module, actually connected to TEC-1G, is Red

scrollText:
    ld HL, txtTable         ; Start of Text string data (has 3 spaces before to clear screen)
    ld DE, blue8x8          ; Start of Left display (BLUE) buffer
    ld BC, 24               ; Number of bytes to copy from TextTable to Buffer
    ldir                    ; Copy data from TextTable to Buffer
    ld HL, txtTable         ; HL must be set back to start of text, as it gets screwed by the LDIR

showText:
    ld IX, blue8x8          ; Reload IX with start of the 8x8 Display Buffer
    call BGR8x8
    ld C, scanKeys_
    RST $10                  ; Kills IX
    jr nc, showText
    cp $13                  ; ESC (AD) Key pressed
    jr z, scrollExit
    cp $11                  ; MINUS key pressed
    jr z, scrollMinus
    cp $10                  ; PLUS key pressed
    jr z, scrollPlus
    cp $00                  ; ZERO key press - Reset back to start
    jr z, scrollText
    jr showText

scrollPlus:
    ld DE, 8
    add HL, DE
    push HL
    ld DE, blue8x8          ; Start of Blue (left) buffer
    ld BC, 24               ; only need to copy 3 characters
    ldir
    pop HL
    jr showText

scrollMinus:
    ld DE, 8
    sbc HL, DE
    push HL
    ld DE, blue8x8          ; Start of Blue (left) buffer
    ld BC, 24               ; only need to copy 3 characters
    ldir
    pop HL
    jr showText

scrollExit:
    ret

.ORG $4500
smoothScroll:			; #### NOTE #### This scrolling code still has bugs!! ####
    ld HL, txtTable         ;
    ld DE, left8x8          ; Start of off-screen (left) buffer
    ld BC, 40
    ldir
    ld HL, txtTable         ; HL must be set back to start of text, as it gets screwed by the LDIR
    ld DE, 0                ; D & E will each be used to keep track of how many scrolls
smoothText:
    ld IX, buff8x8
    call BGR8x8
    ld C, scanKeys_
    RST $10
    jr nc, smoothText
    cp $13                  ; ESC (AD) Key pressed
    jr z, scrollExit2
    cp $11                  ; MINUS key pressed
    jr z, smoothMinus
    cp $10                  ; PLUS key pressed
    jr z, smoothPlus
    cp $00                  ; ZERO key press - Reset back to start
    jr z, smoothText
    jr smoothText

smoothPlus:
    xor A
    cp E
    jr nz, plusScroll
plusScroll:
    ld IX, buff8x8
    ld IY, txtTable
    call scroll8x8L          ; Scroll the 3 screen buffer 1 pixel left
    ld A, 8
    dec D
    inc E
    cp E
    jr nz, smoothText
        ld E, 0
    jr smoothText

smoothMinus:
    xor A
    cp D
    jr nz, minusScroll
minusScroll:
    ld IX, buff8x8
    ld IY, txtTable
    call scroll8x8R           ; Scroll the 3 screen buffer 1 pixel left
    ld A, 8
    dec E
    inc D
    cp D
    jr nz, smoothText
        ld D, 0
    jr smoothText

scrollExit2:
    ret

; Scroll the display buffer one pixel left
; Needs:    IX  to point to the screen buffer
;           IY  to point to the start of the image datA,
;               arranged in 8 byte blocks. (Should also work for RGB)
;           B   Count of Pixel number
;Destroys:

scroll8x8L:
    push BC
    push IX
    ld B, 8                    ; Count of rows
shiftBGRl:
        ld A, (IX+24)           ; Grab the byte from the Right off-Screen buffer
        rla                     ; Rotate it through the carry flag (CF = Bit 7 of Right)
        ld (IX+24), A           ; Save it back to the Right buffer
        ld A, (IX+16)           ; Grab the byte from the Red buffer
        rla                     ; Rotate it through the carry flag (CF = Bit 7 of Red)
        ld (IX+16), A           ; Save it back to the Red buffer
        ld A, (IX+8)            ; Grab the byte from the Green buffer
        rla                     ; Rotate it through the carry flag (CF = Bit 7 of Green)
        ld (IX+8), A            ; Save it back to the Green buffer
        ld A, (IX+0)            ; load the byte from the Blue buffer
        rla                     ; Rotate it through the carry flag (CF = Bit 7 of Blue)
        ld (IX+0), A            ; Save it back to the Blue buffer
        ld A, (IX-8)            ; load the byte from the Left buffer
        rla                     ; Rotate it through the carry flag (CF = Bit 7 of Left)
        ld (IX-8), A            ; Save it back to the Left buffer
        inc IX
    djnz shiftBGRl                ; Repeat 8 times
    pop IX
    pop BC
    ret

scroll8x8R:
    push BC
    push IX
    ld B, 8                    ; Count of rows
shiftBGRr:
        ld A, (IX-8)            ; Grab the byte from the Left off-Screen buffer
        rra                     ; Rotate it through the carry flag (CF = Bit 7 of Green)
        ld (IX-8), A            ; Save it back to the Blue buffer
        ld A, (IX+0)            ; Grab the byte from the Green buffer
        rra                     ; Rotate it through the carry flag (CF = Bit 7 of Green)
        ld (IX+0), A            ; Save it back to the Blue buffer
        ld A, (IX+8)            ; Grab the byte from the Green buffer
        rra                     ; Rotate it through the carry flag (CF = Bit 7 of Green)
        ld (IX+8), A            ; Save it back to the Blue buffer
        ld A, (IX+16)            ; load the byte from the Blue buffer
        rra                     ; Rotate carry into it (Bit 0 of Screen 1 = CF)
        ld (IX+16), A            ; Save it back to the Blue buffer
        ld A, (IX+24)           ; Grab the byte from the Right off-Screen buffer
        rra                     ; Rotate it through the carry flag (CF = Bit 7 of Right)
        ld (IX+24), A           ; Save it back to the Right buffer
        inc IX
    djnz shiftBGRr                ; Repeat 8 times
    pop IX
    pop BC
    ret



; ----------------------------------------------------------------
; RGB8x8
; INPUT:        IX = Start of screen buffer or graphics data, 24 bytes, 8 bits per byte.
; DESTROYS:     A
;
;   TopL
;    7 6 5 4 3 2 1 0    Byte 0
;    7 6 5 4 3 2 1 0    Byte 1
;    7 6 5 4 3 2 1 0    Byte 2
;    7 6 5 4 3 2 1 0    Byte 3
;    7 6 5 4 3 2 1 0    Byte 4
;    7 6 5 4 3 2 1 0    Byte 5
;    7 6 5 4 3 2 1 0    Byte 6
;    7 6 5 4 3 2 1 0    Byte 7
;                         BotR
;
; Outputs 24 bytes to an RGB 8x8.
; IX to contain start address of graphic datA, with
; 8 bytes of RED, 8 bytes of GREEN and 8 bytes of BLUE
; The RGB 8x8 is configured in Byte order; no need for any data rotation
; 1st row is at top
; ----------------------------------------------------------------

RGB8x8:
    push BC
    push IX
    ld C,$01            ; Row counter

rgbScan:
    ld A,(IX+0)         ; Load A with Red Data
    out (Rx8x8),A
    ld A,(IX+8)         ; Load A with Green Data
    out (Gx8x8),A
    ld A,(IX+16)        ; Load A with Blue Data
    out (Bx8x8),A
    ld A,C              ; load the current row into A
    out (Y8x8),A

    ld B,$40            ; ON time counter
loopON:
        djnz loopON
    xor A               ; turn off to prevent shadow
    out (Y8x8),A

    inc IX              ; Point to the next byte of Red data
    rl C                ; next row down
    jr nc, rgbScan

    pop IX
    pop BC
    ret


BGR8x8:
    push BC
    push IX             ; IX to contain Start of 8x8 screen data
    ld C,$01            ; Row counter

brgScan:
    ld A,(IX+0)         ; Load A with Red Data
    out (Bx8x8),A
    ld A,(IX+8)         ; Load A with Green Data
    out (Gx8x8),A
    ld A,(IX+16)        ; Load A with Blue Data
    out (Rx8x8),A
    ld A,C              ; load the current row into A
    out (Y8x8),A

    ld B,$40            ; ON time counter
loopON2:
        djnz loopON2
    xor A               ; turn off to prevent shadow
    out (Y8x8),A

    inc IX              ; Point to the next byte of ROW data
    rl C                ; next row down
    jr nc, brgScan

    pop IX
    pop BC
    ret


clr8x8:
    xor A
    out (Rx8x8),A
    out (Gx8x8),A
    out (Bx8x8),A
    out (Y8x8),A
    ret

; Clear the 24 byte screen buffer, pointed to by HL
; Needs:  HL pointing to start of screen buffer
; Destroys: A
clrBuff:
    push HL
    xor A
    ld B, 24        ; Buffer size of 3x 8x8 screens
clrIt:
    ld (HL),A
    inc HL
    djnz clrIt
    pop HL
    ret



.ORG    $5FFF
txtCount:
    .db 16
txtTable:
    .db 0,0,0,0,0,0,0,0                         ; {blank space}
    .db 0,0,0,0,0,0,0,0                         ; {blank space}
    .db 0,0,0,0,0,0,0,0                         ; {blank space}
    .db $AA, $AA, $AA, $AA, $AA, $AA, $AA, $AA  ; Test pattern
    .db 0,0,0,0,0,0,0,0                         ; {blank space}
    .db $FE,$FE,$38,$38,$38,$38,$38,$38         ; T
    .db $FE,$FE,$E0,$F8,$F8,$E0,$FE,$FE         ; E
    .db $3C,$FE,$EE,$E0,$E0,$EE,$FE,$7C         ; C
    .db $00,$00,$00,$7E,$7E,$00,$00,$00         ; -
    .db $38,$78,$F8,$38,$38,$38,$38,$38         ; 1
    .db $3C,$FE,$E6,$E0,$EE,$E6,$FE,$7C         ; G
    .db 0,0,0,0,0,0,0,0                         ; {blank space}
    .db $AA, $AA, $AA, $AA, $AA, $AA, $AA, $AA  ; Test pattern
    .db 0,0,0,0,0,0,0,0                         ; {blank space}
    .db 0,0,0,0,0,0,0,0                         ; {blank space}
    .db 0,0,0,0,0,0,0,0                         ; {blank space}


rgbMario1:
    .db $00, $04, $28, $3C, $A5, $3C, $3C, $24
    .db $00, $04, $3C, $34, $81, $00, $00, $00
    .db $3C, $3E, $14, $08, $5A, $00, $00, $24
rgbMario2:
    .db $00, $04, $28, $35, $24, $BC, $3C, $48
    .db $00, $04, $3C, $35, $00, $80, $00, $00
    .db $3C, $3E, $14, $00, $5A, $00, $00, $48

rgbSpacey1:
    .db $00, $00, $00, $24, $00, $3C, $00, $00
    .db $24, $7E, $FF, $DB, $7E, $7E, $BD, $81
    .db $00, $00, $00, $00, $00, $3C, $00, $00

rgbSpacey2:
    .db $00, $00, $00, $24, $00, $18, $00, $00
    .db $42, $7E, $FF, $DB, $7E, $7E, $BD, $42
    .db $00, $00, $00, $00, $00, $18, $00, $00

rgbSmile:
    .db $1C, $7E, $48, $DB, $FF, $7E, $7E, $18
    .db $1C, $7E, $48, $DB, $FF, $5A, $66, $18
    .db $00, $00, $00, $12, $00, $00, $00, $00

rgbGhost1:
    .db $00, $00, $36, $12, $00, $00, $00, $00
    .db $38, $7C, $FE, $DA, $FC, $FC, $FC, $B4
    .db $3C, $7E, $FF, $DB, $FF, $FF, $FF, $B6

rgbGhost2:
    .db $00, $00, $36, $24, $00, $00, $00, $00
    .db $38, $7C, $FE, $EC, $FC, $FC, $FC, $D8
    .db $3C, $7E, $FF, $ED, $FF, $FF, $FF, $DB

rgbCherry:
    .db $00, $00, $00, $06, $6F, $F7, $F6, $60
    .db $0E, $14, $24, $20, $02, $20, $00, $00
    .db $00, $00, $00, $00, $02, $20, $00, $00

rgbGay:
    .db $FF, $FF, $FF, $00, $00, $00, $FF, $00
    .db $FF, $00, $FF, $FF, $FF, $00, $00, $00
    .db $FF, $00, $00, $00, $FF, $FF, $FF, $00

rgbEggplant:
    .db $00, $00, $1C, $7E, $FE, $FE, $FC, $78
    .db $09, $0F, $02, $11, $60, $00, $00, $00
    .db $00, $00, $1C, $7E, $FE, $FE, $FC, $78

    .dw $C3, $BD, $7E, $66, $18, $66, $BD, $C3
    .dw $C3, $81, $20, $00, $18, $66, $BD, $C3
    .dw $00, $00, $20, $00, $18, $66, $3C, $00

    .db $00, $00, $1C, $7E, $FE, $FE, $FC, $78
    .db $09, $0F, $02, $11, $60, $00, $00, $00
    .db $00, $00, $1C, $7E, $FE, $FE, $FC, $78

    .db $00, $00, $1C, $7E, $FE, $FE, $FC, $78
    .db $09, $0F, $02, $11, $60, $00, $00, $00
    .db $00, $00, $1C, $7E, $FE, $FE, $FC, $78

