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

However also a prepared bash script exists [`convertDataHGCROCFocal_TBSPSH4_2026.sh`](https://github.com/eic/epic-lfhcal-tbana/blob/main/NewStructure/convertDataHGCROCFocal_TBSPSH4_2026.sh). In this script you will have to update the locations of the raw data (`dataRaw`) and where you would like the converted data to go (`dataDir`) ideally this is done under and if condition with your favorite `$USERNAME` . In case you added more runs make sure you updated the `runList`-file. For an example of such configuration have a look below

```bash
if [ $1 = "fbockLaserOct" ]; then 
  dataRaw=/media/fbock/FrediExt4TB/FOCAL_TB/202610_FocalLaser/raw/            # source directory for output files from DAQ system
  dataDir=/media/fbock/FrediExt4TB/FOCAL_TB/202610_FocalLaser/HGCROCData      # base directory for root trees  fi
  # global run list & mapping for laser tests Oct 2026
  mapping=../configs/FOCalTest2026/mapping_LaserTestFocal_202610_BottomLeft.csv
  runList=../configs/FOCalTest2026/DataDB_LaserTestFocal_202610.csv
fi
```

You can then afterwards run the script with your adapted user settings. Make sure you actually set the run numbers you would like to convert in the respective set option

```bash
# run conversion
bash convertDataHGCROCFocal_TBSPSH4_2026.sh $USERNAME Oct
```

## Basic Calibrations

During data taking make sure you also take one true pedestal run without any external triggers with the setup.  This respective pedestal run can then be analyzed to ascertain the baseline pedestal level and electrical noise in the system. For a more detailed description how to start this for a single run including plots please have a look a the corresponding section in the LFHCal tutorial ([pedestal section](https://friederikebock.gitbook.io/epiclfhcaltb-ana/calibration/pedestal-extraction#hgcroc-data)).&#x20;

Moreover, the TOA phase offset correction has to be determined every time the KCU has been restarted (ideally this has been marked in the logbook). A description on how this can be done in detail can be found in the [TOA phase correction section](https://friederikebock.gitbook.io/epiclfhcaltb-ana/calibration/toa-phase-extraction) of the LFHCal tutorial.&#x20;

Last but not least these pieces have to be put together and applied to the laser runs taken in order to correctly visualize the waveforms.&#x20;

All of these steps can be run using a prepared steering script, which needs to be run after the conversion step in the following order:

```bash
# Example processing steps
# extraction of pedestals for all October pedestal runs
bash runHGCROCCalibration_FocalLaser_2026.sh $USERNAME pedestal Oct 
# extraction of the ToA phase for the RF4 first runs (can be applied for all Oct runs)
bash runHGCROCCalibration_FocalLaser_2026.sh $USERNAME toaPhase RF4
# application of pedestal, ToA phase correction and bad channle map to the data
bash runHGCROCCalibration_FocalLaser_2026.sh $USERNAME calibMuon BCTOA Oct_RF4_V43_T-27
# visualization of waveforms and basics of TOT analysis per run per cell
bash runHGCROCCalibration_FocalLaser_2026.sh $USERNAME wave Oct_RF4_V43_T-27
```

Currently all runs from the October laser data taking campaign are included and the following set names are consistently implemented for the `calibMuon` and `wave` options:

* `Oct_RF4_T22`
* `Oct_RF4_V43_T-27`
* `Oct_RF4_V45_T-27`
* `Oct_RF12_V43_T-27`
* `Oct_RF12_V43_T22`
* `Oct_RF12_V45_T-27`
* `Oct_RF12_V45_T22`
* `Oct_RF9_V43_T-27`
* `Oct_RF9_V45_T-27`
* `Oct_RF9_V43_T22`
* `Oct_RF9_V45_T22`

Additionally some options are already implemented for the September set as well.&#x20;

