vhost style megasas LIO driver and QEMU eventfd patches

This code was originally developed against LIO + QEMU code
from the Feb 2013.

As per Dr. Hannes:

"Attached is the latest version (v6) of the rts_megasas combo.
As threatened I've updated the emulation to a later silicon 
(9260-4i), so that Windows _might_ be compelled to use MSI/MSI-X.

As it turns out, that worked in the sense that Windows indeed tries 
to activate MSI/MSI-X. However, the idea of how an MSI-X 
implementation should work seems to be different on the Qemu and the 
Windows side.

When I _enable_ MSI-X support in the driver I'll get a nice BSOD 
when booting Win Vista.
Windows 7 _thinks_ it has enabled MSI/MSI-X (can't tell which), 
whereas Qemu still feels that both are disabled and uses INTx.
Consequently Windows 7 installation hangs with default settings.

However, when I disable just MSI-X (MSI still enabled) with passing
'use_msix=false' to the rts_megasas driver in qemu Windows uses INTx 
and everything's working.

Except for MSI, of course.

So it really looks like an incompability between Qemu MSI/MSI-X 
implementation and Windows. Which probably will have to be tracked 
down eventually.

On the good side the driver seems to be stable, and I even managed 
to get the 'megacli' command running under windows. Which displayed 
the disks and everything.
The 'MSM' (ie the UI version) worked, too, but failed to display any 
disks. Probably all the better as you couldn't modify the RAID 
settings anyway :-)"
