---
description: >-
  This page is to show how to do calibration comparisons based on the data taken
  with the HGCROC using injections.
---

# Calibration comparisons

This section heavily relies on the frame work explained on a [separate page](https://friederikebock.gitbook.io/epiclfhcaltb-ana/tb-analysis-basics/tb-analysis-basics) for installation instructions please have look there. The main prerequisits are a working root installation.&#x20;

## Converting the calib-outputs

A first introduction to the CalibParser can also be found [there](https://friederikebock.gitbook.io/epiclfhcaltb-ana/calibration/reading-hgcroc-online-calibrations). As the outputs we will be processing are based of the [H2GCalibX](setting-up-daq-pc.md#software-installation) please use the following commands:

{% code overflow="wrap" %}
```bash
mappingFile=../configs/FOCalTest2026/mapping_injectionTest.txt
runList=../configs/FOCalTest2026/DataDB_InjectionTestFocal_202604.csv

./ParseCalibSamples -i $InputTextBase -d 1 -I -m $mappingFile -r $runList -n $RunNr -o $RootOutputFileName -p $PlottingDirectory

```
{% endcode %}

The `ParseCalibSamples`  program take multiple options:

* &#x20;`-i`  is followed by the input text file base name. These tend to have the following format:&#x20;

{% file src="../.gitbook/assets/205_Injection_asic4_injdac250_mg7_pack8_chn76_val0.csv" %}

You would wanna give the file path and name without `_val0.csv` . Make sure the file has the correct header (should start with `#ch`) in the first line. If it doesn't please fix them using the following script.

{% file src="../.gitbook/assets/FixInjectionsFormat_add_header_and_ids.sh" %}

{% code overflow="wrap" %}
```bash
bash FixInjectionsFormat_add_header_and_ids.sh 205_Injection_asic4_injdac400_mg7_pack8_chn76_val0.csv
```
{% endcode %}

* `-d`  is followed by a debug option \[1-3], enabling different levels of couts in the code
* <mark style="background-color:$info;">`-I`</mark>  <mark style="background-color:$info;"></mark><mark style="background-color:$info;">triggers the reading of the</mark> <mark style="background-color:$info;"></mark><mark style="background-color:$info;">`H2GCalibX`</mark> <mark style="background-color:$info;"></mark><mark style="background-color:$info;">inputs from the injection scans. IMPORTANT!</mark>
* `-m $mappingFile`  is required to define how the channels are related to the real readout geometry and an example file can be found in [../configs/FOCalTest2026/mapping\_injectionTest.txt](https://github.com/eic/epic-lfhcal-tbana/blob/main/configs/FOCalTest2026/mapping_injectionTest.txt)
* `-r $runList`  is necessary for correct labeling and an example of such run list can be found in  [../configs/FOCalTest2026/DataDB\_InjectionTestFocal\_202604.cs](https://github.com/eic/epic-lfhcal-tbana/blob/main/configs/FOCalTest2026/DataDB_InjectionTestFocal_202604.csv)v the run numbers are here freely chosen, as the injections in principle don't store this information&#x20;

{% code overflow="wrap" %}
```csv
year 2026
month 04
readout HGCROC
facility CERN
beam-line injection
#Run Number,type,bias Voltage,V_br,machine gun,dead time,phase,nrKCU,nrAsic,RF,CF,CC,CFcomp,mode,value,location,comments
1,injection,0,38.3,7,0,1,0,4,4,8,4,8,0,250,FOCALTests-DefSettingsShihai-ORNL04-05/test_wo_detector/302_ToTCalib_Target400/205_Injection_Low/205_Injection_20260424_165941/205_Injection_asic4_injdac250_mg7_pack8_chn76,
2,injection,0,38.3,7,0,1,0,4,4,8,4,8,0,100,FOCALTests-DefSettingsShihai-ORNL04-05/test_wo_detector/302_ToTCalib_Target400/205_Injection_Low/205_Injection_20260424_153821/205_Injection_asic4_injdac100_mg7_pack8_chn76,
```
{% endcode %}

It is important to add all relevant information, i.e. what it is type="injection", as well as all the information you can gather on the setting for the `RF, CF, CFcomp, CC,` high or low injection (mode), the injection value and where it can be found for your own convenience.

* `-n $RunNr`  defines what run number you assign, it has to be contained in the runList you have given before. Otherwise it will crash.
* `-o $RootOutputFileName`  defines the root output file name for everything which is stored
* `-p $PlottingDirectory`  defines where the plots go and enables the plotting. This is also necessary in case you want to later make any comparison plots.

For all asics the following overview plots will be created

{% file src="../.gitbook/assets/TOA_Asic00.pdf" %}

{% file src="../.gitbook/assets/TOT_Asic00.pdf" %}

{% file src="../.gitbook/assets/Waveform_Asic00.pdf" %}

## Comparing the calibration outputs

Once you converted the calib outputs according to the previous instructions you can now compare them using the following command

{% code overflow="wrap" %}
```bash
./CompareInjection -d 1 -e 1 -E 1 -f -H -I comparisonInjections_RFVaried.txt -o testingPlots/newInjection.root -O testingPlots/RFVaried/ -r ../configs/FOCalTest2026/DataDB_InjectionTestFocal_202604.csv
```
{% endcode %}

The helper function explains the options:&#x20;

{% code overflow="wrap" %}
```bash
./CompareInjection --help
Usage:
./CompareInjection [-option (arguments)]
Options:
-d [0-3] Debugging mode
-e [0-1] extended plotting
-E [1-X] histo reading options for expanded file list
-f       Force to write output if already exist
-F fff   set explicit plot extension explicitly, default is pdf 
-H       switch to HGCROC output
-i uuu   Input file list
-I uuu   expanded input file list
-L [1-63]restrict max layer plotting
-o vvv   Output file name (mandatory)
-O kkk   Output directory name for plots (mandatory)
-r rrr   Name of run list file  2024 PS TB [../configs/DataTakingDB_202409_CAEN.csv] 
-R       Trending plots versus run #
-V       Trending plots versus Vop
-h       this help

```
{% endcode %}

We are here uisng the expanded histo reading option (`-E 1`) as we don't only wanna compare the calib parameters which are stored. `-H`  switches to the HGCROC outputs. This allows to produce among other thes following plots:

{% file src="../.gitbook/assets/TileWaveOverlay_Mod00_Layer01.pdf" %}

{% file src="../.gitbook/assets/WaveOverlay_Asic00.pdf" %}

{% file src="../.gitbook/assets/HGPedSummary_RunOverlay.pdf" %}

{% file src="../.gitbook/assets/HGPedWidthSummary_RunOverlay.pdf" %}

If only one parameter for RF, CF, CFComp or CC is varied the labeling will be automatically be picking up the primary variation and instead of the run labels the correct values will be displayed for the respective parameter. An example configuration file is given below.

{% file src="../.gitbook/assets/comparisonInjections_RFVaried.txt" %}
