# Running Nginx Under a Non-Root User

Sometimes, rarely, you will find yourself needing to run Nginx as a non-root
user without sudo permissions. Figuring out the various settings needed to do
this from scratch can be an annoying process: by default Nginx assumes it has
write access to all sorts of restricted places in a UNIX filesystem, and each
of those is controlled by a different configuration option.

To run this example, first set up the Vagrant VM. This will install Nginx and
create an `nginx` user with write access to the default `/vagrant` synced
folder:

```
vagrant up
```

Now log in as the default `vagrant` user:

```
vagrant ssh
```

Once logged in switch to the `nginx` user and launch Nginx:

```
sudo su
su - nginx
/usr/sbin/nginx -c /vagrant/nginx.conf
```

You can satisfy yourself that Nginx is running just fine on port 8080 even
though the `nginx` user doesn't have write access to `/var/run`, `/var/log`, and
other restricted locations.

To stop Nginx:

```
/usr/sbin/nginx -s stop -c /vagrant/nginx.conf
```

The various settings needed for this to work are documented in `nginx.conf`, and
are easy enough to alter for other use cases.
