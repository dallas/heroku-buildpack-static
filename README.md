Heroku/dokku buildpack: Static
============================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpack)—which can also be used with dokku—which serves static files using node.js, express or nginx.

This buildpack has been modified from the original for use with Docker containers that have a `www-data` user instead of a `www` user. It also has stricter policies on denying access to certain files and directories—including blocking access to the `/conf` directory entirely and to the `_static.cfg` file. It also opts to serve up 404 errors for blocked files/directories rather than 403 errors.

Usage
-----

Example usage:

    $ ls -R *
    _static.cfg                img.png                    text.txt
    ...

    $ heroku create --stack cedar --buildpack https://github.com/abhishekmunie/heroku-buildpack-static.git
    ...

    $ git push heroku master
    ...
    -----> Heroku receiving push
    -----> Fetching custom buildpack... cloning with git...done
    -----> Static app detected
    -----> Creating default 404 page... done
    ...
    -----> Discovering process types
    ...

The buildpack will detect your app as Static if it has the file `_static.cfg` in the `root`.
For nginx, you can set custom nginx config as described for [heroku-buildpack-nginx](https://github.com/abhishekmunie/heroku-buildpack-nginx).

Configuring Buildpack
---------------------

Buildpack reads its configuration from `_static.cfg`

    SERVER_TYPE="node" or "express" or "nginx"
    BUILD_WEB_ASSETS="true"

Hacking
-------

To modify this buildpack, fork it on Github. Push up changes to your fork, then
create a test app with `--buildpack <your-github-url>` and push to it.

For Nginx Serve, buildpack simply creating default nginx configuration for static site
and uses [heroku-buildpack-nginx](https://github.com/abhishekmunie/heroku-buildpack-nginx) to create nginx server.
