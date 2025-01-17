# FAQ

## I've installed Batpred but I don't see the correct entities

- First look at AppDaemon.log (can be found in the list of log files in the System/Log area of the GUI). See if any errors are warnings are found. If you see an error it's likely something is configured wrongly, check your entity settings are correct.
- Make sure Solcast is installed and it's auto-updated at least a couple of times a day (see the Solcast instructions). The default solcast sensor names maybe wrong, you might need to update the apps.yml config to match your own names (some people don't have the solcast_ bit in their names)

## Why is my predicted charge % higher or lower than I might expect?

- Batpred is based on costing, so it will try to save you money. If you have the PV 10% option enabled it will also take into account the more worse case scenario and how often it might happen, so if the forecast is a bit unreliable it's better to charge more and not risk getting stung importing.
- Have you checked your energy rates for import and export are correct, maybe check the rates graph and confirm. If you do something like have export>import then Batpred will try to export as much as possible.
- Have you tuned Solcast to match your output accurately?
- Have you tuned the **metric_min_improvement**, **best_soc_min** and **best_soc_keep settings**?
- Do you have predicted car charging during the time period?
- You can also tune **load_scaling** and **pv_scaling** to adjust predictions up and down a bit
- Maybe your historical data includes car charging, you might want to filter this out using car_charging_hold (see below)

## Why didn't the slot actually get configured?

- make sure **set_charge_window** and **set_soc_enable** is turned on

## The charge limit keeps increasing/decreasing in the charge window or is unstable

- Check you don't have any other automations running that adjust GivTCP settings during this time. Some people had a script that changes the reserve %, this will cause problems - please disable other automations and retry.

## I changed a config item but it made no difference?

- If **user_config_enable** is True then many config items are now inside Home Assistant, in which case change it there instead.

## It's all running but I'm not getting very good results

- You might want to tune **best_soc_keep** to set a minimum target battery level, e.g. I use 2.0 (for 2kWh, which is just over 20% on a 9.5kWh battery)
- Have a read of the user configuration guide above depending on your tariff different settings maybe required
- Check your solar production is well calibrated (you can compare solcast vs actually in home assistant energy tab or on the GivEnergy portal)
- Make sure your inverter max AC rate has been set correctly
- If you have an EV that you charge then you will want some sort of car charging sensor or use the basic car charging hold feature or your load predictions maybe unreliable
- Do you have a solar diverter? If so maybe you want to try using the IBoost model settings.
- Perhaps set up the calibration chart and let it run for 24 hours to see how things line up
- If your export slots are too small compared to expected check your inverter_limit is set correctly (see below)

If you are still having trouble feel free to raise a ticket for support to post on the [GivTCP Facebook group](https://www.facebook.com/groups/615579009972782).
