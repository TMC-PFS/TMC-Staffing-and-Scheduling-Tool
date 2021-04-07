# TMC-Staffing-and-Scheduling-Tool

## Installation
This program requires the Java Runtime Environment (JRE). If you don't already have the JRE or a Java SDK installed, get the latest version of the **JRE 5.0 Update** from:
http://java.sun.com/j2se/1.5.0/download.jsp

The TMC Staffing and Scheduling Tool does not require any installation once the files are copied onto the computer. Note that the tool must be run from a drive with a letter (like C:), rather than from an unmapped network share. The tool is currently only designed to work under Microsoft Windows.

## Running the tool
Double-click on **Staffing Tool.cmd.** The black console window that opens can be closed if desired.

## Using the tool
The staffing tool has two parts: **Shift Scheduling** and **Relief Factor** calculations. These sections are accessed by clicking on the tabs at the top of the window. The two functions are independent; there is no interaction between them.

Shift Scheduling
The tool requires you to define the hours worked for all shifts that operators may be assigned to, and input the demand (number of operators required) for each hour of each day of the week. The tool then calculates the number of employees needed for each shift for each day, and also calculates the day on which each employee should start his or her work week.

Assumptions:
The algorithm on which this tool is based makes the following assumptions about demand and about employee schedules.
-Demand varies in a weekly cycle.
-All employees work five consecutive days, followed by two consecutive days off. The day on which an employee's work weeks starts is determined by the algorithm.

The numbers that appear above each column in the "Shift work hours" and "Number of operators required by day and hour" tables represent the hours of the day using a 24-hour clock (hour 0 is the midnight to 1 am hour; hour 12 is the noon to 1 pm hour).
The Shift Scheduling Tab:

Shift Scheduling Tab
**Inputs:**
1. **Tabs** - Click the tabs to toggle between the Shift Scheduling interface and the Relief Factor interface.

2. **Shift work hours** - Define shifts by selecting the checkboxes for the hours worked during the shift. Shifts can be any length and can have any pattern of hours worked. Click the Add button to add a new shift. Select one or more shifts and click the Remove button to delete the selected shift(s).

3. **Number of operators required by day and hour** - The demand (expressed in terms of the the number of operators required to accomplish the work that must be done) in each hour of each day. Press **ENTER** or move the cursor to a different field after changing any value so that the change takes effect.

4. **Save, Load and Calculate** - Click the Save... button to save the input data as a comma separated values (CSV) file. Click the Load... button to load previously saved input data. Click the Calculate button to calculate the outputs based on the current set of inputs.

**Outputs:**

5. **Status messages** - Various status messages appear here. If the outputs shown are based on the current input data, "Output is up to date." will be displayed. If the input data has changed since the last time the Calculate button was pressed, "Output is out of date. Click Calculate to update." will be displayed. If there is demand in a time period that is not covered by any shift work hours, "Specified demand cannot be satisfied by the specified shifts." will be displayed.

6. **Employees needed for each day and shift** - Each cell shows the number of employees who need to be working on each shift on each day. Depending on the pattern of demand and the way the shifts are defined, some shifts may not have any employees assigned to them.

7. **Employees by first day of work week and shift** - The tool assumes that all employees work a five-days-on, two-days-off schedule. This table shows the number of employees on each shift who need to begin their work weeks on each day. Some cells will be blank, indicating that no employees on that shift need to start work on that day.

8. **Scheduling statistics** - "Excess hours per week" is a calculated value showing the number of "slack" hours in the schedule (number of employee-hours where staffing exceeds demand). "Scheduling efficiency" is a ratio of total employee time required to total employee time scheduled. If staffing exactly equalled demand, this ratio would be equal to 100%. The algorithm used in the tool will never understaff, so the scheduling efficiency is always less than or equal to 100%.

9. **Export** - Click the Export... button to save the output data as a comma separated values (CSV) file.

The CSV files produced by this program can be opened in a spreadsheet program such as Excel. You should not modify the files created by the Save... button, as the program expects the data to be in a specific format when it is loaded.

## Relief Factor
The Relief Factor indicates how many employees it takes to fill a single job position, taking into account vacation, sick leave, training days, and other types of leave. The relief factor is expressed as a number, typically close to one, that represents the number of employees needed per position to be staffed.

Relief Factor Tab
White fields are inputs.
Yellow fields are outputs.

**Inputs:**
The relief factor depends on the average number of days off per employee, which is determined by the total days off for all employees and the number of employees included in that total. If the average is already known, enter it into **Total days off** and specify **1** for **Number of employees.**
1. **Total days off** - The total number of days off for all employees.
2. **Number of employees** - The number of employees included in the above total. Enter 1 if the total is actually the average.
3. **Number of positions** - The number of positions which need to be staffed. This could be the number of employees calculated on the Shift Scheduling tab.

Outputs:

4. **Average days off** - The average number of days off per employee. This is calculated as:
  Total days off / Number of employees
5.  **Relief factor** - The average number of employees that need to be hired to handle the workload of one position. This is calculated as:
  365 / (365 - (Average days off))
6. **Employees required** - The number of employees required to staff the number of positions given in 5. This is calculated as:
  (Relief factor) * (Number of positions)

## Examples
Shift Scheduling - Single day example:

The inputs for this example are provided in the file **example1.csv.** You can either enter the data manually or load the file.
This example shows how to calculate the staffing requirements for a single day with the following demand:

Hour:	  0	1	 2	3	4	5	6	7	8	  9	 10 11
Demand:	3	10 9	5	5	1	5	5	10	10 9	5
Create four shifts and select the hours worked on each shift:

Example 1 step 1

Enter the demand into the table for Monday:

Example 1 step 2

Click on Calculate to determine the number of employees needed for each shift:

Example 1 shift results

The number of employees required for each shift is shown in the row for Monday. Since all employees work the same schedule but starting at different times, there will sometimes be more employees working during an hour than there is demand.

Note that when multiple shifts can be used to cover the demand for a period, the algorithm randomly decides which shift to use to cover the demand. Therefore, clicking Calculate multiple times may result in slight variations in the outputs.

Also note that since any work week that includes Monday will cover the demand, the employees may be assigned to start on any day that starts a work week that includes Monday:

Example 1 work week results

A start day is randomly chosen if there are multiple start days which provide equal coverage. In this case, all employees would work from Thursday to Monday.


Shift Scheduling - Multiple day example:

This example shows how to calculate a work schedule for a simple week-long case.
This demand will require employees in two different shifts.

Example 2
The starting days for the two employees working shift 1 may be different, but they will always start two days apart so that they cover the whole week. One employee works Thursday-Monday while the other works Saturday-Wednesday.

The employee working shift 2 starts Wednesday and finishes Sunday, providing coverage for the demand during hour 19 of Sunday.
