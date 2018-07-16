# Based on quadportnick/cups-airprint and andrewmichael/docker-cups-airprint

Simply added Xerox WorkCentre 6515 and 3335 PPDs. Deleted airprint features.

 https://github.com/quadportnick/docker-cups-airprint
 https://github.com/andrewmichael/docker-cups-airprint

This Ubuntu-based Docker image runs a CUPS instance.

## Prereqs
* No other printers should be shared under Control Panel>External Devices>Printer so that the DSM's CUPS is not running. 
* `Enable Bonjour service discovery` needs to be marked under Control Panel>Network>DSM Settings 

## Configuration

### Volumes:
* `/config`: where the persistent printer configs will be stored
* `/services`: where the Avahi service files will be generated

### Variables:
* `CUPSADMIN`: the CUPS admin user you want created
* `CUPSPASSWORD`: the password for the CUPS admin user

### Ports:
* `631`: the TCP port for CUPS must be exposed

## Using
CUPS will be configurable at http://[diskstation]:631 using the CUPSADMIN/CUPSPASSWORD when you do something administrative.

If the `/services` volume isn't mapping to `/etc/avahi/services` then you will have to manually copy the .service files to that path at the command line.

## Notes
* CUPS doesn't write out `printers.conf` immediately when making changes even though they're live in CUPS. Therefore it will take a few moments before the services files update
* Don't stop the container immediately if you intend to have a persistent configuration for this same reason
 
