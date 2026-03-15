# -CAN-Based-Automotive-Dashboard-
Implemented an Automotive Dashboard using CAN bus where ECU1 and ECU2 send vehicle data to ECU3 which displays it on an LCD.


          CAN BUS NETWORK
       -----------------------

      ECU1                ECU2
   (Speed & Gear)     (RPM & Indicator)
       |                     |
       |                     |
       -----------CAN BUS---------
                    |
                    |
                 ECU3
             Dashboard ECU
           (CLCD Display + LEDs)


