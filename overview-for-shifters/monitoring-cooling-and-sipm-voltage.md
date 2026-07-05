---
description: >-
  This pages describes how to setup the temperature and SiPM voltage monitoring
  and controls on the "Calibration PC" (lfhcal-pc).
---

# Monitoring Cooling & SiPM voltage

## Setting up the monitoring & controls

For opening the dashboard for control and monitoring of the SIPM bias:

```
cd /home/lfhcal/ivmonitor/monitoring
source .venv/bin/activate
python3 dashboard.py --port 5050 
```

*   You will see something like this:&#x20;

    <figure><img src="https://codimd.web.cern.ch/uploads/upload_89004a4e366ef44a25404b90cb6781ce.png" alt=""><figcaption></figcaption></figure>
* In the printout you will see the address link to visualize the GUI. The default is http://127.0.0.1:5050/
* Once you open the GUI you will see a first part dedicated to applying the bias, and a lower part dedicated to the monitoring of current and Voltage.



![](https://codimd.web.cern.ch/uploads/upload_43518c7258db995dc8559b9f9a56da5c.png)

## To set the Bias Voltage:

![](https://codimd.web.cern.ch/uploads/upload_321e4dc1a5475b28ca4b41ce44040d98.png)

In the Dashboard, input the desired voltage and press "Apply".

To change Voltage, you will be forced to STOP and Apply again. In the back-hand that will open the connection with the Keithley (IP specified in the config.ini), apply the bias, and begin monitoring.

It will store locally a file and, at the same time, push a file to DataBase. The name of the files are automatically created as:

`<Voltage>_SIPM<_label>` e.g. `45V_SIPM` or `45V_SIPM_debug` (if a label is added)

By Default (it is suppose to work like that!), the system will append your result to the output files with the same name.

Make sure to highlight the Database box, so that the data is also stored there!

#### NOTE:

This interface replaces the standard Keithley WebUI. Therefore if you want to connect to that one, you will have to stop the process pressing the "STOP" button in the interface. Note that on the right of the button you will also see the process ID, in case you need to kill it from terminal. In that case you can run:

{% code overflow="wrap" %}
```
kill -9 <processID>
```
{% endcode %}

## Monitoring:

**!! Remember to refresh the page to see the newly produced files in the drop down menu !!**

Once the correct file is selected, just include in the plot the portion of time you'd like to monitor!

## Notification:

Every time the Voltage changes, the communication is lost, or the processed is closed, you will receive a notification in the Shifter MM group from our biasbot. Please keep an eye on it:

![](https://codimd.web.cern.ch/uploads/upload_2d9ed9e1a3fb3204146fa2f25233c160.png)

