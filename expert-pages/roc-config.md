
# RoC (Readout Chip) Configuration

The signal from SiPMs is weak and fast, so it needs to be amplified and digitized. This is done by the RoC (Readout Chip) which is H2GCROC in our case.
Configuring the RoC is done via a Terminal UI in the FLP. As always, you need to log in to the FLP first:

```shellscript
ssh flp@alio2-flp-focal
```

> **Note:** If you cannot ssh into the FLP, you can try to ping it using the command `ping alio2-flp-focal`. If you cannot ping it, call Shihai/Tommaso.

## Program the CRU

(run as root)

```shellscript
cd ~/focaltb_fw/2025-10
for i in 1; do /root/intelFPGA_pro/24.1/qprogrammer/quartus/bin/quartus_pgm --cable=$i --mode=JTAG --operation="p;cru_paddedx12.sof"; done;
source ~/rescan_only.sh
```

## Load the configuration files

The sequence of steps for loading the configuration files for the "old firmware" is as follows:

0. Open the Terminal UI
1. Set the local clock source
2. Initialize the lpGBT
3. Load the configuration files
4. Unset the local clock source / Set the LTU clock source
5. Set the roc-config
6. Set the pattern player
7. Initialize the lpGBT (same as step 2)
8. Set the User Logic

> **Note:** The "new firmware" is not verified by July 4th, so only the "old firmware" sequence should be followed.

### Open the Terminal UI

First, we need to open the Terminal UI:

```shellscript
cd /home/flp/cru-sw
source .venv/bin/activate
python3 COMMON/sj_001_ui.py
```

Then you should see it pop up like this:

![TUI main screen](../.gitbook/assets/TUI_main.png)

### Set the local clock source

> **Warning:** We only need to do this if it is made clear that we are using the old firmware.

To change the clock source, go to the `Connection` tab on the left, and in the `clock-config.py` section:

![TUI local clock source](../.gitbook/assets/TUI_clock_local.png)

Set the `Clock source` to `local` and **uncheck** the `PON upstream` option. Then click `Run clock-config.py` button. You should see the following output if successful:

![TUI clock success output](../.gitbook/assets/TUI_clock_success.png)

If the number of up links are not 2, or it fails, **retry 3 times**. If it still fails, call Shihai.

### Initialize the lpGBT

There are two lpGBT chips used, so to initialize them, go to the `focal-hcal-mb6x-lpgbt-cli.py` section of the `Connection` down at the bottom, set the `MB6x channel` to `0` and click `Run MB6x init` button, if successful, **set the `MB6x channel` to `1` and click the button again**.

### Load the configuration files

Go to the `JSON loader` tab on the left, and in the `Config JSON files` section, set the files as follows:

**RF_4_CF_4_CFC_4_CC_3_Cd_0**
x 0 ASIC 0: /home/flp/cru-sw/COMMON/Calib_Config/RF_4_CF_4_CFC_4_CC_3_Cd_0/SN_D13_D25_D5_D12/asicD13_final_calib_i2c_L1_40.json
x 0 ASIC 1: /home/flp/cru-sw/COMMON/Calib_Config/RF_4_CF_4_CFC_4_CC_3_Cd_0/SN_D13_D25_D5_D12/asicD25_final_calib_i2c_L1_40.json
x 1 ASIC 0: /home/flp/cru-sw/COMMON/Calib_Config/RF_4_CF_4_CFC_4_CC_3_Cd_0/SN_D13_D25_D5_D12/asicD5_final_calib_i2c_L1_40.json
x 1 ASIC 1: /home/flp/cru-sw/COMMON/Calib_Config/RF_4_CF_4_CFC_4_CC_3_Cd_0/SN_D13_D25_D5_D12/asicD12_final_calib_i2c_L1_40.json

**RF_12_CF_10_CFC_6_CC_3_Cd_0**
x 0 ASIC 0: /home/flp/cru-sw/COMMON/Calib_Config/RF_12_CF_10_CFC_6_CC_3_Cd_0/SN_D13_D25_D5_D12/asicD13_final_calib_i2c_L1_40.json
x 0 ASIC 1: /home/flp/cru-sw/COMMON/Calib_Config/RF_12_CF_10_CFC_6_CC_3_Cd_0/SN_D13_D25_D5_D12/asicD25_final_calib_i2c_L1_40.json
x 1 ASIC 0: /home/flp/cru-sw/COMMON/Calib_Config/RF_12_CF_10_CFC_6_CC_3_Cd_0/SN_D13_D25_D5_D12/asicD5_final_calib_i2c_L1_40.json
x 1 ASIC 1: /home/flp/cru-sw/COMMON/Calib_Config/RF_12_CF_10_CFC_6_CC_3_Cd_0/SN_D13_D25_D5_D12/asicD12_final_calib_i2c_L1_40_dummy.json

Then, click the `Load JSON configs` button, and you should see the following output flowing in the log window:

![TUI I2C running output](../.gitbook/assets/TUI_i2c_running.png)

If you see lots of RD_WAIT errors, make sure which firmware is loaded and check with experts if you need to do the `Set the local clock source` step above.

### Unset the local clock source / Set the LTU clock source

> **Warning:** Only do this if it is made clear that we are using the old firmware, and you have already set the local clock source.

It is the same section but the reverse. 

![TUI LTU clock source](../.gitbook/assets/TUI_clock_ttc.png)

Set the `Clock source` to `ltu` and **check** the `PON upstream` option. Then click `Run clock-config.py` button. You should see the same output as above if successful.

### Set the roc-config

Click the `Run roc-config` button in the `Connection` tab.

### Set the pattern player

Click the `Run o2-roc-pat-player` button in the `Connection` tab.

### Set the User Logic

Click the `Run o2-roc-ul` button in the `Connection` tab.
