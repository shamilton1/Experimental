This register allows you to set the number corresponding to the Transceiver DRP control mailbox or the
Transceiver control register bank to be accessed. The range is 0 to N-1,
where N is the value returned from the [Number of Transceiver][] Interfaces
register.

|Bit|Default Value|Access Type|Description|
|:-----:|:-----:|:-----:|-----|
|[0]|0|RW|Set when any bit in image completion vector=0|
|[1]|0|RW|AXIMM Write Error|
|[2]|0|RW|CmDQ Overflow|
|[29:3]|0|RW|Reserved|
|[31:30]|0|RW|Download Image Source|

