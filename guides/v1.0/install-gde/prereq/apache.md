---
layout: default
group: install
subgroup: Prerequisites
title: Apache
menu_title: Apache
menu_order: 2
github_link: install-gde/prereq/apache.md
---


#### Contents

*	<a href="#apache-support">Apache versions supported</a>
*	<a href="#apache-help-beginner">Help if you're just starting out</a>
*	<a href="#install-prereq-apache-ubuntu">Installing Apache on Ubuntu</a>
*	<a href="#install-prereq-apache-centos">Installing Apache on CentOS</a>

<h2 id="apache-support">Apache versions supported</h2>

Magento requires Apache 2.2.x or 2.4.x.

<h2 id="apache-help-beginner">Help if you're just starting out</h2>
If you're new to all this and need some help getting started, we suggest the following:

*	<a href="{{ site.gdeurl }}install-gde/basics/basics_magento-installed.html">Is the Magento software installed already?</a>
*	<a href="{{ site.gdeurl }}install-gde/basics/basics_software.html">What is the software that the Magento server needs to run?</a>
*	<a href="{{ site.gdeurl }}install-gde/basics/basics_os-version.html">What operating system is my server running?</a>
*	<a href="{{ site.gdeurl }}install-gde/basics/basics_login.html">How do I log in to my Magento server using a terminal, command prompt, or SSH?</a>


<h2 id="install-prereq-apache-ubuntu">Installing Apache on Ubuntu</h2>
Install Apache 2 if you haven't already done so:

	apt-get -y install apache2

<h3 id="install-ubuntu-apache-rewrites">Enabling Apache rewrites</h3>
Ubuntu 12 (which natively supports Apache 2.2) is different from Ubuntu 14 (which natively supports Apache 2.4).

It's very important you choose a value for `AllowOverride` that is suited to your deployment. You can use `AllowOverride All` in development but it might not be desirable in production.

More information about `AllowOverride`:

*	<a href="http://httpd.apache.org/docs/2.2/mod/core.html#allowoverride" target="_blank">Apache 2.2</a>
*	<a href="http://httpd.apache.org/docs/current/mod/core.html#allowoverride" target="_blank">Apache 2.4</a>

See one of the following sections:

*	<a href="#apache-rewrites2.4">Enabling Apache Rewrites for Apache 2.4</a>
*	<a href="#apache-rewrites2.2">Enabling Apache Rewrites for Apache 2.2</a>

<h4 id="apache-rewrites2.4">Enabling Apache Rewrites for Apache 2.4</h4>
Use this section to enable Apache rewrites and specify <code>.htaccess</code> if you use Apache 2.4, which is supported by the default Ubuntu 14 repository.

1.	Enter the following command:

	<pre>a2enmod rewrite</pre>

2.	Specify the type of directives that can be used in <code>.htaccess</code>.

	For guidelines, see the <a href="http://httpd.apache.org/docs/current/mod/mod_rewrite.html" target="_blank">Apache 2.4 documentation</a>.

	Note that in Apache 2.4, the server's default site configuration file is <code>/etc/apache2/sites-available/000-default.conf</code>

	For example, you can add the following to the bottom of <code>000-default.conf</code>:

		<Directory "/var/www/html">
		AllowOverride <value from Apache site>
		</Directory>

	<div class="bs-callout bs-callout-info" id="info">
	<span class="glyphicon-class">
	<p>You must change the value of <code>AllowOverride</code> in the directive for the directory to which you expect to install the Magento software. For example, to install in the web server docroot, edit the directive in <code>&lt;Directory /var/www></code>.</p></span>
	</div>

3.	Restart Apache:

	<pre>service apache2 restart</pre>

Continue with the next prerequisite (<a href="{{ site.gdeurl }}install-gde/prereq/php-ubuntu.html">PHP Ubuntu</a>), or start your installation by going to <a href="{{ site.gdeurl }}install-gde/install/composer-clone.html">Install Composer and clone the Magento repository</a>.

<h4 id="apache-rewrites2.2">Enabling Apache Rewrites for Apache 2.2</h4>
Use this section to enable Apache rewrites and specify <code>.htaccess</code> if you use Apache 2.2, which is supported by the default Ubuntu 12 repository.

1.	Open the following file for editing.

		vim /etc/apache2/sites-available/default

2.	Locate the following block.

		<Directory /var/www/>
	    Options Indexes FollowSymLinks MultiViews
	    AllowOverride None
	    Order allow,deny
	    allow from all
		<Directory>

3.	Change the value of `AllowOverride` to `<value from Apache site>`.

		<Directory /var/www/>
		Options Indexes FollowSymLinks MultiViews
    	AllowOverride <value from Apache site>
    	Order allow,deny
    	allow from all
		<Directory>

4.	Save the file and exit the text editor.

5.	Configure Apache to use the <code>mod_rewrite</code> module.

		cd /etc/apache2/mods-enabled
		ln -s ../mods-available/rewrite.load

6.	Restart Apache.

	<pre>service apache2 restart</pre>

Continue with the next prerequisite (<a href="{{ site.gdeurl }}install-gde/prereq/php-ubuntu.html">PHP Ubuntu</a>), or start your installation by going to <a href="{{ site.gdeurl }}install-gde/install/composer-clone.html">Install Composer and clone the Magento repository</a>.

<h2 id="install-prereq-apache-centos">Installing Apache on CentOS</h2>

Magento requires Apache use server rewrites. You must also specify the type of directives that can be used in <code>.htaccess</code>, which Magento uses to specify rewrite rules.

Installing and configuring Apache is basically a three-step process: install the software, enable rewrites, and specify <code>.htaccess</code> directives.

<h3 id="apache-install-centos">Installing Apache</h3>
Install Apache 2 if you haven't already done so.

	yum -y install httpd

<h3 id="apache-rewrites">Enabling Apache Rewrites</h3>

1.	Open <code>httpd.conf</code> for editing.

	<pre>vim /etc/httpd/conf/httpd.conf</pre>

2.	Locate the block that starts with:

	<pre>&lt;Directory /var/www/html></pre>

3.	In that block, change the value of `AllowOverride` to one of the values documented on the <a href="http://httpd.apache.org/docs/2.2/mod/core.html#allowoverride" target="_blank">Apache site</a>.

4.	Save your changes to <code>httpd.conf</code> and exit the text editor.

5.	Restart Apache.

	<pre>service httpd restart</pre>

Continue with the next prerequisite (<a href="{{ site.gdeurl }}install-gde/prereq/php-centos.html">PHP CentOS</a>), or start your installation by going to <a href="{{ site.gdeurl }}install-gde/install/composer-clone.html">Install Composer and clone the Magento repository</a>.


#### Related topics:

*	<a href="{{ site.gdeurl }}install-gde/prereq/php-ubuntu.html">PHP 5.5 or 5.6&mdash;Ubuntu</a>
*	<a href="{{ site.gdeurl }}install-gde/prereq/php-centos.html">PHP 5.5 or 5.6&mdash;CentOS</a>
*	<a href="{{ site.gdeurl }}install-gde/prereq/mysql.html">Installing and configuring MySQL</a>
*	<a href="{{ site.gdeurl }}install-gde/prereq/security.html">Configuring security options</a>
*	<a href="{{ site.gdeurl }}install-gde/prereq/optional.html">Installing optional software</a>
*	<a href="{{ site.gdeurl }}install-gde/install/composer-clone.html">Install Composer and Clone the Magento repository</a>
*	<a href="{{ site.gdeurl }}install-gde/install/prepare-install.html">Update installation dependencies</a>
