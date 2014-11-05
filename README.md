Heroku/dokku buildpack: Static
============================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpack)—which can also be used with dokku—which serves static files using node.js, express or nginx.

This buildpack has been modified from the original for use with Docker containers that have a `www-data` user instead of a `www` user. It also has stricter policies on denying access to certain files and directories—including blocking access to the `/conf` directory entirely and to the `_static.cfg` file. It also opts to serve up 404 errors for blocked files/directories rather than 403 errors.

Usage
-----

Example usage:

    $ echo 'BUILDPACK_URL="https://github.com/dallas/heroku-buildpack-static.git"' > .env
    $ echo 'SERVER_TYPE="nginx"' > _static.cfg
    $ git origin add production dokku@<your-domain>:<app-name>
    $ git push production master

The buildpack will detect your app as Static if it has the file `_static.cfg` in the `root`.
For nginx, you can set custom nginx config as described for [heroku-buildpack-nginx](https://github.com/abhishekmunie/heroku-buildpack-nginx).

Configuring Buildpack
---------------------

Buildpack reads its configuration from `_static.cfg`

    SERVER_TYPE="[node|express|nginx]"
    BUILD_WEB_ASSETS="[true|false]"

Hacking
-------

To modify this buildpack, fork it on Github. Push up changes to your fork, then
create a test app with `--buildpack <your-github-url>` and push to it.

For Nginx Serve, buildpack simply creating default nginx configuration for static site
and uses [heroku-buildpack-nginx](https://github.com/abhishekmunie/heroku-buildpack-nginx) to create nginx server.
