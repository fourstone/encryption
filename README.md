# encryption with SSDs
Just got 2 Samsung Evo 850 500G SSDs into my machine. 
Hope is to be able to utilize dedup with ZFS on top of the hardwarebased encryption

sedutil-cli --yesIreallywanttoERASEALLmydatausingthePSID <PSID> /dev/sda
sedutil-cli --initialSetup <password> /dev/sda
sedutil-cli --enableLockingRange 0 <password> /dev/sda

shutdown, then start from machine turned off

sedutil-cli --setLockingRange 0 rw <password> /dev/sda
sedutil-cli --setMBRDone <password> /dev/sda

So far for today, we will see how it goes with automatic unlocking and starting the zfs filesystem as I do not want to use a PBA as it is not my system drive and the target is to keep it all startable via ssh interaction without having to use IPMI or local console as a PBA would require.
As of today I am not aware of a remote-capable PBA for SEDUTIL.
