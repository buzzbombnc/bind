bind
====

Ansible role to install bind DNS server/utilities and DNS keys on Slackware Linux.

DNS Keys
--------

DNS keys are typically needed on more than one server.  As such, variables are applied in a group that ends with 
"_dnskey".

The format of `X_dnskey` is a dictionary with two keys:
* `algorithm`
* `secret`

Example:
```
test_dnskey:
    algorithm: hmac-sha256
    secret: "EFh57V/BI2BeR0QqEzBMfBiaGriOK0azJQHle8QkxPE="  # DON'T USE THIS.
```

*Storing this in a vault is probably the right choice.*

Generating this is beyond the scope of this document, but as a quickstart:
```
$ /usr/sbin/tsig-keygen -r /dev/urandom test
key "test" {
        algorithm hmac-sha256;
        secret "EFh57V/BI2BeR0QqEzBMfBiaGriOK0azJQHle8QkxPE=";  <-- DON'T USE THIS.
};
```

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      become: true
      roles:
         - bind

TODO
----

* Maybe ditch the include and do the keys as a block?

License
-------

MIT License

Copyright (c) 2018 Ken Treadway

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
