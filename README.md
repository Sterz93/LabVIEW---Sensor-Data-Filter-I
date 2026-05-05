# LabVIEW---Sensor-Data-Filter-I
When using handheld sensor hardware, all measurement channels usually record information, regardless of any connection to a lightguide and subsequent sensor. It's useful to identify and discard information, which is linked to empty channels.


THE PROJECT IS FOR LEARNING PURPOSES SO FAR

The program is written for data analysis with a FireSting Blue device, particularly with chloride sensing, and it starts with a "Path Constant". The linked path should be the folder containing the relevant measurement data as ".txt" data.  
The program reads out the phase angle values and evaluates them along 3 different approaches.

The most practically useful approach is to just analyze the phase angle range of the sensor responses. The calibration and sample response data, i.e. data with a sensor being connected, all fall in the range of 10°- 50°. 
Thus, the program analyzes the value range of the phase angle response and assigns boolean constants to sensor data (true) and empty channels (false). Via the "select" function, the paths of the appropriate sensor data 
files is saved outside the For-Loop in the "array w/ subset deleted". This approach is not very elegant, but happens to be the most efficient one.

The second and third approaches attempt to identify sensor data through their plateaus among a response. 
The idea for the second (upper) approach is to read out phase angle data in packages of two subsequent values. By subtracting both values each and storing the result, the onset of any plateau ought to be well identifyable. The onset of a plateau can be identified by a rapid change in phase angle values, so the "max" value of the subtraction ought to be higher in sensor-related data than for empty channel data. However, the noise in empty channels is in a very similar range to sensor data, where the response happened to be weak due to the relative absence of the analyte. "Sort 1D" did not remedy the situation either. 

The third approach (middle) works with statistics, but the result is similar to the second approach. The program effectively builds a moving standard deviation with 3 data points each along the content of a measurement file. At the onset of the plateau, the standard deviation ought to be very high and thus make the sensor data identifyable against empty channel data. The results was, that empty channel data in fact did often display higher standard deviations than the standard deviations at the onset of a measurement plateau, particularly at low analyte concentrations.

This program is still a work in progress in so far that the first approach displays obvious weaknesses for more broad sensor applications. 
It is desirable to identify plateau values, but statistics can not be the foundation to the solution.
