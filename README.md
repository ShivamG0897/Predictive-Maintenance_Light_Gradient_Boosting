“PdM_machines.csv” contains the metadata of the machines. This descriptive information
includes machine ID, machine model (4 types) and age (in years). Safe to say that the cranes are 
known to have a load capacity of around 35-45 tons, but this information is not being considered 
for the case since all the machines are believed to be of equal duty. Dimensions of the file: 100 
rows x 3 columns. Below are the total occurrences of various “model”:
1. model1: 16
2. model2: 17
3. model3: 35
4. model4: 32
 
“PdM_telemetry.csv” – contains the sensors readings taken sequentially on an hourly basis for 
the year 2015-16 for respective Machine Id. Nevertheless, sensory data include volt (in volts), 
rotate (Rounds Per Minute), pressure (in psi), vibration (in mm/s).# Predictive-Maintenance

“PdM_errors.csv” file – includes details about the type of error that occurred in respective 
machine_ID with details about time of occurrence. Errors here are any technical blockade in the 
readings of the sensors. For instance, in an infrared sensor dust hinders the reading, a specific type 
of error is observed. Due to sensitivity wrong information is passed. It shows a glitch in the 
algorithm, but it is not to be confused with the failures since these do not result in shutting down 
of a machine. Generally, we won’t know the different types of errors but still try and find patterns 
with signals data. 

“PdM_maint.csv” : This set of data carries information about the regularly scheduled 
replacements of components (preventive maintenance). Any rectifications made in belt, oil, 
engine, or filters etc. for each machine_ID are provided in this. 3286 instances with 3 columns are
the dimensions of this dataset. 

“PdM_failures.csv” : Information about component replacement due to failure is recorded in this 
file. This datafile is thus a subset of the maintenance data since it becomes a reactive maintenance
record. 
