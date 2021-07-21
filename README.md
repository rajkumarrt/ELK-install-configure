# ELK-install-configure

<h3> #Pre Requisite</h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
User : root or user with root privilege 
OS: Ubuntu 18.x above
Memory : 4GB
CPU: 2
Java: Oracle JDK 8 Version 
</code></pre></div>

<h3> #Update the system</h3>
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

<h3> #IInstall NginxK</h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
vagrant@linux:~$sudo apt-get install nginx
</code></pre></div>

<h3> #Add Repository </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
vagrant@linux:~$wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
</code></pre></div>

<h3> #Install apt-transport-https </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
vagrant@linux:~$ sudo apt-get install apt-transport-https
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following NEW packages will be installed:
  apt-transport-https
0 upgraded, 1 newly installed, 0 to remove and 3 not upgraded.
Need to get 0 B/4,680 B of archives.
After this operation, 162 kB of additional disk space will be used.
Selecting previously unselected package apt-transport-https.
(Reading database ... 269462 files and directories currently installed.)
Preparing to unpack .../apt-transport-https_2.0.6_all.deb ...
Unpacking apt-transport-https (2.0.6) ...
Setting up apt-transport-https (2.0.6) ...
</code></pre></div>

<h3> # Install Elastic search</h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
#Add system repositories
vagrant@linux:~$ echo “deb https://artifacts.elastic.co/packages/7.x/apt stable main” | sudo tee –a /etc/apt/sources.list.d/elastic-7.x.list

“deb https://artifacts.elastic.co/packages/7.x/apt stable main”

#install
vagrant@linux:~$ sudo apt-get update


vagrant@linux:~$ sudo apt-get install elasticsearch
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following NEW packages will be installed:
  elasticsearch
0 upgraded, 1 newly installed, 0 to remove and 1631 not upgraded.
Need to get 327 MB of archives.
After this operation, 545 MB of additional disk space will be used.
Get:1 https://artifacts.elastic.co/packages/7.x/apt stable/main amd64 elasticsearch amd64 7.13.4 [327 MB]
Fetched 327 MB in 59s (5,516 kB/s)                                                                                                                                                                                
Selecting previously unselected package elasticsearch.
(Reading database ... 269466 files and directories currently installed.)
Preparing to unpack .../elasticsearch_7.13.4_amd64.deb ...
Creating elasticsearch group... OK
Creating elasticsearch user... OK
Unpacking elasticsearch (7.13.4) ...
Setting up elasticsearch (7.13.4) ...
Created elasticsearch keystore in /etc/elasticsearch/elasticsearch.keystore
Processing triggers for ureadahead (0.100.0-21) ...
Processing triggers for systemd (245.4-4ubuntu3.10) ...
</code></pre></div>

<h3> #Modify the config file </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
vagrant@linux:~$sudo vim /etc/elasticsearch/elasticsearch.yml

uncomment  the below lines
#network.host: 192.168.0.1
#http.port: 9200)

Change (network.host: 192.168.0.1 to network.host: localhost)

# ---------------------------------- Network -----------------------------------
#
# By default Elasticsearch is only accessible on localhost. Set a different
# address here to expose this node on the network:
#
network.host: localhost
#
# By default Elasticsearch listens for HTTP traffic on the first free port it
# finds starting at 9200. Set a specific HTTP port here:
#
http.port: 9200
</code></pre></div>

<h3> # Update the JVM heap size</h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
uncomment -Xms and -Xmx and provide value of 512m

##New Value
-Xms512m
-Xmx1024m
</code></pre></div>

<h3> # Start the service</h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
vagrant@linux:~$ sudo systemctl start elasticsearch.service

vagrant@linux:~$ sudo systemctl enable elasticsearch.service
</code></pre></div>

