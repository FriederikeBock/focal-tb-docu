# Using the server

If you want root access, instead of writing your username, use root as username, and then the same password as before.

If you want to remote in on the server, you can use the command&#x20;

{% code overflow="wrap" %}
```
ssh username@AliFoC-XX
```
{% endcode %}

or&#x20;

{% code overflow="wrap" %}
```
ssh AliFoc-XX -l username
```
{% endcode %}

If you then want root from your remote access, use command su, and you will then have root access.

If you want to copy a drive, to e.g. make a redundant bootdrive, you can then use the command:&#x20;

{% code overflow="wrap" %}
```
dd if=/dev/sda of=/dev/sdb bs=4M status=progress 
```
{% endcode %}

When doing this step, it is important, to have the harddrive you are copying from, set as the bootdrive, while the harddrive you are copying onto is not. It is also easier if the drive you are copying to is in the second bay.

To completely wipe a drive, use the command:&#x20;

{% code overflow="wrap" %}
```
dd if=/dev/zero of=/dev/sdb bs=4M status=progress
```
{% endcode %}

In this command you are just copying the disk full of zeros which essentially wipes the drive.

