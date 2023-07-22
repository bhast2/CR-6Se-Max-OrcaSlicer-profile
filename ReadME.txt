These are files to add the CR6SE to orcaslicer. 

Don't overwrite the existing resources folder in orcaslicer. add the Cr-6SE.json and Cr-6SE folder in to resources/profiles.


please make sure the start and end Gcode look like the follow code



Machine Start G-code

G90 ; use absolute coordinates
M83 ; extruder relative mode
M140 S[bed_temperature_initial_layer] ; set final bed temp
M104 S150 ; set temporary nozzle temp to prevent oozing during homing
G4 S10 ; allow partial nozzle warmup
G28 ; home all axis
G1 Z50 F240
G1 X2 Y10 F3000
M104 S[nozzle_temperature_initial_layer] ; set final nozzle temp
M190 S[bed_temperature_initial_layer] ; wait for bed temp to stabilize
M109 S[nozzle_temperature_initial_layer] ; wait for nozzle temp to stabilize
G1 Z0.28 F240
G92 E0
G1 Y140 E10 F1500 ; prime the nozzle
G1 X2.3 F5000
G92 E0
G1 Y10 E10 F1200 ; prime the nozzle
G92 E0




Machine End G-code

{if max_layer_z < printable_height}G1 Z{min(max_layer_z+2, printable_height)} F600 ; Move print head up{endif}
G1 X5 Y{print_bed_max[1]*0.8} F{travel_speed*60} ; present print
{if max_layer_z < printable_height-10}G1 Z{min(max_layer_z+70, printable_height-10)} F600 ; Move print head further up{endif}
{if max_layer_z < printable_height*0.6}G1 Z{printable_height*0.6} F600 ; Move print head further up{endif}
M140 S0 ; turn off heatbed
M104 S0 ; turn off temperature
M107 ; turn off fan
M84 X Y E ; disable motors