<h3> # Test the Elastic search</h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
vagrant@linux:~$curl http://localhost:9200
{
  "name" : "linux",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "Kb8Qar5XQRSorFWLwho_wg",
  "version" : {
    "number" : "7.13.4",
    "build_flavor" : "default",
    "build_type" : "deb",
    "build_hash" : "c5f60e894ca0c61cdbae4f5a686d9f08bcefc942",
    "build_date" : "2021-07-14T18:33:36.673943207Z",
    "build_snapshot" : false,
    "lucene_version" : "8.8.2",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
</code></pre></div>
------------------------------------------------------------------------------------------
<h3> #Install Kibana </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
vagrant@linux:~$sudo apt-get install kibana
</code></pre></div>

<h3> #Update the configuration </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
Uncomment the below settings
server.port: 5601

server.host: "localhost"

elasticsearch.hosts: ["http://localhost:9200"]
</code></pre></div>

<h3> #Start Kibana </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
vagrant@linux:~$ sudo systemctl start kibana

vagrant@linux:~$ sudo systemctl enable kibana
Synchronizing state of kibana.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable kibana
Created symlink /etc/systemd/system/multi-user.target.wants/kibana.service → /etc/systemd/system/kibana.service.
</code></pre></div>

<h3> #Allow traffic on 5601 </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
vagrant@linux:~$ sudo ufw allow 5601/tcp
Rules updated
Rules updated (v6)
</code></pre></div>
===========================================================================================================================
<h3> #Install Logstash </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
vagrant@linux:~$ sudo apt-get install logstash
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following NEW packages will be installed:
  logstash
0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
Need to get 363 MB of archives.
After this operation, 625 MB of additional disk space will be used.
Get:1 https://artifacts.elastic.co/packages/7.x/apt stable/main amd64 logstash amd64 1:7.13.4-1 [363 MB]
Fetched 363 MB in 1min 18s (4,664 kB/s)                                                                                                                                                                       
Selecting previously unselected package logstash.
(Reading database ... 333823 files and directories currently installed.)
Preparing to unpack .../logstash_1%3a7.13.4-1_amd64.deb ...
Unpacking logstash (1:7.13.4-1) ...
Setting up logstash (1:7.13.4-1) ...
Using bundled JDK: /usr/share/logstash/jdk
Using provided startup.options file: /etc/logstash/startup.options
OpenJDK 64-Bit Server VM warning: Option UseConcMarkSweepGC was deprecated in version 9.0 and will likely be removed in a future release.
/usr/share/logstash/vendor/bundle/jruby/2.5.0/gems/pleaserun-0.0.32/lib/pleaserun/platform/base.rb:112: warning: constant ::Fixnum is deprecated
Successfully created system startup script for Logstash
</code></pre></div>

<h3> # Start Logstash service </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
vagrant@linux:~$ sudo systemctl start logstash

vagrant@linux:~$ sudo systemctl enable logstash
Created symlink /etc/systemd/system/multi-user.target.wants/logstash.service → /etc/systemd/system/logstash.service.
</code></pre></div>
=======================================================================================================================================

<h3> # Install Filebeat</h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
vagrant@linux:~$ sudo apt-get install filebeat
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following NEW packages will be installed:
  filebeat
0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
Need to get 36.3 MB of archives.
After this operation, 142 MB of additional disk space will be used.
Get:1 https://artifacts.elastic.co/packages/7.x/apt stable/main amd64 filebeat amd64 7.13.4 [36.3 MB]
Fetched 36.3 MB in 12s (3,106 kB/s)                                                                                                                                                                               
Selecting previously unselected package filebeat.
(Reading database ... 350653 files and directories currently installed.)
Preparing to unpack .../filebeat_7.13.4_amd64.deb ...
Unpacking filebeat (7.13.4) ...
Setting up filebeat (7.13.4) ...
Processing triggers for ureadahead (0.100.0-21) ...
Processing triggers for systemd (245.4-4ubuntu3.10) ...

</code></pre></div>

<h3> #Update configuration </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
Comment below lines

vagrant@linux:~$ sudo vim /etc/filebeat/filebeat.yml

#output.elasticsearch:
  # Array of hosts to connect to.
  #hosts: ["localhost:9200"]

Uncomment below lines
output.logstash:
  # The Logstash hosts
  hosts: ["localhost:5044"]
</code></pre></div>

<h3> #Enable the filesystem module </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
vagrant@linux:~$ sudo vim /etc/filebeat/filebeat.yml
</code></pre></div>

<h3> #Load the template </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
vagrant@linux:~$ sudo filebeat setup --index-management -E output.logstash.enabled=false -E 'output.elasticsearch.hosts=["localhost:9200"]'

Overwriting ILM policy is disabled. Set `setup.ilm.overwrite: true` for enabling.
</code></pre></div>

<h3> #Start the Filebeat </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
vagrant@linux:~$ sudo systemctl start filebeat

vagrant@linux:~$ sudo systemctl enable filebeat
Synchronizing state of filebeat.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable filebeat
Created symlink /etc/systemd/system/multi-user.target.wants/filebeat.service → /lib/systemd/system/filebeat.service.
</code></pre></div>

<h3> #Verify the Elastic search data </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="ELK"><pre><code>
curl -XGET http://localhost:9200/_cat/indices?v
</code></pre></div>

Thenn try the url http://localhost:5601
