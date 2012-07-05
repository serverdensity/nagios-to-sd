Nagios to ServerDensity.com Plugin
==============================

`nagios-to-sd` is a plugin, for the Nagios family of server monitoring and metrics collection tools, to send metrics data to the Server Density server monitoring service.

Why?
----

There are millions of Nagios (et al) installations around the world monitoring sysops' systems, and we thought it might be nice if you could take advantage of the SaaS monitoring provided by SD by just installing an extra plugin in those systems, rather than configuring and deploying our software agent.

How?
----

The plugin is a small Python script that, once installed on your Nagios node(s) and configured to run after all other plugins and checks, will attempt to find equivalent metrics to those we monitor (by default there are only 5, but hopefully this can be expanded in future, especially with more support for non-default plugins) and then sends that as a postback to the SD API.

Python dependencies
-------------------

 * py-serverdensity
 * NagParser

Installation
------------

Just copy `push_to_sd` to your plugins dir, and copy `push_to_sd.conf.example` as `push_to_sd.conf` either in the same dir, or somewhere else on the file system you can reference it.

You'll need Python installed on the machine, which comes by default on most distributions.
To install python dependencies you can use::

    sudo pip install -r requirements.txt

If you don't have `pip` installed you can `easy_install` each requirement manually (see the `requirements.txt` file or the requirements section above)

Edit the push_to_sd.conf file with your ServerDensity.com API credentials and agent key (see http://developer.serverdensity.com/docs/read/Authentication), as well as any other configuration values:

``[nagios]``

*error-return-code*
  A Nagios plugin return code (ok, warning, critical, or unknown) to return if the return-on-error setting is true (1).

*return-on-error*
  If the plugin encounters an error, e.g. an an error posting to the SD API, then return (with error-return-code) instead of continuing. Does not effect the error being logged


``[serverdensity]``

*agents*
  Newline seperated list of agent configs, these should be the hostnames that Nagios knows about.