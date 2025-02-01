1.Open the OPENLANE Software
cd Desktop/work/tools/openlane_working_dir/openlane
Desktop/work/tools/openlane_working_dir/openlane$  docker
 ./flow.tcl  -interactive
% package require openlane 0.9
% prep –design picorv32a

 
 
2.% run_synthesis (Command for Synthesis)
 
3.Reviewing synthesis results
 
Flop ratio=Flipflop cell/Total number of cells
	=1613/14876
•	cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs
•	Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs$ ls  -ltr
•	Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs$  cd date_time
•	Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/ date_time$ cd results
•	Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/ date_time/results$
 
 
 
4. FloorPlanning
% run_floorplan
 

 
Finding Die Area in Micron
•	Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/ date_time/ results/floorplan$ less picorv32a.floorplan.def
 
 

Open floorplan in Magic
•	Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/ date_time/ results/floorplan$ magic –T  /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/ magic/ sky130A.tech.lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &

 
 
Placement
•	Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/ date_time/ results/floorplan$ cd ../placement/
•	Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/ date_time/ results/ placement$  magic –T  /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/ magic/ sky130A.tech.lef read ../../tmp/merged.lef def read picorv32a.placement.def &
Cloning github vsdststdcelldesign
•	Desktop/work/tools/openlane_working_dir/openlane$    git clone https://github.com/nickson-jose/vsdstdcelldesign.git
 
Copying sky130A.tech library to from pdk to vsdstdcell design

Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/ magic$ cp sky130A.tech /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign/


 
 
Opening the layout in Magic
Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign$  magic  -T sky130A.tech sky130_inv.mag &


 
Extracting layout to Spice file
Type the the following commands  in tkcon  after opening magic
% extract all
% ext2spice cthresh 0 rthresh 0
% ext2spice

 

Open the extracted spice file from layout
Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign$  vim sky130_inv.spice

 
Type I to get INSERT mode in spice file
To save a program in the Linux terminal, you can use the :wq command in the vim editor. 
Steps 
1.	Open the terminal
2.	Open the file using the vim editor
3.	Press i to enter insert mode
4.	Type your program
5.	Press Esc
6.	Type :wq to save the file

 --------------------------------------------------------------------------------------------------------------------------------------
Running extracted spice file using ngspice
Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign$  ngspice sky130_inv.spice

 
