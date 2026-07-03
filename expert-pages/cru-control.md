# CRU control

## Configuring the CRU through GUI

Log in to the FLP:&#x20;

{% code overflow="wrap" %}
```shellscript
ssh flp@alio2-flp-focal
```
{% endcode %}

To start the GUI:&#x20;

{% code overflow="wrap" %}
```shellscript
cd /home/flp/cru-sw
source .venv/bin/activate 
python3 COMMON/sj_001_ui.py
```
{% endcode %}

<figure><img src="../.gitbook/assets/SJ_Gui.png" alt=""><figcaption></figcaption></figure>

### Configurations settings
#### RF_4_CF_4_CFC_4_CC_3_Cd_0
* x 0 asic 0 json: /home/flp/cru-sw/COMMON/Calib_Config/RF_4_CF_4_CFC_4_CC_3_Cd_0/ToT_300/SN_D25_D13/fpga1_404_ToTCalibY_20260701_163015/asic0_final_calib_i2c_L1_63.json
* x 0 asic 1 json: /home/flp/cru-sw/COMMON/Calib_Config/RF_4_CF_4_CFC_4_CC_3_Cd_0/ToT_300/SN_D25_D13/fpga1_404_ToTCalibY_20260701_163015/asic2_final_calib_i2c_L1_63.json
* x 1 asic 0 json: /home/flp/cru-sw/COMMON/Calib_Config/RF_4_CF_4_CFC_4_CC_3_Cd_0/ToT_300/SN_D04_D05/fpga1_404_ToTCalibY_20260701_111944/asic0_final_calib_i2c_L1_63.json
* x 1 asic 1 json: /home/flp/cru-sw/COMMON/Calib_Config/RF_4_CF_4_CFC_4_CC_3_Cd_0/ToT_300/SN_D04_D05/fpga1_404_ToTCalibY_20260701_111944/asic2_final_calib_i2c_L1_63.json
#### RF_9_CF_8_CFC_6_CC_3_Cd_0
* x 0 asic 0 json: /home/flp/cru-sw/COMMON/Calib_Config/RF_9_CF_8_CFC_6_CC_3_Cd_0/ToT_500/SN_D25_D13/fpga1_404_ToTCalibY_20260701_182411/asic0_final_calib_i2c_L1_63.json
* x 0 asic 1 json: /home/flp/cru-sw/COMMON/Calib_Config/RF_9_CF_8_CFC_6_CC_3_Cd_0/ToT_500/SN_D25_D13/fpga1_404_ToTCalibY_20260701_182411/asic2_final_calib_i2c_L1_63.json
* x 1 asic 0 json: /home/flp/cru-sw/COMMON/Calib_Config/RF_9_CF_8_CFC_6_CC_3_Cd_0/ToT_500/SN_D04_D05/fpga1_404_ToTCalibY_20260630_203008/asic0_final_calib_i2c_L1_63.json
* x 1 asic 1 json: /home/flp/cru-sw/COMMON/Calib_Config/RF_9_CF_8_CFC_6_CC_3_Cd_0/ToT_500/SN_D04_D05/fpga1_404_ToTCalibY_20260630_203008/asic2_final_calib_i2c_L1_63.json
#### RF_12_CF_10_CFC_6_CC_3_Cd_0
* x 0 asic 0 json: /home/flp/cru-sw/COMMON/Calib_Config/RF_12_CF_10_CFC_6_CC_3_Cd_0/ToT_650/SN_D25_D13/fpga1_404_ToTCalibY_20260701_173930/asic0_final_calib_i2c_L1_63.json
* x 0 asic 1 json: /home/flp/cru-sw/COMMON/Calib_Config/RF_12_CF_10_CFC_6_CC_3_Cd_0/ToT_650/SN_D25_D13/fpga1_404_ToTCalibY_20260701_173930/asic2_final_calib_i2c_L1_63.json
* x 1 asic 0 json: /home/flp/cru-sw/COMMON/Calib_Config/RF_12_CF_10_CFC_6_CC_3_Cd_0/ToT_650/SN_D05_D04/fpga1_404_ToTCalibY_20260630_144147/asic0_final_calib_i2c_L1_63.json
* x 1 asic 1 json: /home/flp/cru-sw/COMMON/Calib_Config/RF_12_CF_10_CFC_6_CC_3_Cd_0/ToT_650/SN_D05_D04/fpga1_404_ToTCalibY_20260630_144147/asic2_final_calib_i2c_L1_63.json

## Changing the trigger delays & restarting the trigger&#x20;

Setting the trigger delay:&#x20;

{% code overflow="wrap" %}
```shellscript
o2-roc-pat-player --id=1165 --pat0=0x36363636 --pat1=0x4b4b4b4b --pat1-trigger-select=0x10 --pat1-delay=21 --pat1-length=16 --pat3=0x36363636 --pat3-length=1
```
{% endcode %}

Setting the system id (which is 39):&#x20;

{% code overflow="wrap" %}
```shellscript
o2-roc-ul --id 1165 --system-id 39 --event-size 8000
```
{% endcode %}

Turning on the trigger:&#x20;

{% code overflow="wrap" %}
```shellscript
cd /home/flp/LTU cat FASTLM | atb 57
```
{% endcode %}

Turning off the trigger:&#x20;

{% code overflow="wrap" %}
```shellscript
cd /home/flp/LTU cat EOT | atb 57
```
{% endcode %}
