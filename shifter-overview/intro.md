# Introduction to Testbeam Shifts

Welcome to the July 2026 FOCAL Testbeam! 

## Shift Flow
- At start of shift, make sure to have one of the shifters log in to their CERN account on Mattermost, etc. If it keeps logging you back in to the previous person's account, clear the browser cookies.'
- Remember to fill out the End Of Shift report during your shift, and submit it as a log in the [ALICE bookkeeping system](http://alio2-flp-focal.cern.ch:4000/).
- A team of 2 shifters can divide tasks by one person performing the runs and keeping track of the ALICE bookkeeping system, while the other keeps track of the Google sheets bookkeeping system

## Shifter Screen Layout
- The following layout can be used for convenient data taking


## QUICKSTART: Run Checklist
1. Create new environment in [Control GUI](http://alio2-flp-focal.cern.ch:8080/)
2. Start run from within configured environment
3. Setup the terminal to monitor the trigger (`roc-trig-monitor --i=1165 --upd`).
4. Record run settings in the [google sheet](https://docs.google.com/spreadsheets/d/1CEVsBG8wgO2F9DYG3_Rz1IMYbPuPbzVct7_hPUwUYgk/edit?usp=sharing) and add them as a log in the [ALICE bookkeeping system](http://alio2-flp-focal.cern.ch:4000/)
5. In the [ALICE bookkeeping system](http://alio2-flp-focal.cern.ch:4000/), tag run with appropriate beam type and energy
6. Monitor [run QC](http://alio2-flp-focal.cern.ch:8082/) and [error log](http://alio2-flp-focal.cern.ch:8081/?q={%22message%22:{%22exclude%22:%22TRG%20error%20call=%5C%22RunList%5C%22%25%0ASubTimeFrame%20deserialization%20failed.%25%0ADirectory%20for%20(Sub)TimeFrame%20file%20sink%20cannot%20be%20created%25%22},%22severity%22:{%22in%22:%22E%20F%20W%22}})
7. Log any issues during the run in the [ALICE bookkeeping system](http://alio2-flp-focal.cern.ch:4000/)
9. Stop run when needed from [Control GUI](http://alio2-flp-focal.cern.ch:8080/)
10. Shutdown environment (**do not kill!**)
