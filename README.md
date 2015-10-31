# Fedora 4 URI minter module

[![Build Status](https://travis-ci.org/fcrepo4-exts/fcrepo-mint.png?branch=master)](https://travis-ci.org/fcrepo4-exts/fcrepo-mint)

The `fcrepo-mint` module provides extension features to a [Fedora 4](https://github.com/fcrepo4/fcrepo4) repository. In particular,
it allows users to provide their own URI minting behavior. The default fedora4 minter creates hierarchical paths based on UUIDs,
but this module allows repository administrators to override that behavior. This implements a configurable hierarchical minter as well
as a connector to an external web service.

To use this module in the context of [fcrepo-webapp-plus](https://github.com/fcrepo4-exts/fcrepo-webapp-plus), an administrator would need
to update the Spring configuration to inject this implementation.

For example (in `./spring/rest.xml`):

    <!-- Mints PIDs-->
    <bean class="org.fcrepo.mint.UUIDPathMinter"
        c:length="${fcrepo.uuid.path.length:2}"
        c:count="${fcrepo.uuid.path.count:4}"/>

Alternately, to wire in an external minter available as a web service:

    <!-- Mints PIDs using external REST service
    <bean class="org.fcrepo.mint.HttpPidMinter"
        c:url="http://localhost/my/minter"
        c:method="POST"
        c:username="${fcrepo.minter.username:minterUser}"
        c:password="${fcrepo.minter.password:minterPass}"
        c:regex=""
        c:xpath="/response/ids/value"/>

## Building fcrepo-mint

The `fcrepo-mint` module requires Maven 3 and Java 8. To build the module, issue the command:

    mvn install

