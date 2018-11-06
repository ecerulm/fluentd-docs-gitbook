::: {#main .section}
::: {#page}
::: {.topic_content}
::: {style="text-align:right"}
::: {style="text-align:right"}
Versions \| [v1.0 (td-agent3)](/v1.0/articles/install-by-dmg) \|
***v0.12* (td-agent2) **
:::
:::

------------------------------------------------------------------------

Installing Fluentd using .dmg Installer (MacOS X)
=================================================

This article explains how to install td-agent, the stable Fluentd
distribution package maintained by [Treasure Data,
Inc](http://www.treasuredata.com/), on MacOS X.

[]{#what-is-td-agent?}

::: {#table-of-contents .section}
### Table of Contents

-   [What is td-agent?](#what-is-td-agent?)
-   [Step1: Install td-agent](#step1:-install-td-agent)
-   [Step2: Launch td-agent](#step2:-launch-td-agent)
-   [Step3: Post Sample Logs via
    HTTP](#step3:-post-sample-logs-via-http)
-   [Uninstall td-agent](#uninstall-td-agent)
-   [Next Steps](#next-steps)
:::

What is td-agent?
-----------------

Fluentd is written in Ruby for flexibility, with performance sensitive
parts written in C. However, casual users may have difficulty installing
and operating a Ruby daemon.

That's why [Treasure Data, Inc](http://www.treasuredata.com/) is
providing **the stable distribution of Fluentd**, called `td-agent`. The
differences between Fluentd and td-agent can be found
[here](http://www.fluentd.org/faqs).

For MacOS X, we're using the OS native .dmg Installer to distribute
td-agent.

[]{#step1:-install-td-agent}

Step1: Install td-agent
-----------------------

Please download the `.dmg` file from here, and install the software.

-   [Download](https://td-agent-package-browser.herokuapp.com/2/macosx)

[]{#step2:-launch-td-agent}

Step2: Launch td-agent
----------------------

You can launch `td-agent` with `launchctl` command. Please make sure the
daemon started correctly from the log
(`/var/log/td-agent/td-agent.log`).

``` {.CodeRay}
$ sudo launchctl load /Library/LaunchDaemons/td-agent.plist
$ less /var/log/td-agent/td-agent.log
2013-04-19 16:55:03 -0700 [info]: starting fluentd-0.10.33
2013-04-19 16:55:03 -0700 [info]: reading config file path="/etc/td-agent/td-agent.conf"
```

**Your configuration file** is located at `/etc/td-agent/td-agent.conf`.
Your plugin directory is at `/etc/td-agent/plugin`. In case you want to
stop the agent, please execute the command below.

``` {.CodeRay}
$ sudo launchctl unload /Library/LaunchDaemons/td-agent.plist
```

[]{#step3:-post-sample-logs-via-http}

Step3: Post Sample Logs via HTTP
--------------------------------

By default, `/etc/td-agent/td-agent.conf` is configured to take logs
from HTTP and route them to stdout (`/var/log/td-agent/td-agent.log`).
You can post sample log records using the curl command.

``` {.CodeRay}
$ curl -X POST -d 'json={"json":"message"}' http://localhost:8888/debug.test
$ tail -n 1 /var/log/td-agent/td-agent.log
2013-04-19 16:51:47 -0700 debug.test: {"json":"message"}
```

[]{#uninstall-td-agent}

Uninstall td-agent
------------------

td-agent for Mac doesn't provide uninstallation app unlike rpm / deb. If
you want to uninstall td-agent from your Mac, remove these files /
directories.

-   /Library/LaunchDaemons/td-agent.plist
-   /etc/td-agent
-   /opt/td-agent
-   /var/log/td-agent

[]{#next-steps}

Next Steps
----------

You're now ready to collect your real logs using Fluentd. Please see the
following tutorials to learn how to collect your data from various data
sources.

-   Basic Configuration
    -   [Config File](config-file)
-   Application Logs
    -   [Ruby](ruby), [Java](java), [Python](python), [PHP](php),
        [Perl](perl), [Node.js](nodejs), [Scala](scala)
-   Examples
    -   [Store Apache Log into Amazon S3](apache-to-s3)
    -   [Store Apache Log into MongoDB](apache-to-mongodb)
    -   [Data Collection into HDFS](http-to-hdfs)

Please refer to the resources below for further steps.

-   [ChangeLog of
    td-agent](http://docs.treasuredata.com/articles/td-agent-changelog)
-   [Chef Cookbook](https://github.com/treasure-data/chef-td-agent/)

::: {style="text-align:right"}
Last updated: 2016-10-21 06:12:48 UTC
:::

------------------------------------------------------------------------

::: {style="text-align:right"}
Versions \| [v1.0 (td-agent3)](/v1.0/articles/install-by-dmg) \|
***v0.12* (td-agent2) **
:::

------------------------------------------------------------------------

If this article is incorrect or outdated, or omits critical information,
please [let us
know](https://github.com/fluent/fluentd-docs/issues?state=open).
[Fluentd](http://www.fluentd.org/) is a open source project under [Cloud
Native Computing Foundation (CNCF)](https://cncf.io/). All components
are available under the Apache 2 License.
:::
:::
:::