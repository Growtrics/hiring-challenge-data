# Kestrel Labs testing pipeline: how it works today

Synthetic. Written for this take-home.

## Diagram

```
 customer uploads app build
            |
            v
 +---------------------+      +------------------------------+
 | Scheduler           | ---> | Explorer agent               |
 | one run per build   |      | AI model + one farm device   |
 +---------------------+      | taps, types, reads screens   |
                              +------------------------------+
                                  |  on any step failure:
                                  |  restart the app and replay
                                  |  the run from the start
                                  |  (up to 3 retries)
                                  v
                              +------------------------------+
                              | Bug reporter agent           |
                              | AI model                     |
                              | 1. drafts each report        |
                              | 2. scores its own report     |
                              |    from 0 to 1               |
                              | 3. sends it if score >= 0.6  |
                              +------------------------------+
                                  |
                                  v
                              +------------------------------+
                              | Customer portal              |
                              | customer marks each report   |
                              | accepted or rejected         |
                              +------------------------------+
```

## Details

- **Scheduler:** starts one run for every app build a customer uploads.
- **Explorer agent:** an AI model drives one device from the device farm. It explores the app, records screens, logs and video, and passes what it saw to the bug reporter.
- **Device farm:** rented from an outside vendor at $0.12 per device minute.
- **Retries:** when a step fails, for example a timeout, an element that cannot be found or a device that disconnects, the explorer restarts the app and replays the whole run from the beginning. It does this up to three times.
- **Bug reporter agent:** an AI model drafts a report for each suspected bug. The same model then gives its own report a score from 0 to 1, and sends every report scoring 0.6 or higher to the customer. No other step reviews a report before the customer sees it.
- **Customer portal:** customers mark each report as accepted, a real bug, or rejected, not a real bug. The acceptance count in the cost log comes from here.
- **Models:** the explorer and the reporter use the same commercial AI model. A cheaper model from the same provider costs about half as much per call.
- **Monitoring:** the team sees run counts and total monthly spend on a dashboard. Spend is not broken down by stage.
- **Where `cost_log.csv` comes from:** it was assembled by hand from vendor invoices and model bills for this review. The live dashboard shows only total spend.
