# Logs and Bookkeeping

Error monitoring during runs is done by checking the Infologger, which can be found [here](http://alio2-flp-focal.cern.ch:8081/?q={%22message%22:{%22exclude%22:%22TRG%20error%20call=%5C%22RunList%5C%22%25%0A%0ASubTimeFrame%20deserialization%20failed.%25%22},%22severity%22:{%22in%22:%22E%20F%22}}). 

To keep track of each run that we perform during the testbeam, it is important to be consistent about recording problems and solutions as they come up. To this end, you should use the bookkeeping system that can be accessed [here](http://alio2-flp-focal.cern.ch:4000/).

## Infologger

### Modes

The infologger can run in two modes: **Query** and **Live**. As the names imply, the **Live** mode allows you to monitor ongoing runs and catch error messages as they come up, while **Query** allows you to search through the error log. 

When you first enter the infologger, its message display setting will automatically be set to **Query**, so you must manually change it over to **Live**. 

### Filters
There are a variety of options for what messages the infologger can be configured to display. 
- This is mostly useful if you would like to perform a query, and look for errors that came up during a specific run or time period 
- The filters are displayed as headers (see Hostname, Rolename, PID, etc in the image above) and can be controlled by typing in the two rows of text field below each header

<img src="../.gitbook/assets/infologger.png">

- The first header (on the far left of the GUI) is **Date/Time**. As indicated by the GUI text, you can set the time interval you want to search in by adding the start time to the top row, and the end time to the bottom.
- For the rest of the filters, the top row works as an include filter, while the bottom works as an exclude filter
- So, for example, to look at error messages coming from a specific run, enter the run number in the first text field under the header **Run** 
- Press the **Query** button again to apply the filters and update the display

**NB**: These filters are not removed automatically! If you decide to switch back to **Live** mode after making a filtered query, make sure to remove whatever filters you have added. If you can't remember what you added and what was already there, reload the page with the default filter configuration we have set from the [link](http://alio2-flp-focal.cern.ch:8081/?q={%22message%22:{%22exclude%22:%22TRG%20error%20call=%5C%22RunList%5C%22%25%0A%0ASubTimeFrame%20deserialization%20failed.%25%22},%22severity%22:{%22in%22:%22E%20F%22}}). 

### Default Filter Settings
Some error messages are known by us going in to the test, i.e. not important for you as the shifter to worry about. We have set up some default filter settings for the shifter layout, so that you do not have to worry about them! The link above automatically applies those filters when you load the page. If you are suddenly getting a bunch of errors, your first port of call should be to double check that you haven't accidentally removed these filters, just in case.


## Bookkeeping

The bookkeeping system helps us to keep track of the settings of each run. It also becomes a record of problems that come up (and, importantly, how to solve them). To see the list of runs, click on the **Run** header. To see a specific run, click on the corresponding run number in the list.

### Tagging runs
2 tags are needed for each run - beam type and energy.

- Once inside the run, click on **Edit Run**
- A field with the tags will then pop up, and you can tick the tag to select it:
<img src="../.gitbook/assets/tag_run.png">

- Once the runs are tagged, you'll find the beam configuration under "tags" in the logbook
<img src="../.gitbook/assets/tag_example.png">

In the future, this will help a lot to filter runs, because this can be used in the bookkeeping filter tool:
<img src="../.gitbook/assets/logbook_filters.png">

### Making Logs
When problems come up during a run, note them down using the bookkeeping **Log** functionality. 

- Next to **Edit Run**, you will see another button, **Add log to this run**
- Give your log a relevant name and tags, and then describe the error that came up, including any relevant error messages from infologger, etc

<img src="../.gitbook/assets/log_eg.png">

- Finally, click the **Post log** button to publish it
- Once your log is posted, other people can reply to it, for example with solutions to the described problem

It is important to make a log of any issues that are solved during a run unless otherwise informed!

## Logbook Template

### General information
**Run number:**

**Number of events:**

**Synchronized:**

### Beam configuration
**Particle:**

**Energy (GeV):**

### Table position
**Horisontal position:**

**Vertical position:**

### FoCal-H settings
**Trigger scheme:**

**Threshold:**

**Gain:**

**Bias:**

**ECAL in front**

**Run number / configuration file:**

**Saved:**

### Other comments
xx


## IMPORTANT NOTES
- Always check your infologger mode! If an environment or run is in error and you are not seeing any error messages, make sure it is not because you are accidentally stuck in **Query**.
- It is advised that you clear all error messaages and return to **Live** mode before you deploy a new environment, so that you do not get confused by error messages coming from previous environments/runs.
