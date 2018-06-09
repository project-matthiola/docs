# WebSocket `/broadcaster`

## Order Book

```json
{
    "type": "order_book",
    "mode": "snapshot",
    "futures_id": "GC_SEP18",
    "data": {
        "bids": [
            ["49.99","133.95"]
        ],
        "asks":[
            ["50.01","25.77"]
        ]
    }
}
```

Traders would get snapshots of order books after order books had been changed. `bids` and `asks` are arrays of `[price, size]` tuples and represent the entire order book.

## Trade

### Snapshot

```json
{
    "type": "trade",
    "mode": "snapshot",
    "futures_id": "GC_SEP18",
    "data": [
        {
            "price": "50.01",
            "quantity": "7.35",
            "time": "2018-06-08 20:47:37 +0800 CST"
        }
    ]
}
```

When subscribing to the channel, it will first send a message with the type `trade`, mode `snapshot` and the corresponding `futures_id` and `data` array with data of trades.

### Update

```json
{
    "type": "trade",
    "mode": "snapshot",
    "futures_id": "GC_SEP18",
    "data": {
        "price": "50.01",
        "quantity": "7.35",
        "time": "2018-06-08 20:47:37 +0800 CST"
    }
}
```

Subsequent updates will have the mode `update`, with the corresponding data of the single trade updated.
