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

## September & October 2026 setup

Illustrations of the setup of September and October 2026 can be found below. In both cases the laser was mounted in a fixed position at the front of the FOCal-H module. The scans in September were done at different temperatures & for different PCB boards (meaning the position of the laser cone on the FOCal-H module was changed). For the October campaign the same PCB was under test but a different fraction of channels was enabled by a plastic mask.&#x20;

<figure><img src="../.gitbook/assets/IllustrationLaserTests.png" alt=""><figcaption><p>Illustration of Laser setup for 2026 September and October laser tests. </p></figcaption></figure>

<div><figure><img src="../.gitbook/assets/IllustrationLaserTestsWithMask.png" alt="" width="563"><figcaption><p>Illustration of Laser setup for 2026 October laser tests with the mask applied, blocking part of the laser light at the front of the module. </p></figcaption></figure> <figure><img src="../.gitbook/assets/MaskV2.png" alt="" width="188"><figcaption><p>Mask for the front of the FOCal-H Protoype 3 (equivalent of ¼ of TB coverage). This mask can be used to either have all slots open, only 1 or several (i.e. 2 center ones in parallel) &#x26; is used for cross talk evaluations.</p></figcaption></figure></div>

