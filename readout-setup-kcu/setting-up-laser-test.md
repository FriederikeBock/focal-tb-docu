---
description: This page describes the electronics setup for the lab laser test
---

# Setting up the laser test

## Trigger scheme

The triggers for the laser system (PDL 800-B) and for the data acquisition system (KCU board) are both from the same function generator (TG5012A).

<figure><img src="../.gitbook/assets/LaserTest-Page-2.drawio.png" alt=""><figcaption></figcaption></figure>

**Note:** The two outputs from TG5012A is not automatically synchronized, so you need to press the \`align\` button after changing the frequency settings.

Because of PDG 800-B is triggered on the falling edge and KCU is triggered on the rising edge, you need to adjust the delay settings of the KCU trigger by the width of the laser pulse in order to ensure they roughly coincide.

<figure><img src="../.gitbook/assets/IMG_0582.png" alt=""><figcaption><p>The function generator (left) and the laser system (right) used in September 2026.</p></figcaption></figure>

The sampling clock on the front-end ASIC (H2GCROC) is derived from the 40MHz clock provided by the KCU board, such that the actual sampling is asynchronized with the laser signal, creating a time jitter between the laser pulse and the ASIC sampling. Further, the falling time of the signal from the function generator is limited to \~ 5ns, bringing an additional timing uncertainty in the same order to the actual laser timing.

<figure><img src="../.gitbook/assets/YellowKCUTrigIN_BlueLaserTrigIn.png.avif" alt=""><figcaption><p>Oscilloscope output cross checking the signal alignment for  KCU trigger input (yellow) and laser input (blue).</p></figcaption></figure>

<figure><img src="../.gitbook/assets/YellowKCUTrigIN_BlueLaserSynchOUT.png (2).avif" alt=""><figcaption><p>Oscilloscope output cross checking the signal aligment and settting for KCU trigger input (yellow) and Laser sync output (blue).</p></figcaption></figure>

Please use the following settings for the pulse generator (proved to work Oct 2026):

* ch 1: KCU trigger IN
  * 10 mus pulse
  * 0 mus delay
  * 900 mV
  * 10Hz
* ch 2: Laser trigger IN
  * 100ns pulse
  * 0 mus delay
  * 850 mV pulse
  * 10Hz

Don't forget to press the **SYNC-button.**

In the laser test in September 2026, an L1Offset value of 8 (the default value) and an ex trg delay of 16 (set in H2GDAQ) is used, effectively delaying the sampling time by 8 clock cycles (8 \* 25 ns = 200 ns).
