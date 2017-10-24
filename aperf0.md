This register enables the AXI4-Lite timeout. This ensures that transactions to the
transceiver registers do not lock the AXI4-Lite bus which can happen if the
transceiver is in reset or not being clocked when an access is attempted for
example.

|Bit|Default Value|Access Type|Description|
|:-----:|:-----:|:-----:|-----|
|[0]|0|RW|Set when any bit in image completion vector=0|
|[1]|0|RW|AXIMM Write Error|
|[2]|0|RW|CmDQ Overflow|
|[29:3]|0|RW|Reserved|
|[31:30]|0|RW|Download Image Source|
