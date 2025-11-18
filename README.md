# CS 370 - Lab 3

## Group Members
- Gregory Larson
- Patrick Ho
- Rachel Rogers

## Contributions
- Gregory Larson
	- Completed part 1, the Factory Preset Model. Created diagrams.
- Patrick Ho
	- Created part 2, the User-Programmable Model.
- Rachel Rogers
	- Created part 2, the 8-Bit Sequencer.

## Files Attached
- README.txt
	- This documentation file.
- Lab3_Images (Folder)
	- StateDiagram.jpg
		- This is an image of the state diagram for the logic in part 1.
	- StateTable.jpg
		- This is an image of the state table for the logic in part 1.
	- KMap.jpg
		- This is an image of the K-maps for the logic in part 1.
	- Equations.jpg
		- This is an image of the equations for the logic in part 1.
- Raw CCT Files (Folder)
	- 1_Gotcha_Anti-Theft.cct
		- Contains the documented .cct file of part 1 of the lab, the Factory Preset Model.
   	- 8_Bit_Sequencer.cct
		- Contains the documented .cct file of the 8-Bit Sequencer for part 2 of the lab.
   	- User_Programmable.cct
		- Contains the documented .cct file of the User-Programmable Code for part 2 of the lab.
- Part_1_Factory_Preset_Model.cct
	- Contains the documented .cct file of the finished Factory Preset Model circuit part.
- Part_2_User_Programmable_Model.cct
	- Contains the documented .cct file of the finished 8-Bit Sequencer and User-Programmable Code circuit parts.
- Lab3.clf
	- Contains the finished circuit parts of Lab 3. The Factory Preset Model, the 8-Bit Sequencer and the User-Programmable Code

## Key Used
Key from Gregory Larson's RedID: 01010101

## Design Process
For part 1, the Factory Preset Model, we have 2 buttons inputs, BTN_1 and BTN_0 on the left, 0 and 1. When pressed, these inputs send a 1 through. These buttons feed through a flip-flop "X" which manages the input from the user. It sends a 0 or 1, depending on the input pressed. BTN_0 also feeds into an AND gate called "X RESET" which combines BTN_0 and RESET which is the reset of "X". Then, theres the clock pulse, "C PULSE," which takes the inverted input of BTN_1 and BTN_0. C inputs respond to positive edge, C PULSE stays in 1, switches to 0 on button pressed, and reverts to 0 on release. Then we have the clock logic, the "COUNTER" counter and "16_COUNT" flip-flop. The 4-bit counter tracks presses 0-15, and the flip-flop tracks the 16th press. It will toggle to 1 when COUNTER overflows, which disables "SIGNAL_OUT," (which will start the engine after the correct code is detected and the signal is not locked) and resets "COUNTER RESET" (which is an OR gate that resets the two counter components when the RESET button is pressed or the correct code is detected before lockout), effectively locking the user out at 16 presses. We also used a signal bus that has the signal wires: X', X, C', C, B', B, and A. It is optimized to only use 3 flip-flops, reducing the hardware required. This all was determined by the logic shown in our state diagram, state table, and k-map optimized equations, which are included in this zip file in the Lab3_Images folder. 

StateDiagram.jpg  
![StateDiagram](image-url)
StateTable.jpg  
KMap.jpg  
Equations.jpg  

For part 2, we have the User-Programmable Model and the 8-Bit Sequencer. The User-Programmable Model stores the user programmable code and is clocked by the "SAVE" input. The "INPUT CHECKER" is built with XNOR gates that compare output from the 8-Bit Sequencer to the user's secret byte. The XNOR gate ensures that 1 outputs only is both inputs are 1.
The 8-Bit Sequencer has outputs Disp00-Disp07 (for the probes) and Out00-Out07 (the output to feed into the User-Programmable Model). Using similar inputs as part 1, it has the 0 and 1 buttons. There are 8 flip-flops, M1-M8. M1 takes direct input from the push buttons 1 and 0, using asynchronous input to change state. Its D and C are set to 0 (unused). M2-M8 hold the previous inputs. Clock is pulsed when 1 and 0 are pressed, causing the data to shift to the next flip-flop. The RESET hooks up the reset of M1-M8, inverted, and also is the input for an OR gate with the 0 button to connect to the clocks of M1-M8. 

