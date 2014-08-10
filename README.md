## Heroku buildpack: Erlang

This is a Heroku buildpack for Erlang apps. It uses [Rebar](https://github.com/basho/rebar).


### Configure your Heroku App

    $ heroku config:add BUILDPACK_URL="https://github.com/zatonovo/heroku-buildpack-erlang.git" -a YOUR_APP

or
    $ heroku create --buildpack "https://github.com/zatonovo/heroku-buildpack-erlang.git"

Note that only the cedar-14 stack is supported. Check your stack with `heroku stack`. If you need to change your stack, use the `heroku stack:set cedar-14` command. [1]

### Select an Erlang version

The Erlang/OTP release version that will be used to build and run your application is now sourced from a dotfile called `.preferred_otp_version`. It needs to be the branch or tag name from the http://github.com/erlang/otp repository, and further, needs to be one of the versions that precompiled binaries are available for.

Currently supported OTP versions:

* master (17.0)
* 17.0

To select the version for your app:

    $ echo 17.0 > .preferred_otp_version
    $ git commit -m "Select 17.0 as preferred OTP version" .preferred_otp_version

Note that the run-time can be cached. If you wish to clear the cache, `touch .no_cache` in the base of your project directory.

### Build your Heroku App

    $ git push heroku master

You may need to write a new commit and push if your code was already up to date.

### ERTS Notes
```
./configure
make
make RELEASE_ROOT=~/17.0/otp -ik release
```

## References
[1] https://devcenter.heroku.com/articles/stack
