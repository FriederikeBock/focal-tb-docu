---
description: >-
  This page explains how setup the different HGCROC boards with their respective
  FPGA boards.
---

# Setting up the HGCROC boards

## HGCROC proto-boards with KCU

<figure><img src="../.gitbook/assets/Screenshot from 2025-11-17 15-29-43.png" alt=""><figcaption></figcaption></figure>

The following cables need to be connected in order to setup the HGCROC for local testing:

* ethernet (either 1GbE or 10GbE connections) - make sure to use CAT7 ethernet cables if you choose 10GBase-T SFP + copper ethernet cables. Otherwise fiber connection with appropriate network card and apaters would work too.
* Power ([replacement](https://www.digikey.fr/en/products/detail/sl-power-advanced-energy/TE90A1251N01/6580452))
* programming cable (micro USB to USB-A) from DAQ computer
* HV cables to HGCROC proto boards - individually for each HGCROC ([connectors](https://www.digikey.com/en/products/detail/phoenix-contact/1803594/260531))
* SMA inputs for external triggering and syncronization. **ATTENTION:** these should only be provided with 1.8 V (step down from classical 5V NIM signal needed).

Details on where each cable goes can be found in the picture above. Don't forget to also set the jumper to provide only 1.2 V after boot (right side red box in picture).

* Important the `DataPort` needs to be set to <mark style="background-color:$danger;">ON</mark> hence port 11001 !!
