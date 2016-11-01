# Service script for debianoids

Look at [LSB init scripts](http://wiki.debian.org/LSBInitScripts) for more information.

Original script taken from from [naholyr's gist](https://gist.github.com/naholyr/4275302)

## Usage

Copy to `/etc/init.d`:

```sh
# replace "$YOUR_SERVICE_NAME" with your service's name (whenever it's not enough obvious)
cp "service.sh" "/etc/init.d/$YOUR_SERVICE_NAME"
chmod +x /etc/init.d/$YOUR_SERVICE_NAME
```

Edit the script and replace following tokens:

* `<NAME>` = `$YOUR_SERVICE_NAME`
* `<DESCRIPTION>` = Describe your service here (be concise)
* Feel free to modify the LSB header, I've made default choices you may not agree with
* `<COMMAND>` = Command to start your server (for example `/home/myuser/.dropbox-dist/dropboxd`)
* `<USER>` = Login of the system user the script should be run as (for example `myuser`)

Start and test your service:

```sh
service $YOUR_SERVICE_NAME start
service $YOUR_SERVICE_NAME stop
```

Install service to be run at boot-time:

```sh
update-rc.d $YOUR_SERVICE_NAME defaults
```
For rpm based distributions such as CentOS or Red Hat, you can use

```sh
chkconfig $YOUR_SERVICE_NAME --add
```
If you want to see which runlevel your script will run in

```sh
chkconfig $YOUR_SERVICE_NAME --list
```

## Uninstall

The service can uninstall itself with `service $NAME uninstall`. 

That's all? Yeah boy, as easy as it sounds, but easy, my little "Pulpin", is also dangerous. This is an auto-generated script, so you can bring it back very easily, but do not test it in a production server. I tested to install/uninstall services in various normal environments. However, that does not guarantee that it will work perfect on yours.

Don't want it? Remove lines 56-58 of the service's script.

## Logs?

Your service will log its output to `/var/log/$NAME.log`. Don't forget to setup a log-rotate :)

## I'm noob and/or lazy

Yep, I'm lazy too. But still, I've tried to write a script to automate this :)

```sh
wget 'https://raw.github.com/gist/4275302/new-service.sh' && bash new-service.sh
```

This script will download a `service.sh` file into a temporal file `tempfile`. After that, will replace some parameters and will ask you to run some commands as superuser.

If you feel confident enough with my script, you can `sudo` the script directly:

```sh
wget 'https://raw.github.com/gist/4275302/new-service.sh' && sudo bash new-service.sh
```

Note: the cool hipsterish `curl $URL | bash` won't work here, I don't really want to check why.

### Demo

Creating the service:

![service-create](http://dl.dropbox.com/u/6414656/gist-4275302/service-create.png)

Looking at service files (logs, pid):

![service-files](http://dl.dropbox.com/u/6414656/gist-4275302/service-files.png)

Uninstalling service:

![service-uninstall](http://dl.dropbox.com/u/6414656/gist-4275302/service-uninstall.png)

Note: You can achieve the same thing that this project tries to achieve by using the [MetaInit](https://wiki.debian.org/MetaInit) package in Debian.
