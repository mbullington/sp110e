# Reverse Engineering SP110e LED Controller

Through Bluetooth sniffing, using this method I've been able to (semi reliably) control the SP110e controller via Homebridge.

You can find this controller for very cheap here: https://www.aliexpress.com/item/4000773623427.html?spm=a2g0o.productlist.0.0.4f09329cJ7C1H4&algo_pvid=542e757b-587f-4540-8652-2195883f1349&algo_expid=542e757b-587f-4540-8652-2195883f1349-0&btsid=0bb0622a16012309671478585ed4bd&ws_ab_test=searchweb0_0,searchweb201602_,searchweb201603_

This entire guide is for Bluetooth LE libraries, and uses hexidecimal.

## LE configuration

Service ID can be found with `ffe0`. Under this is two characteristics, `ffe1` and `ffe2`.

**Important:**

Upon connection, you immediately need to write data in this order to prevent the connection from closing.

I'm not honestly sure why.

`ffe2`: `01 00`
`ffe1`: `01 b7 e3 d5`

## Controlling after Connected

All of these commands should be written to the `ffe1` characteristics.

`VV`, `RR`, `GG`, and `BB` in this case are hex strings between 0-255.

**Turn on:**

`fa 0e c7 aa`

**Turn off**:

`b0 4f c2 ab`

**Change color**:

`RR GG BB 1e`

**Control brightness:**

`VV ed 29 2a`

**Change to preset:**:

`VV 09 fa 2c`

**Change speed of preset:**:

`VV 10 34 03`

