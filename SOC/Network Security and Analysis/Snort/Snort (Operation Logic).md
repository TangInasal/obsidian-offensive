
- Packet Decoder - It collects and prepares the packets for pre-processing. 
- Pre-processors - A component that arranges and modifies the packets for the detection engine.
- Detection Engine - The primary component that process, dissect and analyse the packets by applying the rules. 
- Logging and Alerting - Log and alert generation component.
- Outputs and Plugins - Output integration modules (i.e. alerts to syslog/mysql) and additional plugin (rule management detection plugins) support is done with this component.

- snort.conf: Main configuration file.
- local.rules: User-generated rules file.

