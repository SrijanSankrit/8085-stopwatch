## Stopwatch based on Microprocessor 8085 with PAUSE-RESET-START functions.
#### This project was made using MICROFRIEND DYNA-85
###### Microfriend  DYNA-85  is  an  introduction  to  a  low cost trainer and  development kit. It was developed to assist the novice to get familiar with  INTEL  8085  microprocessor in  a user friendly environment.

There are two parts of this project.

### First part : NORMAL STOPWATCH

  *  The stopwatch displayed time in **minutes, seconds and 1/100th of a second** format.
  *  We need a delay of **10 ms** for the 1/100th second values, so we wrote a routine to implement that.
      > LXI D,04E2</br>
      > UP : DCX D</br>
      > MOV A,D</br>
      > ORA E</br>
      > JNZ UP</br>
      
     This routine ensures that we get a delay of 10ms.
  *  The data field of the display shows 1/100th second value while address field shows the minutes and seconds value. When the data field value   reaches 63H (or 100), we need to update seconds while making data field zero.
  * When the seconds field reaches 59, we need to update the minutes field and make seconds zero.
  * when the stopwatch reaches 59:59:99 , we just jump back to the beginning (i.e. 00:00:00).

### Second part : INTERRUPT ROUTINE

  * For achieving this part, we used **vector interrupt(VI)** on the machine which is basically the **RST 7.5** of 8085 microprocesser.
  * We kept the value of B register as 00H for most of the time when the stopwatch code runs.
  * When we press VI for the first time, stopwatch goes to **PAUSE** mode while value of B register is updated to 01H. We achieve this mode by running the interrupt code into an infinite loop.
  * When we press VI for the second time , this is the **RESET** mode, where value of B register is 01H, so we first update the value of B register to 02H and then reset A register to 00H and HL register pair to 0000H and run that in an infinite loop.
  * When we press VI for the third time, this is the **START** mode, where we just return to the stopwatch routine and thus, continue the flow of the stopwatch code and value of B register goes back to 00H.


  This project was made by</br>
     Srijan Sankrit (https://github.com/sankr170104072) - Team Leader</br>
     Sarvesh Choushetti (https://github.com/choushetti)</br>
