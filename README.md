fluent-plugin-twilio
=====================

## Overview
Fluentd Output plugin to make a call with twilio.

## Installation

install with gem or fluent-gem command as:

`````
### system installed gem
gem install fluent-plugin-twilio

### td-agent bundled gem
/usr/lib64/fluent/ruby/bin/fluent-gem install fluent-plugin-twilio
`````

## Configuration

### Message Format
`````
fluent_logger.post('notify.call', {
  :message  => 'Hello World!',   # Required
  :number   => '+8109012345678'  # Required
})
`````

### Sample
`````
<source>
  type http
  port 8888
</source>

<match notify.call>
  type twilio

  # Set account Sid and Token from twilio.com/user/account
  account_sid     TWILIO_ACCOUNT_SID           # Required
  auth_token      TWILIO_AUTH_TOKEN            # Required

  # Set caller ID with country code
  from_number     +81312345678                 # Required

  # Set defaults of making outbound call.
  # To call multiple phone at the same time, list them with comma like below.
  default_number  +819012345678,+818012345678  # Optional

  # Set log level to prevent info error for Fluentd v0.10.43 or later.
  log_level       warn
</match>
`````

### Quick Test
`````
# test call to +819012345678 and say "Help! System ABC has down." with woman voice.
$ curl http://localhost:8888/notify.call -F 'json={"number":"+819012345678","voice":"woman","message":"Help! System ABC has down."}'

# check twilio activity log
$ tail -f /var/log/td-agent/td-agent.log
`````

## Backend Service

* Twilio https://www.twilio.com/
* Twilio Japan http://twilio.kddi-web.com/

## Blog Articles

* http://y-ken.hatenablog.com/entry/fluent-plugin-twilio-has-released

## TODO
Pull requests are very welcome!!

## Copyright
Copyright © 2013- Kentaro Yoshida ([@yoshi_ken](https://twitter.com/yoshi_ken))

## License
Apache License, Version 2.0

