# cure-perfctl

A very simple utility to remove the perfctl malware.

__Any contributions are highly appreciated__

## Stating the obvious

Know your enemy (https://www.aquasec.com/blog/perfctl-a-stealthy-malware-targeting-millions-of-linux-servers/).

Check your system with [rkhunter](https://rkhunter.sourceforge.net/) - can be installed as a standard system package. And with chkrootkit (`chkrootkit -x lkm`).

It is important to note that you need to remove the vulnerability from your system first, otherwise it will keep getting reinfected.

The easiest way is always to reinstall the machine from scratch as this leads to the latest versions of software being installed.

This utility works on our Debian 12 machines. Before blindly running it, please see what is inside and tweak accordingly.

The tool reboots the machine abruptly, possibly leaving something in an unpredictable state.

## How it works?

It installs a systemd service that runs before perfctl and moves it to a safe location.

In our case, the executable was `/bin/perfcc`.

We did not find any hook in the libraries, LD preload etc. So this is not covered

You can find the isolated files under `/root/perfctl` afterwards.

## How to use it?

The tool does not handle the machine in gloves. Do not just bluntly run it. Read the source first and tweak it.

Find occurrences of perfctl on your machine. `grep -rl "perfcc" /` might be a good way.

Tweak the scripts accordingly.

Run as root.
