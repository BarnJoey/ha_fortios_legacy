# FortiOS Device Tracker component for Home Assistant
this is a custom component for Home Assistant that adds compatability for older Fortinet devices.

the offical FortiOS Device Tracker doesn't support devices running FortiOS under then 6.4.3, this does
it should support all the way from 5.6 but I've only tested it on 6.0

along with compatibility with older devices it also adds the ability to recognize FortiOS tags as either blacklist or whitelist terms

here's an example configuration:
```yaml
device_tracker:
  - platform: fortios_legacy
    host: <hostname / ip+port of fortinet device>
    token: <api token here>
    verify_ssl: false (default)
    max_last_seen: 60 (default)
    whitelist: "NULL" (default)
    blacklist: "NULL" (default)
```

Host, Token and Verify SSL work exactly like the offical component, you can view the doc here: https://www.home-assistant.io/integrations/fortios/

```yaml
max_last_seen: 60
```
this controls the maximum amount of seconds that can elapsed between when your fortinet device last saw a device before it considers the device away

```yaml
whitelist: "ha_tracking"
```
put in the name of a tag exactly how it appears in FortiOS to have home assistant recognize it as a whitelist term. avoid using spaces

```yaml
blacklist: "ha_tracking_exclude"
```
exactly like the whitelist but will prevent devices from being recognized by home assistant

the blacklist / whitelist are totally optional, you can use neither and track all devices or use one or both. the blacklist will supercede the whitelist
