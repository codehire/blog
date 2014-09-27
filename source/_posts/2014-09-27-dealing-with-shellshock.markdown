---
layout: post
title: "Dealing with Shellshock"
date: 2014-09-27 11:51:01 +1000
comments: true
categories: [Security]
author: Dan Draper
---

![Bash Security Problem](/images/shellshock.png)

## Critical Bash Security Hole

In case you haven't heard, a severe security problem, dubbed _ShellShock_ was found in Bash last week and it affects virtually every flavour
of Linux and BSD, including MacOSX. It appears that Apple have not yet released an official patch but unless you're running a webserver on your Macbook Pro you probably don't need to worry for now. If you are concerned you can follow [these instructions](http://security.stackexchange.com/questions/68202/how-to-patch-bash-on-osx-in-wake-of-shellshock).

## To check if you are vulnuerable

Most likely, if you don't have someone managing your servers for you they will be unpatched. You can check with the following command:

{% highlight bash %}
env x='() { :;}; echo vulnerable' bash -c 'echo hello'
{% endhighlight %}

If you see vulnerable in the output, you are vulnerable. AskUbuntu has a [longer explaination](http://askubuntu.com/questions/528101/what-is-the-cve-2014-6271-bash-vulnerability-shellshock-and-how-do-i-fix-it).

{% highlight bash %}
hello
vulnerable
{% endhighlight %}

### Patching your servers

#### Ubuntu 14.04

On ubuntu do the following:

{% highlight bash %}
sudo apt-get update
sudo apt-get install bash
{% endhighlight %}

To check that you have updated, make sure the version is as follows:

{% highlight bash %}
dpkg -s bash | grep Version
=> Version: 4.3-7ubuntu1.3
{% endhighlight %}

I had lots of servers to do so I put all of my server hostnames in a file called `servers` and ran:

{% highlight bash %}
for i in `cat servers`; do ssh -t "deploy@$i" "sudo apt-get update && sudo apt-get install bash"; done
{% endhighlight %}

I just had to enter my password for sudo each time but was still a lot faster than manually logging in to each server.

#### Older Ubuntu Systems

The same steps above will work but you may need to check to see that an update has been provided for your distro version. Older versions may be unsupported and may not have a patch available yet.

If you don't have an official update for your version, you can follow these steps:

{% highlight bash %}
mkdir src
cd src
wget http://ftp.gnu.org/gnu/bash/bash-4.3.tar.gz
#download all patches
for i in $(seq -f "%03g" 0 26); do wget http://ftp.gnu.org/gnu/bash/bash-4.3-patches/bash43-$i; done
tar zxvf bash-4.3.tar.gz 
cd bash-4.3
#apply all patches
for i in $(seq -f "%03g" 0 26);do patch -p0 < ../bash43-$i; done
#build and install
./configure --prefix=/ && make && make install
cd .. 
cd ..
rm -r src
{% endhighlight %}

*These steps were shared [Stack Exchange](http://superuser.com/questions/816787/how-do-i-patch-the-shellshock-vulnerability-on-an-obsolete-ubuntu-system-that-i), I haven't tested them myself.*

#### Redhat, Fedora, CentOS

To patch, just update to the latest version of Bash and then use the steps above to check that the vulnerability is no longer present. You may need to check that the specific version of your disto has a patch available.

{% highlight bash %}
yum update bash
{% endhighlight %}

#### MacOSX

There is no official patch for MacOSX yet but as mentioned above, unless you're using your laptop as a webserver then it probably doesn't affect you right now. See [these instructions](http://security.stackexchange.com/questions/68202/how-to-patch-bash-on-osx-in-wake-of-shellshock) if you're concerned. 

Happy Patching!
