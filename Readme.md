Thumbor Heroku
==============

Introduction
------------

This project is a Heroku configuration in order to use Thumbor on Heroku. It is configured for very specific needs,
which include the availability of the `smart` mode (and thus OpenCV), you should fork it in order for it to match your
needs.


Configuration
-------------

### Detectors

In order for the smart mode to be useful, the `DETECTORS` are set. This requires OpenCV to be available to Python.

### Storages

In the configuration, picture files come from a S3 file storage, wich are as easy to reach that any Heroku addon, so
there is no need for a file storage.

The generated output are supposedly kept by a reverse proxy put in front of the Thumbor.

However, what can be CPU-heavy is the run of detectors. In this regard, the output of detectors is kept in cache. Here
we use a *RedisToGo* Heroku addon, which can be interchanged with any other one. Memcache addons are however not usable,
since they require authentication, which is not supported by Thumbor's storages.

### Security Key

The `unsafe` mode is forbidden, and you need to set a security key. You can do this by setting the
`THUMBOR_SECURITY_KEY` Heroku environment variable.


Deployment
----------

This project comes along with the [jetpack](https://github.com/ActivKonnect/jetpack) buildpack. The `jetpack.sh`
configuration file is quite straightforward.

It uses a pre-pack which embeds Python and OpenCV, which are the two dependencies required for Thumbor to run correctly.


License
-------

This chunk of configuration is available under the terms of the WTFPL. See the attached COPYING file.
