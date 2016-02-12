# heroku-buildpack-apt

Add support for apt-based dependencies during both compile and runtime.
## Usage

This buildpack works best with [heroku-buildpack-multi](https://github.com/ddollar/heroku-buildpack-multi) so that it can be used with your app's existing buildpacks.

Include a list of apt package names to be installed in a file named `Aptfile`

By default packages are downloaded from internet on every build. To speed things up, switch on caching:

    heroku config:set APT_CACHING=yes

If Aptfile has not changed since last build, and packages are installed from package cache. If Aptfile has changed, or `APT_CACHING=no`, cache will be cleared and packages will be re-downloaded.

If you want to install packages from a non-standard repository, set its URL in the APT_SOURCE heroku variable like in a `/etc/apt.list.d/custom.repo` file:

    deb http://dl.google.com/linux/chrome/deb/ stable main

Several repositories can be listed separated by comma.

You can disable Apt forcibly even if `Aptfile` is present by setting heroku varable `APT_ENABLED=no`.

## Example

#### .buildpacks

    https://github.com/ivandeex/heroku-buildpack-apt
    https://github.com/heroku/heroku-buildpack-python

#### Aptfile

    xvfb
    fluxbox
    x11-xkb-utils
    xfonts-100dpi
    http://downloads.sourceforge.net/project/wkhtmltopdf/0.12.1/wkhtmltox-0.12.1_linux-precise-amd64.deb

### Example output

	Fetching buildpack... done
	Detecting buildpack... done, Multipack
	Fetching cache... done
	Compiling app...
	=====> Downloading Buildpack: https://github.com/ddollar/heroku-buildpack-apt
	=====> Detected Framework: Apt
	  Updating apt caches
	  ...
	  Installing libpq-dev_8.4.17-0ubuntu10.04_amd64.deb
	  Installing libpq5_8.4.17-0ubuntu10.04_amd64.deb
	  Writing profile script
	=====> Downloading Buildpack: https://github.com/heroku/heroku-buildpack-ruby
    ...
	
## License

MIT
