# FIX

The [FIX](https://en.wikipedia.org/wiki/Financial_Information_eXchange), or Financial Information eXchange protocol is an electronic communications protocol initiated in 1992 for international real-time exchange of information related to the securities transactions and markets.

## Messages

### Header

Reference: [https://legacy.fixspec.com//FIX/5.0-SP2/Standard-Header](https://legacy.fixspec.com//FIX/5.0-SP2/Standard-Header)

| Tag | Name | Type | Description |
| :-- | :--- | :--- | :---------- |
| 8 | BeginString | String | Must be `FIXT.1.1`. |
| 9 | BodyLength | Length | Message length, in bytes, forward to the CheckSum field. |
| 35 | MsgType | String | Defines message type. |
| 49 | SenderCompID | String | The ID of the sender. |
| 56 | TargetCompID | String | The ID of the target. |
| 34 | MsgSeqNum | SeqNum | Integer message sequence number. |
| 52 | SendingTime | UTCTimestamp | Time of message transmission. |
| 50 | SenderSubID | String | The name of the trader. |
| 1128 | ApplVerID | Char | Must be `9`. |

### Trailer

Reference: [https://legacy.fixspec.com/FIX/5.0-SP2/Standard-Trailer](https://legacy.fixspec.com/FIX/5.0-SP2/Standard-Trailer)

| Tag | Name | Type | Description |
| :-- | :--- | :--- | :---------- |
| 10 | CheckSum | String | Checksum. |

### New Order Single (MsgType = `D`)

Sent by the client to enter an order.

Reference: [https://legacy.fixspec.com/FIX/5.0-SP2/New-Order-Single](https://legacy.fixspec.com/FIX/5.0-SP2/New-Order-Single)

| Tag | Name | Type | Description |
| :-- | :--- | :--- | :---------- |
| 11 | ClOrdID | UUID | Unique identifier of the order as assigned by institution or by the intermediary with closest association with the investor. |
| 40 | OrdType | Char | Order type. |
| 54 | Side | Char | Must be **1** to buy or **2** to sell. |
| 55 | Symbol | String | Representation of the futures. E.g. `CG_SEP18` |
| 38 | OrderQty | Qty | Quantity of the futures. |
| 44 | Price | Price | Required for **limit** and **stop limit** OrdTypes. |
| 99 | StopPx | Price | Required for **stop market** and **stop limit** OrdTypes. |
| 60 | TransactTime | UTCTimestamp | Time this order request was initiated/released by the trader, trading system, or intermediary. |

### Order Cancel Request (MsgType = `F`)

The order cancel request message requests the cancellation of all of the remaining quantity of an existing order. Note that the Order Cancel/Replace Request should be used to partially cancel (reduce) an order).

Reference: [https://legacy.fixspec.com/FIX/5.0-SP2/Order-Cancel-Request](https://legacy.fixspec.com/FIX/5.0-SP2/Order-Cancel-Request)

| Tag | Name | Type | Description |
| :-- | :--- | :--- | :---------- |
| 11 | ClOrdID | UUID | Unique ID of cancel request as assigned by the institution. |
| 37 | OrderID | UUID | OrderID of the order to be canceled. |
| 55 | Symbol | String | Symbol of the order to cancel. |

## Mapping

### OrdType

| Value | Meaning |
| :---- | :------ |
| 1 | MARKET |
| 2 | LIMIT |
| 3 | STOP MARKET |
| 4 | STOP LIMIT |

### Side

| Value | Meaning |
| :---- | :------ |
| 1 | BUY |
| 2 | SELL |

### OrdStatus

| Value | Meaning |
| :---- | :------ |
| 0 | NEW |
| 1 | PARTIALLY_FILLED |
| 2 | FILLED |
| 3 | CANCELED |
| 8 | REJECTED |
| A | PENDING_NEW |
