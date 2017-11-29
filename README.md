[![Build Status](https://travis-ci.org/CSCfi/ansible-role-puppetmaster.svg?branch=master)](https://travis-ci.org/CSCfi/ansible-role-puppetmaster)

Puppet master Ansible role
==========================

This is an Ansible role for configuring a Puppet master. Most configuration is
actually done by Puppet and Ansible is simply used to bootstrap the
configuration process.

Usage
-----

Minimally, you will need to set a Git repository URL using
the puppet\_environments\_repo variable in e.g. host\_vars. This needs to point
to a Git repository that contains a so called control repository for Puppet.
This control repository contains:

  * manifests directory with site.pp and nodes.pp
  * hieradata directory containing Hiera data
  * Puppetfile for downloading Puppet modules using r10k

You will also need to set up your Hiera hierarchy as specified in the r10k.yaml
file under templates.

Place PKI keys and certificates in environment
----------------------------------------------

When using encryption in hiera, the keys need to be deployed before puppet can run on the puppetmaster.
Provide the keys via environment as following:

```sh
export HIERA_PRIVATE_KEY="$(cat credentials/hiera_private_key.pkcs7.pem)"
export HIERA_PUBLIC_KEY="$(cat credentials/hiera_public_key.pkcs7.pem)"
```

Optionally for the puppetmaster PKI keys can be provided via environment as well:

```sh
export PUPPETMASTER_CA_PRIVKEY="$(cat credentials/puppetmaster_ca_privkey.pem)"
export PUPPETMASTER_CA_CERT="$(cat credentials/puppetmaster_ca_cert.pem)"
```

Caveats
-------

You **must** set the inventory hostname for the Puppet master to be the same as
the host's FQDN.
