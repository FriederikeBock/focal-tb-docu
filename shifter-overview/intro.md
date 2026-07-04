# Introduction

Welcome to the July 2026 FOCAL Testbeam!

## Shift Flow

* At start of shift, make sure to have one of the shifters log in to their CERN account on Mattermost, etc. If it keeps logging you back in to the previous person's account, clear the browser cookies.
* Remember to fill out the End Of Shift (EOS) report during your shift, and submit it as a log in the [ALICE bookkeeping system](http://alio2-flp-focal.cern.ch:4000/). At the beginning of your shift, read the previous shifter's EOS report, so that you are aware of what has been going on before your shift.
* A team of 2 shifters can divide tasks by one person performing the runs and keeping track of the ALICE bookkeeping system, while the other keeps track of the Google Sheets bookkeeping system
* A team of 3 shifters can divide tasks by one person performing the runs, another person keeping track of the ALICE bookkeeping system, and the third person keeping track of the Google Sheets bookkeeping system

## Shifter Screen Layout

* The following layout can be used for convenient data taking

<img src="../.gitbook/assets/Shifters screen 1.png" alt="Left-hand side screeen" width="600">

<img src="../.gitbook/assets/Shifters screen 2.png" alt="Right-hand side screeen" width="600">

**Left-hand side screen**

* On the left-hand side screen, the runs will be executed
* 2 important tabs should be open on this screen:
  * The ECS Control GUI
  * The bias voltage/amplitude modifier (Keithley)
* The terminal should also be visible at the bottom of the screen. Here, the number of events can be seen

**Right-hand side screen**

* On the right-hand side screen, the ALICE booking will be taken care of
* 3 windows will be open on this screen:
  * The QC, where data can be monitored
  * The Infologger, where you can look for errors
  * The ALICE bookkeeping. Here, it is important to log issues if present

**Laptop screen**

* The third screen will be a personal laptop that can easily open the Google Sheets bookkeeping file
* It is a good idea to have the ALICE bookkeeping file open on the laptop as well
  * Here, it is important to log the run number, the environment ID, and the starting time-stamp from the ALICE bookkeeping
  * In case of issues present, log these into the notes section of the sheet

## QUICKSTART: Run Checklist

1. Create new environment in [Control GUI](http://alio2-flp-focal.cern.ch:8080/)
2. Start run from within configured environment
3. Setup the terminal to monitor the trigger (`roc-trig-monitor --i=1165 --upd`).
4. Record run settings in the [google sheet](https://docs.google.com/spreadsheets/d/1CEVsBG8wgO2F9DYG3_Rz1IMYbPuPbzVct7_hPUwUYgk/edit?usp=sharing) and add them as a log in the [ALICE bookkeeping system](http://alio2-flp-focal.cern.ch:4000/)
5. In the [ALICE bookkeeping system](http://alio2-flp-focal.cern.ch:4000/), tag run with appropriate beam type and energy
6. Monitor [run QC](http://alio2-flp-focal.cern.ch:8082/) and [error log](http://alio2-flp-focal.cern.ch:8081/?q=\{%22message%22:\{%22exclude%22:%22TRG%20error%20call=%5C%22RunList%5C%22%25%0ASubTimeFrame%20deserialization%20failed.%25%0ADirectory%20for%20\(Sub\)TimeFrame%20file%20sink%20cannot%20be%20created%25%22},%22severity%22:\{%22in%22:%22E%20F%20W%22\}})
7. Log any issues during the run in the [ALICE bookkeeping system](http://alio2-flp-focal.cern.ch:4000/)
8. Stop run when needed from [Control GUI](http://alio2-flp-focal.cern.ch:8080/)
9. Shutdown environment (**do not kill!**)
