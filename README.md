# ELK-install-configure

<h3> #Pre Pre Requisite</h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
User : root or user with root privilege 
OS: Ubuntu 18.x above
Memory : 4GB
CPU: 2
Java: Oracle JDK 8 Version 
</code></pre></div>

<h3> #Pre Pre Requisite</h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
User : root or user with root privilege 
OS: Ubuntu 18.x above
Memory : 4GB
CPU: 2
Java: Oracle JDK 8 Version 
</code></pre></div>

<h3> #Pre Requisite</h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
vagrant@linux:~$ sudo apt update

vagrant@linux:~$ sudo apt-get upgrade -y
</code></pre></div>

<h3> #Java version Pre-check</h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
vagrant@linux:~$ java -version

Command 'java' not found, but can be installed with:

sudo apt install default-jre              # version 2:1.11-72, or
sudo apt install openjdk-11-jre-headless  # version 11.0.11+9-0ubuntu2~20.04
sudo apt install openjdk-13-jre-headless  # version 13.0.7+5-0ubuntu1~20.04
sudo apt install openjdk-16-jre-headless  # version 16.0.1+9-1~20.04
sudo apt install openjdk-8-jre-headless   # version 8u292-b10-0ubuntu1~20.04
sudo apt install openjdk-14-jre-headless  # version 14.0.2+12-1~20.04

</code></pre></div>

<h3> #Install JDK</h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
vagrant@linux:~$ sudo apt install default-jre

vagrant@linux:~$ java -version
openjdk version "11.0.11" 2021-04-20
OpenJDK Runtime Environment (build 11.0.11+9-Ubuntu-0ubuntu2.20.04)
OpenJDK 64-Bit Server VM (build 11.0.11+9-Ubuntu-0ubuntu2.20.04, mixed mode, sharing)
</code></pre></div>


<h3> #Install JDK</h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
vagrant@linux:~$ sudo apt install default-jre

vagrant@linux:~$ java -version
openjdk version "11.0.11" 2021-04-20
OpenJDK Runtime Environment (build 11.0.11+9-Ubuntu-0ubuntu2.20.04)
OpenJDK 64-Bit Server VM (build 11.0.11+9-Ubuntu-0ubuntu2.20.04, mixed mode, sharing)
</code></pre></div>

<h3> #Download Oracle JDK</h3>
<p>Ref: <a href="
https://www.oracle.com/java/technologies/javase-downloads.html">
https://www.oracle.com/java/technologies/javase-downloads.html</a>&nbsp;</p>
<p align=left> Click the JDK Download button and you’ll be taken to a screen that shows the versions available. Click the .tar.gz package for Linux.</p>

<h3 align="left">
Java Download </h3>
<p align="left" <img src="https://github.com/rajkumarrt/icons/blob/main/jdk%20install.PNG"/> </a>



