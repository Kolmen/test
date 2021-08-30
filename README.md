This README file describes how to build and use the **iis2iclx_tilt_angle_DT_generator.c** program to generate two decision trees for tilt sensing, how to create from the decision trees an .ucf configuration file for the **Machine Learning Core (MLC)** of the [**IIS2ICLX**](https://www.st.com/en/mems-and-sensors/iis2iclx.html) and how to evaluate the result.


# 1. Build the C program
First, it is necessary to install a C compiler. The following lines show the procedure of compilation with the GCC compiler on Windows (using [**Cygwin**](https://www.cygwin.com/)). You can check that the GCC is sucessfully installed by writing `gcc -v` in the Command prompt.

Download the **iis2iclx_tilt_angle_DT_generator.c** file to your PC. The program may be modified according to one's needs in a text editor. However, for many cases or for basic evaluation the default program is sufficient.

Open the Windows Command Prompt (e.g. press Win+R, type cmd and press Enter key) and go to the folder, where the **iis2iclx_tilt_angle_DT_generator.c** is located. For instance, if the file is located in C:\tilt_angle_dual_plan\angle_customization_script, then you can write the following command:
```
cd C:\tilt_angle_dual_plan\angle_customization_script
```

The correct location can be verified by writing command `dir` or `ls` as visible below:
// <img src="./images/prog_loc.png" alt="prog_loc" style="zoom:60%;" />


Write the command to build the **iis2iclx_tilt_angle_DT_generator.c**:
```
gcc iis2iclx_tilt_angle_DT_generator.c -o iis2iclx_tilt_angle_DT_generator
```

The command creates an executable file in current folder. (in this case the name of the file is **iis2iclx_tilt_angle_DT_generator.exe**)

# 2. Generate decision trees with the built program
After the program is built it is possible to run it simply with the following command (it will use the default configuration):
```
iis2iclx_tilt_angle_DT_generator.exe
```

This program creates two text files (in './dec_tree' folder), each of which contains a decision tree (one for the x axis and one for y axis of the accelerometer) in the format required by Unico to generate the MLC. Each decision tree contains 255 acceleration threshold levels to be detected, spaced symetrically around zero degree of inclination within the specified angular range (by default it is +/- 20 degrees). The threshold levels correspond to certain inclination angles.
Please note, that typical sensor errors (like zero-g offset, sensitivity error, etc.) are not considered in this example. If more accurate measurement is required, the calibration must be performed and then projected into the calculated threshold levels (modification of the program is then needed).

It is possible to configure following parameters of the program from the Windows Command Prompt:

- **Angle range**
- **Folder name**, where two text files with the decision trees should be stored

**Angle range** must be an integer *N* in range from 2 to 90 [deg]. The final angle range will be symmetrical around zero (thus, [-N, N] degrees).
**Folder name** must start with an alphabet character and must not contain following special characters: 
```
<,>:\"/\\|?*@\'^.
```

**Default configuration:**
```
**Angle range** = +/- 20 degrees
**Folder name** = 'dec_tree'
```

The default configuration of the program can be modified by using following options:

	`-a`	Set the angle range parameter
	`-o`	Set the output folder name

Option `-h`	can be used to display help message.

###Example:

1. Help: 
```
iis2iclx_tilt_angle_DT_generator.exe -h
```
This example only prints help of the program.

2. Configuration
```
iis2iclx_tilt_angle_DT_generator.exe -a 25 -o my_folder
```
This example executes the program with following modification of parameters:
```
**Angle range** = +/- 25 degrees
**Folder name** = 'my_folder'
```
