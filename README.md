# Hackfest
### Abstract
We believe that the safety of healthcare workers is of utmost importance.
CASCOV- Consultation And Sanitization for COVID-19 is a bot that has been designed to 
prevent and minimize the exposure of healthcare workers to this virus and prevent the 
spread through contact with infected surfaces.

### Software Used
• GSM module
• Arduino IDE
• AutoCAD
• TinkerCAD
• Glowscript
• MATLAB/Simulink
• Visual Python

### Functions
#### Motion
Follows the moving mechanism of a line follower robot, an 
automated guided vehicle, which follows a visual black line painted 
on the floor. The path is customized with unique markings near the 
walls and the bed so that the bot can sense and function accordingly. 
The bot will move around the whole ward, spraying sanitizer on the 
walls, floor, and objects simultaneously.
An ultrasound sensor will detect any obstacles in its path to 
prevent a collision. This feature would enable our robot to move 
without any supervision.
Floor markings are as follows:-


• Type1: This indicates that the bot is in front of the wall, so it has to 
stop, spray sanitizer on the wall and then start moving again.


• Type 2: This indicates that the bot is at the head of the bed, so it 
will have to stop, perform arm rotation to make the arm horizontal, 
put it under the bed, and then start moving further.


• Type 3: This indicates the bot to stop, take the arm back to its 
initial vertical position, and then start moving.


• Type 4: This indicates that the bot moves along a parallel wall on 
the right to spray while moving continuously.


• Type 5: This indicates that the bot moves along a parallel wall on 
the left to spray while moving continuously.
#### Mopping
To achieve this functionality, we attach a circular acrylic sheet 
below the bot with a motor. The acrylic sheet scrubs the surface, thus 
cleaning it far more efficiently. The bottle with disinfectant liquid is 
attached to the surface of the bot with a few connecting tubes that can 
be drawn from it to clean the surface properly.

#### Sanitization
This spraying mechanism has a working similar to that of a piston. 
An engine type of mechanism will be implemented to push the piston of 
the sprayer. Depending on the type of signal received at the markings,
the vertical arm of the bot is rotated so that it faces the surface on which 
the spraying is to be done.
The same mechanism will be used to spray sanitizer under the beds 
and on the walls. But now a second stepper motor will be used to make 
the vertical arm horizontal.

#### Communication
For the communication of the bot with the medical staff via voice 
call, a GSM Shield(SIM 900) is used with an external SIM Card 
connected with the Arduino UNO board. This is connected to an external 
speaker and a microphone circuit. The feature will include a pushbutton, 
which will enable the patient to converse with the medical staff. 
The following is the schematic diagram for the sample circuit connection 
of the Arduino Board with the GSM Shield having an integrated 
microphone.
