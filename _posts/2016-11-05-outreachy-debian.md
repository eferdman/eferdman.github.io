---
layout: post
title: Applying to Debian for Outreachy 2016
summary: Applying to the PKI Clean Room Project for Round 13 of Outreachy 
date:       2016-11-05
categories: debian outreachy
tags: 
- planetdebian
- outreachy
---

This year, [Outreachy](https://wiki.gnome.org/Outreachy/2016/DecemberMarch) featured internships from organizations such as Debian, Fedora, GNOME, the Linux Kernel, Mozilla, Python, and Wikimedia, just to name a few. Each organization features mentored projects and in order to apply, applicants must contact the mentor, introduce themselves on the appropriate channels and make a small contribution to the project. After that, applicants might be required to fulfill additional tasks to demonstrate their abilities. Successful applicants will make quality contributions, communicate effectively with mentors, ask questions, fulfill tasks, help out their peers via mailing lists, and/or blog about their experience.

One of the projects I applied to was the [Clean Room for PGP and X.509 (PKI) Key Management](https://wiki.debian.org/Outreachy/Round13#Outreachy.2FRound13.2FProjects.2FCleanRoomForPGPKeyManagement.Clean_Room_for_PGP_and_X.509_.28PKI.29_Key_Management). The project aims to create a Live Disc that enables users to create and manage their PGP keys easily and securely, using a text-based UI. I've been a Debian user for about a year, but before applying to the project I didn't know much about GnuPG or public key encryption. Since then, I've made some contributions and attended my first [keysigning event](https://www.meetup.com/OpenLate/events/234006159/) in San Francisco featuring a lecture by Neal Walfield (more on that below).

For my initial contribution, [Daniel Pocock](https://danielpocock.com), the mentor for this project, asked that I write a script that lists the USB flash devices connected to the system and specifies which device the system booted from. Here's the [bash script](https://lists.alioth.debian.org/pipermail/pki-clean-room-devel/attachments/20161013/bc064327/attachment.sh) that I wrote, and that was enough to submit an application for Debian. 

My next task was to write a dns hook script for the [dehydrated project](https://github.com/lukas2511/dehydrated), a shell client for signing certificates with Let's Encrypt (for free!). The script completes a dns challenge sent by the ACME-server by provisioning a TXT record for a given domain in order to prove ownership of the domain. I chose to write it in python and used the dnspython API. I posted my solution on [github](https://github.com/eferdman/dnspython-hook) and there are many more [here](https://github.com/lukas2511/dehydrated/wiki/Examples-for-DNS-01-hooks).

At the lecture, Neal talked about good practices for key creation and management. Here are a few of those points:

  * Don't store your master key locally

  * Store your master key offline on a smartcard such as GnuK or NitroKey and store backups on a USB stick.

  * Neal mentioned that the OpenPGP card is not open hardware and according to this recent post neither is the [Yubikey](https://www.yubico.com/2016/05/secure-hardware-vs-open-source/)

  * To manage the key, use a dedicated offline computer such as a relatively cheap x40 or x60 Thinkpad (my two cents: use a Thinkpad like X200 or T400 flashed with Libreboot, which solves the proprietary firmware problem) and remove the wireless network card.

  * Use Tails which wipes memory on shutdown.

  * Use subkeys-- an encryption subkey is automatically created with `gpg2 --gen-key`. [Create an additional signing subkey](https://wiki.debian.org/Subkeys).

  * Generate a secure passphrase for your master key using 5-12 words. Example: "pipe after harm horse split seize radar bulb" 
	* [Funny cartoon illustrating this concept](https://xkcd.com/936/)
  * Refresh your keys regularly for new preferences and revokation certificates. An alternative to `gpg2 --refresh-keys` is parcimonie, which uses tor and refreshes keys one at a time.

  * Don't back up `.gnupg/random_seed`

  * [More OpenPGP Best Practices](https://riseup.net/en/security/message-security/openpgp/best-practices)

See the [slides](ftp://ftp.gnupg.org/blurbs/an-advanced-introduction-to-gnupg.pdf) for Neal's full presentation. 
