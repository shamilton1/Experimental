Set the number of AXI clock cycles to wait before terminating the AXI4-Lite
access without completing.
If using timeout, the value must be modified according to the relationship
between the AXI and DRP clock. The IP handles the DRP access by stretching
the AXI interface response until it is completed. If the DRP clock is much
slower than the AXI clock, this results in an unintentional timeout of the
value is not increased.

|Bit|Default Value|Access Type|Description|
|:-----:|:-----:|:-----:|-----|
|[0]|0|RW|Set when any bit in image completion vector=0|
|[1]|0|RW|AXIMM Write Error|
|[2]|0|RW|CmDQ Overflow|
|[29:3]|0|RW|Reserved|
|[31:30]|0|RW|Download Image Source|
