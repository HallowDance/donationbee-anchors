# donationbee-anchors

Hourly anchors for the [DonationBee](https://bee.theorycorner.com) ledger. Each anchor is a
checkpoint the ledger signed (with witness cosignatures), plus an
[OpenTimestamps](https://opentimestamps.org) proof that ties it to the Bitcoin blockchain.

```
anchors/YYYY/MM/DD/<size>.checkpoint       the signed checkpoint, byte for byte
anchors/YYYY/MM/DD/<size>.checkpoint.ots   its timestamp proof (pending at first, complete
                                           after a few hours, once Bitcoin confirms it)
```

Files are only ever added. The only later change is a pending `.ots` proof being replaced by its
completed version. The `main` branch blocks force-pushes and deletion, for admins too.

## Why this exists

If the DonationBee server ever rewrote history, its new checkpoints wouldn't match the ones
already published here. The Bitcoin timestamps prove each one existed at that time.

## Check it yourself

```sh
pip install donationbee-verify opentimestamps-client
vpp-verify --url https://bee.theorycorner.com \
  --anchors-repo https://github.com/HallowDance/donationbee-anchors --check-ots
```

The format is in the ledger spec,
[§13 Anchors](https://github.com/HallowDance/donationbee/blob/master/docs/LEDGER_SPEC.md).
