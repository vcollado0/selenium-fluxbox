### Info

The 'bleeding edge' versions of the drivers do not always work well together, e.g. through errors like:
`org.openqa.selenium.WebDriverException: unknown error: Chrome version must be >= 52.0.2743.0 ...`
Likewise the Selenium hub error
![box](https://github.com/sergueik/selenium-fluxbox/blob/master/screenshots/session_error.png)
indicates a likely versions mismatch between Selenium, Geckodriver and Firefox, or Selenium, ChromeDriver and Chrome.

Unfortunately this is especially true with release __3.0.x__  of Selenium.
One often like to enforce specific past versions of browser-based Selenium testing software stack to be used. 
Vagrant makes this easy.
This project offers a standalone Ubuntu Trusty __14.04__ vagrant box instance containing

 * Fluxbox
 * [Tmux]](https://github.com/tmux/tmux) autologin
 * Stable release of Selenium Server __2.53__
 * Chrome and Chrome Driver
 * Firefox with optional Gecko Driver

The `Vagrantfile` is based on [Anomen/vagrant-selenium](https://github.com/Anomen/vagrant-selenium/blob/master/script.sh)

![box](https://github.com/sergueik/selenium-fluxbox/blob/master/screenshots/box.png)

### Usage

Download the box image [trusty-server-amd64-vagrant-selenium.box](https://atlas.hashicorp.com/ubuntu/boxes/trusty64) locally, name it `trusty-server-amd64-vagrant-selenium.box` and place in the `~/Downloads` or `$env:USERPROFILE\Downloads`.
Then run
```bash
export PROVISION_SELENIUM=true
vagrant up
```
Specific versions of Selenium Server, Firefox, Gecko Driver, Chrome, Chrome Driver can be set through the environment variables
`SELENIUM_VERSION`, `FIREFOX_VERSION`, `GECKODRIVER_VERSION`, `CHROME_VERSION`, `CHROMEDRIVER_VERSION`.


Few supported  combination of old versions are listed below:

|                      |              |
|----------------------|--------------|
| SELENIUM_VERSION     | 2.53         |
| FIREFOX_VERSION      | 45.0.1       |
| CHROME_VERSION       | 54.0.2840.71 |
| CHROMEDRIVER_VERSION | 2.24         |

|                      |              |
|----------------------|--------------|
| SELENIUM_VERSION     | 2.47         |
| FIREFOX_VERSION      | 40.0.3       |
| CHROME_VERSION       | 50.0.2661.75 |
| CHROMEDRIVER_VERSION | 2.16         |


For Chrome, the `CHROME_VERSION` can also set to `stable`, `unstable` or `beta` - forcing the `.deb` package of selected build of Chrome browser to be installed from the
[google repository](https://www.google.com/linuxrepositories/).

A handful of old Chrome build debian packages the box can download from [http://www.slimjetbrowser.com](http://www.slimjetbrowser.com/chrome/lnx/) - check if desired version is available. There is also a relatively recent 32-bit package on this site.
Note:  the error`Unsupported major.minor version 52.0` is a Java version mismatch, and you have to switch to JDK 8 by setting the `USE_ORACLE_JAVA` environment to `true`.

### Limitations
  * The hub is available on `http://127.0.0.1:4444/wd/hub/static/resource/hub.html` with some delay after the Virtual Box reboot - currently there is no visual cue on when the box is ready.

  * If the screen resolution is too low, run on the host
```bash
vboxmanage controlvm "Selenium Fluxbox" setvideomodehint 1280 900 32
```

### Work in Progress
 * Probe [http://dl.google.com/linux/chrome/deb/pool/main/g/google-chrome-stable/](http://dl.google.com/linux/chrome/deb/pool/main/g/google-chrome-stable/) and /or [https://google-chrome.en.uptodown.com/ubuntu/old](https://google-chrome.en.uptodown.com/ubuntu/old) for a valid past Chrome build is a
 * Enable [gecko driver](https://developer.mozilla.org/en-US/docs/Mozilla/QA/Marionette/WebDriver)
 * Dockerfile - see e.g. [docker](https://github.com/elgalu/docker-selenium), [docker-selenium-firefox-chrome-beta](https://github.com/vvo/docker-selenium-firefox-chrome-beta)
 * Upgrade Vagrantfile to [xenial Selenium](https://atlas.hashicorp.com/Th33x1l3/boxes/vagrant-selenium/versions/0.2.1/providers/virtualbox.box) Virtulbox image
 * Switch to [daily xenial](https://cloud-images.ubuntu.com/xenial/current/xenial-server-cloudimg-amd64-vagrant.box) virtualbox image.
 * Find alternative location for downlevel chrome browser download, the `http://www.slimjetbrowser.com` is no longer available.

### Author
[Serguei Kouzmine](kouzmine_serguei@yahoo.com)
