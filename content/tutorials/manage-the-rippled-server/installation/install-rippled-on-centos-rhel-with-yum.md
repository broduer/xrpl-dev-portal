# Install on CentOS/Red Hat with yum

This page describes the recommended instructions for installing the latest stable version of `rippled` on **CentOS 7** or **Red Hat Enterprise Linux 7**, using Ripple's [yum](https://en.wikipedia.org/wiki/Yellowdog_Updater,_Modified) repository.

These instructions install a binary that has been compiled by Ripple.


## Prerequisites

Before you install `rippled`, you must meet the [System Requirements](system-requirements.html).


## Installation Steps

1. Install the Ripple RPM repository:

    Choose the appropriate RPM repository for the stability of releases you want:

    - `stable` for the latest production release (`master` branch)
    - `unstable` for pre-release builds (`release` branch)
    - `nightly` for experimental/development builds (`develop` branch)

    <!-- MULTICODE_BLOCK_START -->

    *Stable*

        $ cat << REPOFILE | sudo tee /etc/yum.repos.d/ripple.repo
        [ripple-stable]
        name=XRP Ledger Packages
        enabled=1
        gpgcheck=0
        repo_gpgcheck=1
        baseurl=https://repos.ripple.com/repos/rippled-rpm/stable/
        gpgkey=https://repos.ripple.com/repos/rippled-rpm/stable/repodata/repomd.xml.key
        REPOFILE

    *Pre-release*

        $ cat << REPOFILE | sudo tee /etc/yum.repos.d/ripple.repo
        [ripple-unstable]
        name=XRP Ledger Packages
        enabled=1
        gpgcheck=0
        repo_gpgcheck=1
        baseurl=https://repos.ripple.com/repos/rippled-rpm/unstable/
        gpgkey=https://repos.ripple.com/repos/rippled-rpm/unstable/repodata/repomd.xml.key
        REPOFILE

    *Development*

        $ cat << REPOFILE | sudo tee /etc/yum.repos.d/ripple.repo
        [ripple-nightly]
        name=XRP Ledger Packages
        enabled=1
        gpgcheck=0
        repo_gpgcheck=1
        baseurl=https://repos.ripple.com/repos/rippled-rpm/nightly/
        gpgkey=https://repos.ripple.com/repos/rippled-rpm/nightly/repodata/repomd.xml.key
        REPOFILE

    <!-- MULTICODE_BLOCK_START -->


2. Fetch the latest repo updates:

        $ sudo yum -y update

3. Install the new `rippled` package:

        $ sudo yum install rippled

    Version 1.3.1 does not require any changes to your config files (`rippled.cfg` and `validators.txt`). This update procedure leaves your existing config files in place.

4. Reload systemd unit files:

        $ sudo systemctl daemon-reload

5. Configure the `rippled` service to start on boot:

        $ sudo systemctl enable rippled.service

6. Start the `rippled` service:

        $ sudo systemctl start rippled.service


## Next Steps

{% include '_snippets/post-rippled-install.md' %}<!--_ -->


## See Also

- **Concepts:**
    - [The `rippled` Server](the-rippled-server.html)
    - [Introduction to Consensus](intro-to-consensus.html)
- **Tutorials:**
    - [Configure rippled](configure-rippled.html)
    - [Troubleshoot rippled](troubleshoot-the-rippled-server.html)
    - [Get Started with the rippled API](get-started-with-the-rippled-api.html)
- **References:**
    - [rippled API Reference](rippled-api.html)
        - [`rippled` Commandline Usage](commandline-usage.html)
        - [server_info method][]


<!--{# common link defs #}-->
{% include '_snippets/rippled-api-links.md' %}
{% include '_snippets/tx-type-links.md' %}
{% include '_snippets/rippled_versions.md' %}
