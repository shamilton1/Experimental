Reading this register returns the number of GT_CHANNEL blocks (same as
the number of lanes). The number returned here can be used by software to
loop round the correct number of times to configure all the transceivers in
the core using the Transceiver.

|Bit|Default Value|Access Type|Description|
|:-----:|:-----:|:-----:|-----|
|[0]|0|RW|Set when any bit in image completion vector=0|
|[1]|0|RW|AXIMM Write Error|
|[2]|0|RW|CmDQ Overflow|
|[29:3]|0|RW|Reserved|
|[31:30]|0|RW|Download Image Source|
