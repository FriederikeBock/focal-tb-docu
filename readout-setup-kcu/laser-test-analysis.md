---
description: This section explains the broad strokes of the laser test analysis.
---

# Laser test analysis

This section heavily relies on the framework explained on a [separate page](https://friederikebock.gitbook.io/epiclfhcaltb-ana/tb-analysis-basics/tb-analysis-basics) for installation instructions please have look there. The main prerequisites are a working root installation.

The main purpose of the laser tests is the cross calibration of the ADC and TOT signals of the HGCROC. For them to be useful for the TB analysis the same calibration settings as during the TB are used.&#x20;

An extensive set was taken during October/November with a cone installed at the front of the FOCal-H. This allowed the laser light to be dispersed over multiple channels by using 1-2 lenses and attenuate the emitted light simultaneously. The most consistent result was reached with a single lense.&#x20;

To study either all channels simultaneously, or specific channels only an additional 3D printed mask was installed for a subset of runs.&#x20;

## Converting the data

The logbook for the October data taking can be found [here](https://docs.google.com/spreadsheets/d/1ukGmXOEbvxOJ1PtvSj__rN_RmVk7UoduYvTIm1c01gU/edit?usp=sharing). It has multiple tabs, please navigate to <kbd>Oct\_laser</kbd>  for the detailed table & <kbd>Oct laser\_runplan</kbd> for the definition of the groups.&#x20;

The data are currently primarily stored on the DAQ computer from the lfhcal crew, please contact Friederike for the details. A general introduction on how to convert the data can be found [here](https://friederikebock.gitbook.io/epiclfhcaltb-ana/tb-analysis-basics/converting-the-data#hgcroc-data-conversion), please read it in order to understand the general concepts.

Running the converter for a single file can be done as follows:

{% code overflow="wrap" %}
```bash
mapping=../configs/FOCalTest2026/mapping_LaserTestFocal_202610_BottomLeft.csv
runList=../configs/FOCalTest2026/DataDB_LaserTestFocal_202610.csv

./Convert -d 0 -f -w -c $dataRaw/Run$runNr.h2g -o $dataDir/rawHGCROC_$runNr.root -m $mapping -r $runList
```
{% endcode %}

However also a prepared bash script exists .&#x20;

