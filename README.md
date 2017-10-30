# Apollo

Apollo is a Vagrant box built around WordPress Development.

This being said, Apollo is designed to quickly and effortlessly run any PHP / HTML application locally.

## Installation

The latest installation guide can be found here: [Apollo Installation Guide](https://github.com/jamesmorrison/apollo/wiki/Installation)

If you are experienced with vagrant, all you need from this repo is the VagrantFile, and the .config directory.

## Usage
Once the installation is complete, you'll see a sites folder has been created in the Apollo directory.

To create a site, add a new folder here using the full domain, including the top level domain. For Example 'site.dev'.

Any files in this directory will be available from http://site.dev. The application will automatically execute PHP applications you access through the URL. All other assets will be provided raw to the browser.

Note: You must configure your hosts file to point site.dev to 10.10.10.10 so that the request successfully reaches Apollo. Documentation for this can be found here: [Windows](https://support.rackspace.com/how-to/modify-your-hosts-file/) [Unix](https://www.weg.ucar.edu/documentation/hostfile-unix.html)

Alternatively you can setup Dnsmasq to automatically route all requests to a certain TLD to Apollo: [Dnsmasq](http://www.thekelleys.org.uk/dnsmasq/docs/setup.html)

## Other Notes

### HTTPS
Apollo has full support for HTTPS, however the certificate is not signed by a valid root certificate. This means that all sites you host locally will show as a security exception in your browser. Simply accepting this security exception will allow you to use https with your local sites with no issues.

### Multiple TDL's
Apollo supports all single level TLD's out the box, as long as the DNS resolves to the Vagrant box.
Only the .co.uk multi-level TLD is supported out the box, however others can be added upon request (raise an issue here: [https://github.com/jamesmorrison/apollo/issues](Issues))

## Advanced Notes

### Multiple local instances of Apollo
As Apollo can support any TLD, its easy to have multiple Apollo instances on your system simultaneously. If you wish to have two instances up at the same time, simply change the IP in the VagrantFile. As long as the correct domain resolves to the correct IP, the Apollo instances will work seamlessly together.
