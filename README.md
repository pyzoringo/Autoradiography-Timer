# Autoradiography-Timer

Use Labview to build a UI, and help interaction with hardwares.  
Also put my ExpressPCB file here. (used to make an Arduino shield)  

Hardware:  
1. Arduino Uno  
2. Padel  
3. Pinch Valve  
4. Double-Channel Relay  
5. Synringe pump  

Basic Functions:  
1. A UI to minitor the status of cerebral blood flow sampling  
2. Control Valve with padel  
3. At time 0, start syringe pump  
4. record the time when padel is pressed  
5. at the end of the sampling, drive guillotine and output sampling file.  


PS: Most Info are stored elsewhere. Here is a place to show final outcome.  

3/21/2016  
DB9 Female to RJ11/12(6 wire) Serial port for communication b/w LabVIEW and Syringe pump  
threads: blue yellow(2) green red(3) black(5) white  

VI error: LIFA time out  Valve buring b/c the program stuck in trigged states.  
Reason: may be accessing DigitalWrite.vi and DIgitalRead.vi too many time in short time.  
Try solution: creating a flag, only access DWvi when Padel status changes.  
Result: semms OK for now.  
the LPF on padel needs to be fixed.  

3/22/2016  
1. Valve relay trigger pin change to 6. Since PIN7 keeps going back to LOW in idle.  
2. LPF was tested. Not quite useful actually. But still, added to PCB board design.    

Error: VI still glitching out (freezes) occasionally. Showing error that ArduinoVI time out.   
Reason: On 3/21, I suggested that accessing DigitalWrite.vi and DigitalRead.vi too many time in short time, but I only fixed DigitalWrite.vi by adding flag.  
Try solution: Every DigitalWrite.vi and DigitalRead.vi in the while loop got WaitTime, 5ms for DigitalRead, and 100ms for DIgitalWrite.  
Result: seems OK for now.  

3/25/2016  
Adding bunch of waitTimeVI to stable the communication b/w LabVIEW and Arduino  

4/01/2016  
Soldering up PCB  

5/07/2016  
Switching to LINX; reorganized LabVIEW block diagram;  
When saving file, create a folder named as current date;(duplicated folder error is neglected)  
Create a temp.txt when creating file prompt was cancelled;(cancle FileDialog error is neglected)  
In the txt file, date and time is stamped on top;  
Automatically open the txt file when it is created;  
Add sound warning in last 5 second of counting;  
Syringe is stopped immediately before guillotine;  
Virtual pedal and start button are greyed out in the process of Arduino initialization.  
Better cosmetic view of front panel.  
LabVIEW 2014; Windows 7; LINX 3.0.0.189
