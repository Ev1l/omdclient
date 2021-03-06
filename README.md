# omdclient

omdclient provides a suite of tools to interact with the APIs associated
with the `check_mk`/Open Monitoring Distribution tool suite

## WATO APIs

WATO is used to create, remove, and modify entries within the OMD user
suite.  This is documented at:

http://mathias-kettner.com/checkmk_wato_webapi.html

### omd-host-crud

Creates/Reads/Updates/Deletes entries from an existing monitoring
interface.

### omd-activate

Activates changes made by the API user.

### omd-puppet-enc

Provides a linkage between a puppet External Node Classifier (ENC) and a
monitoring instance.  In essence, we want to add hosts to monitoring when
a host is added to puppet; remove the host from monitoring when the host
is removed from puppet; and re-tag the host when its role changes.  

https://docs.puppetlabs.com/guides/external_nodes.html

## Multisite/Nagios

https://mathias-kettner.de/checkmk_multisite_automation.html

### omd-nagios-ack

Acknowledges host/service alerts from the command-line.

### omd-nagios-downtime

Schedules host/service downtimes from the command-line.

### omd-nagios-report

Prints a human-readable report on current host and service alerts. 

## How To Use

### /etc/omdclient/config.yaml

You'll have to populate this file on your own:

    server: 'xxxxxx.example'
    site: 'xxxxxx'
    user: 'xxxx-api'
    apikey: 'xxxxxx'


### Configuration of 'expanded views'

The report scripts depend on 'expanded view' versions of the
`hostproblems` and `svcproblems` views, which add comments.  In order to
add these, you generally have to:

1.  Edit view `hostproblems` - it's a default view, so you'll go to 'clone'.
    * Change the name from `hostproblems` to `hostproblems_expanded`.
    * Scroll down to the list of columns, and add one more: `Host Comments`.
    * Save.
2.  Edit the view `svcproblems` and created `svcproblems_expanded`, same 
    as above but with the column `Service Comments`.

(Thanks to Christian Bryn - https://github.com/epleterte - for the docs!)
