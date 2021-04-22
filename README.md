# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.


## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
1. Libraries to read csv file.
2. Libraries to convert record to pdf.
3. Libraries to send report (mail,SMs etc).
4. Libraries to perform operations on date and time.


### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | Yes           | Item is required as PDF need to be saved on weekely basis.
Counting the breaches       | Yes           | This is the part of the software to notify the mothly breach count.
Detecting trends            | Yes           | This is the part of the software  being developed.
Notification utility        | Yes           | Item required to notify user by sending mail with report.

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write the count of breaches from BreachCountForMonth Function  .(If no breach then return 0)
4. Write date and time of the record from RecordTrend Function when reading increases continuosly in specified interval of time(30 min)
5. Write "No record found" from  RecordTrend Function when readings are fluctuating in specified interval of time.
6. Write "Report not found" from ReadInputFromCsv when the report in the not stored in the server.
7. Write "Error occured while reading data" from ReadInputFromCsv when exception occured during operation(in the server like shutdown)
8. Write "File is under other operation." from ReadInputFromCsv when the file is opened by other app/operation(Ex:updating monitored values in csv)
9. Write "Report saved successfully." in WriteToPDF when report from csv is generated and saved as pdf in specified location.
10. Write "Path not found." in WriteToPDF when given path not found.
11. Write "Notification sent successfully." from NotifyReortAvailability funtion when the notification gone.(mail/SMS etc)
12. Write "Error occured while notifying." from NotifyReortAvailability function when exception occured in notification utility(Ex server down)


(add more)

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.


| Functionality            | Input                     | Output                      | Faked/mocked part
|--------------------------|--------------             |-----------------------------|---
Read input from server     | csv file                  | internal data-structure     | Fake the server store
Validate input             | csv data                  | valid / invalid             | None - it's a pure function
Notify report availability | PDF file                  | PDF generated               | fake the Notifier 
Report inaccessible server |server path                | Exception/reportExist       | fake the server 
Find minimum and maximum   | csv data                  | csv data/invalid input      | None-pure function
Detect trend               | csv data                  | date and time/Nothing       |  Pure function
Write to PDF               | max,min,breachcount,trend | PDF                         | mock the pdf generation
