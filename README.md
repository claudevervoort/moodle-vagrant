Moodle on vagrant-php-box
===============

Set up super fast a PHP5 development box with apache, mysql, phpmyadmin and whatever else that you may need.

Changes from original Vagrant was to go to php5.6, and add missing php packages needed by Moodle, prep the DB and add the CRON.

<h2>How to run</h2>

<ul>
  <li>
    Install vagrant using the installation instructions in the 
    <a href="http://docs.vagrantup.com/v2/installation/" /target="_blank">Getting Started document</a>
  </li>
  <li>Clone this repository and run $ vagrant up</li>
  <li>Modify the Vagrant File to point the Sync Folders to where your moodle code is, and where the mooodledata should go</li>
  <li>IP is 192.168.10.10, so add it to your host file with the domain name of your choosing</li>
  <li>Acess http://<your_domain>/install.php and go through the install</li>
  <li>If you need to re-install be sure to first remove the config.php added to your moodle folder</p>
</ul>

<h2>PHP My Admin</h2>
<ul>
  <li>Available on localhost:8080/phpmyadmin</li>
  <li>User: root Password: root</li>
</ul>


