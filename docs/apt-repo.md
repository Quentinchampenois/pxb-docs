# Install with the Percona-release Tool on Debian-based Systems

Ready-to-use packages are available from the Percona XtraBackup software
repositories and the [download page].

Specific information on the supported platforms, products, and versions is
described in [Percona Release Lifecycle Overview].

## Install Percona XtraBackup through percona-release

Install Percona XtraBackup, like many other Percona products, with the `percona-release` package configuration tool.
{.power-number}

1. Use the apt package manager to dowload `percona-release`:

    ```{.bash data-prompt="$"}
    $ sudo apt update
    ```

    ??? example "Expected output"

        ```{.text .no-copy}
        Get:1 http://security.ubuntu.com/ubuntu jammy-security InRelease [129 kB]
        Get:2 http://archive.ubuntu.com/ubuntu jammy InRelease [270 kB]
        Get:3 http://archive.ubuntu.com/ubuntu jammy-updates InRelease [128 kB]
        Get:4 http://security.ubuntu.com/ubuntu jammy-security/main amd64 Packages [2458 kB]
        ...
        Building dependency tree... Done
        Reading state information... Done
        All packages are up to date.
        ```

2. Install the `curl` download utility if it's not installed:

    ```{.bash data-prompt="$"}
    $ sudo apt install curl
    ```
    ??? example "Expected output"

        ```{.text .no-copy}
        Reading package lists... Done
        Building dependency tree... Done
        Reading state information... Done
        The following additional packages will be installed:
        ...
        Updating certificates in /etc/ssl/certs...
        0 added, 0 removed; done.########################################################...] 
        Running hooks in /etc/ca-certificates/update.d...
        done.
        ```

3. Download the `percona-release` the repository package:

    ```{.bash data-prompt="$"}
    $ curl -O https://repo.percona.com/apt/percona-release_latest.generic_all.deb
    ```

    ??? example "Expected output"

        ```{.text .no-copy}
        % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                        Dload  Upload   Total   Spent    Left  Speed
        100 16510  100 16510    0     0  29915      0 --:--:-- --:--:-- --:--:-- 30127
        ```

4. Install the downloaded package and its dependencies using `apt`:

    ```{.bash data-prompt="$"}
    sudo apt install gnupg2 lsb-release ./percona-release_latest.generic_all.deb
    ```

    ??? example "Expected output"

        ```{.text .no-copy}
        Reading package lists... Done
        Building dependency tree... Done
        Reading state information... Done
        ...
        For example, to enable the Percona Distribution for MySQL 8.0 repository use:

          percona-release setup pdps8.0

        Note: To avoid conflicts with older product versions, the percona-release setup command may disable our original repository for some products.

        For more information, please visit:
        https://docs.percona.com/percona-software-repositories/percona-release.html

        Processing triggers for libc-bin (2.35-0ubuntu3.8) ...
        ```

5. Refresh the local cache to update the package information:

    ```{.bash data-prompt="$"}
    $ sudo apt update
    ```

    ??? example "Expected output"

        ```{.text .no-copy}
        Get:1 http://security.ubuntu.com/ubuntu jammy-security InRelease [129 kB]
        Get:2 http://archive.ubuntu.com/ubuntu jammy InRelease [270 kB]
        Get:3 http://archive.ubuntu.com/ubuntu jammy-updates InRelease [128 kB]
        Get:4 http://security.ubuntu.com/ubuntu jammy-security/main amd64 Packages [2458 kB]
        ...
        Building dependency tree... Done
        Reading state information... Done
        All packages are up to date.
        ```

6. Enable the specific percona-release product.

    ```{.bash data-prompt="$"}
    $ sudo percona-release enable pxb-84-lts
    ```
    ??? example "Expected output"

        ```{.text .no-copy}
        * Enabling the Percona Packaging Repository repository
        Hit:1 http://repo.percona.com/pmm2-client/apt jammy InRelease
        Hit:2 http://archive.ubuntu.com/ubuntu jammy InRelease                     
        Hit:3 http://repo.percona.com/prel/apt jammy InRelease                     
        Hit:4 http://security.ubuntu.com/ubuntu jammy-security InRelease
        Hit:5 http://archive.ubuntu.com/ubuntu jammy-updates InRelease
        Get:6 http://repo.percona.com/pxb-84-lts/apt jammy InRelease [12.8 kB]
        Hit:7 http://archive.ubuntu.com/ubuntu jammy-backports InRelease
        Hit:8 http://repo.percona.com/telemetry/apt jammy InRelease
        Get:9 http://repo.percona.com/pxb-84-lts/apt jammy/main Sources [855 B]
        Get:10 http://repo.percona.com/pxb-84-lts/apt jammy/main amd64 Packages [3547 B]
        Fetched 17.2 kB in 4s (3958 B/s)   
        Reading package lists... Done
        ```

7. Install Percona XtraBackup.

    ```{.bash data-prompt="$"}
    $ sudo apt install percona-xtrabackup-84
    ```

    ??? example "Expected output"

        ```{.text .no-copy}
        Reading package lists... Done
        Building dependency tree... Done
        Reading state information... Done
        The following additional packages will be installed:
        libaio1 libcurl4-openssl-dev libdbd-mysql-perl libdbi-perl libev4 libgdbm-compat4
        libgdbm6 libmysqlclient21 libperl5.34 libpopt0 mysql-common netbase perl
        perl-modules-5.34 rsync zstd
        ...
        Setting up libdbd-mysql-perl:amd64 (4.050-5ubuntu0.22.04.1) ...##############.......] 
        Setting up percona-xtrabackup-84 (8.4.0-1-1.jammy) ...#########################.....] 
        Processing triggers for libc-bin (2.35-0ubuntu3.8) ...###########################...] 
        ```

8. Verify the installation.

    ```{.bash data-prompt="$"}
    $ xtrabackup --version
    ```

    ??? example "Expected output"

        ```{.text .no-copy}
        xtrabackup version 8.4.0-1 based on MySQL server 8.4.0 Linux (x86_64) (revision id: da6e1abd)
        ```

9. To decompress backups made using `LZ4` or `ZSTD` compression algorithm, install the corresponding package:

    === "Install the `lz4` package"

        ```{.bash data-prompt="$"}
        $ sudo apt install lz4
        ```

    === "Install the `zstd` package"

        ```{.bash data-prompt="$"}
        $ sudo apt install zstd
        ```

!!! note
 
    For AppArmor profile information, see [Working with AppArmor](work-with-apparmor.md).


!!! admonition "See also"

    To install Percona XtraBackup using downloaded deb packages, see [Install Percona XtraBackup {{vers}}](apt-download-deb.md).

    To uninstall Percona XtraBackup, see [Uninstall Percona XtraBackup {{vers}}](apt-uninstall-xtrabackup.md)

[download page]: https://www.percona.com/downloads
[Percona Release Lifecycle Overview]: https://www.percona.com/services/policies/percona-software-platform-lifecycle#mysql