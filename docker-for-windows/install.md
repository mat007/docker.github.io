---
description: How to install Docker for Windows
keywords: windows, beta, edge, alpha, install, download
title: Install Docker for Windows
---

Docker for Windows is a desktop application based on
[Docker Community Edition (CE)](https://www.docker.com/community-edition).
The Docker for Windows install package includes everything you need to run
Docker on a Windows system. This topic describes pre-install considerations,
and how to download and install Docker for Windows.

> **Already have Docker for Windows?** If you already have
Docker for Windows installed, and are ready to get started, skip to
[Get started with Docker for Windows](index.md) for a quick tour of
the command line, preferences, and tools.

>**Looking for Release Notes?** Get release notes for [Stable](release-notes.md)
>and [Edge](edge-release-notes.md) releases.

> For **Windows Server on Docker Enterprise Edition**, see [Install Docker Enterprise Edition for Windows Server](/install/windows/docker-ee.md).

## Download Docker for Windows

You can download Docker for Windows installers from the **Stable** or **Edge** channel.

Both Stable and Edge installers come with <a
href="https://github.com/docker/cli/blob/master/experimental/README.md">
experimental features in Docker Engine</a> enabled by default. Experimental mode can be toggled on/off on the Daemon tab of the  [Settings dialog](index.md#daemon-experimental-mode).

For more about Stable and Edge channels, see the [FAQs](faqs.md#questions-about-stable-and-edge-channels).

<table style="width:100%">
  <tr>
    <th style="font-size: x-large; font-family: arial">Stable channel</th>
    <th style="font-size: x-large; font-family: arial;">Edge channel</th>
  </tr>
  <tr valign="top">
    <td width="33%">Stable is the best channel to use if you want a reliable platform to work with. Stable releases track the Docker platform stable releases.<br><br>
   On this channel, you can select whether to send usage statistics and other data. <br><br>Stable releases happen once per quarter.
    </td>
    <td width="33%">Use the Edge channel if you want to get experimental features faster, and can weather some instability and bugs. We collect usage data on Edge releases. <br><br>Edge builds are released once per month.
    </td>
  </tr>
  <tr valign="top">
    <td width="33%">
      <a class="button outline-btn" href="https://download.docker.com/win/stable/Docker%20for%20Windows%20Installer.exe">Get Docker for Windows (Stable)</a>
    </td>
    <td width="33%">
      <a class="button outline-btn" href="https://download.docker.com/win/edge/Docker%20for%20Windows%20Installer.exe">Get Docker for Windows (Edge)</a>
    </td>
  </tr>
  <tr valign="top">
    <td width="33%"><a href="https://download.docker.com/win/stable/Docker%20for%20Windows%20Installer.exe.sha256sum"><font color="#BDBDBD" size="-1">Checksum: Stable installer SHA256</font></a>
  </td>
    <td width="33%"><a href="https://download.docker.com/win/edge/Docker%20for%20Windows%20Installer.exe.sha256sum"><font color="#BDBDBD" size="-1">Checksum: Edge installer SHA256</font></a>
    </td>
  </tr>
</table>

* Legacy (`.msi`) installers are available for [Edge](https://download.docker.com/win/edge/InstallDocker.msi) and [Stable](https://download.docker.com/win/stable/InstallDocker.msi) channels.

* Docker for Windows is designed to configure Docker development environments on Windows 10. You can develop both _Docker Linux_ containers and _Docker Windows_ containers. To run Docker Windows containers in production, see [Install Docker Enterprise Edition for Windows Server](/install/windows/docker-ee.md). To run Docker Linux containers in production, see [Install Docker](/install/index.md).

* Docker for Windows requires 64-bit Windows 10 Pro with Hyper-V available. See [What to know before you install](install.md#what-to-know-before-you-install) for a full list
of prerequisites.

* You can switch between Edge and Stable versions, but you can only have one app
installed at a time. Also, you need to save images and export containers you
want to keep before uninstalling the current version before installing another.
For more about this, see the [FAQs about Stable and Edge channels](faqs.md#questions-about-stable-and-edge-channels).

##  What to know before you install

If your system does not meet the requirements to run Docker for Windows, you can install
[Docker Toolbox](/toolbox/overview.md), which uses Oracle Virtual Box instead of
Hyper-V.

* **README FIRST for Docker Toolbox and Docker Machine users**: Docker for Windows requires Microsoft Hyper-V to run.  The Docker for Windows installer enables Hyper-V for you, if needed, and restart your machine. After Hyper-V is
enabled, VirtualBox no longer works, but any VirtualBox VM images
remain. VirtualBox VMs created with `docker-machine` (including the `default`
one typically created during Toolbox install) no longer start. These VMs
cannot be used side-by-side with Docker for Windows. However, you can still use
`docker-machine` to manage remote VMs.
<p />
* Virtualization must be enabled in BIOS and CPU SLAT-capable. Typically, virtualization is enabled by default. This is different from having Hyper-V enabled. For more
detail see [Virtualization must be
enabled](troubleshoot.md#virtualization-must-be-enabled) in Troubleshooting.
<p />
* The current version of Docker for Windows runs on 64bit Windows 10 Pro, Enterprise and Education (1607 Anniversary Update, Build 14393 or later).
<p />
* Containers and images created with Docker for Windows are shared between all user accounts on machines where it is installed. This is because all
Windows accounts use the same VM to build and run containers.
<p />
* Nested virtualization scenarios, such as running Docker for Windows
on a VMWare or Parallels instance, might work, but come with no
guarantees. For more information, see
[Running Docker for Windows in nested virtualization scenarios](troubleshoot.md#running-docker-for-windows-in-nested-virtualization-scenarios)
<p />
* **What the Docker for Windows install includes**: The installation provides [Docker Engine](/engine/userguide/), Docker CLI client, [Docker Compose](/compose/overview.md), [Docker Machine](/machine/overview.md), and [Kitematic](/kitematic/userguide.md).

### About Windows containers

Looking for information on using Windows containers?

* [Switch between Windows and Linux containers](index.md#switch-between-windows-and-linux-containers) describes the Linux / Windows containers toggle in Docker for Windows and points you to the tutorial mentioned above.
<p />
* [Getting Started with Windows Containers (Lab)](https://github.com/docker/labs/blob/master/windows/windows-containers/README.md)
provides a tutorial on how to set up and run Windows containers on Windows 10 or
with Windows Server 2016. It shows you how to use a MusicStore application with
Windows containers.
<p />
* Docker Container Platform for Windows Server 2016 [articles and blog posts](https://www.docker.com/microsoft/) on the Docker website

## Install Docker for Windows desktop app

1. Double-click **Docker for Windows Installer.exe** to run the installer.

    If you haven't already downloaded the installer (`Docker for Windows Installer.exe`), you can get it from
    [**download.docker.com**](https://download.docker.com/win/stable/Docker%20for%20Windows%20Installer.exe).
    It typically downloads to your `Downloads folder`, or you can run it from the recent downloads bar at the
    bottom of your web browser.

2. Follow the install wizard to accept the license, authorize the installer, and proceed with the install.

    You are asked to authorize `Docker.app` with your system password during the install process.
    Privileged access is needed to install networking components, links to the Docker apps, and manage the
    Hyper-V VMs.

3. Click **Finish** on the setup complete dialog to launch Docker.

## Start Docker for Windows

Docker does not start automatically after installation. To start it, search for
Docker, select **Docker for Windows** in the search results, and click it (or
hit Enter).

![search for Docker app](images/docker-app-search.png){:width="400px"}

When the whale in the status bar stays steady, Docker is up-and-running, and
accessible from any terminal window.

![whale on taskbar](images/whale-icon-systray.png)

If the whale is hidden in the Notifications area, click the up arrow on the
taskbar to show it. To learn more, see [Docker Settings](index.md#docker-settings).

If you just installed the app, you also get a popup success message with
suggested next steps, and a link to this documentation.

![Startup information](images/docker-app-welcome.png){:width="400px"}

When initialization is complete, select **About Docker** from the notification
area icon to verify that you have the latest version.

Congratulations! You are up and running with Docker for Windows.

## Where to go next

* [Getting started](index.md) introduces Docker for Windows.

* [Get started with Docker](/get-started/) is a tutorial that teaches you how to deploy a multi-service stack.

* [Troubleshooting](troubleshoot.md) describes common problems, workarounds, and how to get support.

* [FAQs](faqs.md) provides answers to frequently asked questions.

* [Stable Release Notes](release-notes.md) or [Edge Release Notes](edge-release-notes.md).
