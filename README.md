#mooshak-judge

Online Judging Platform for Coding Assignments

##Tentative Roadmap

1. Figure out how Mooshak works
2. Make front-end changes/modifications to the default Mooshak templates
3. Add following features:
	* Add Class (add all enrolled students to contest)
	* Partial Marking (for passing some test cases)
	* Add Question Bank (tentative)

##Proposed Technologies

1. Backend - 
2. Frontend - 

##How to install Mooshak

###For Ubuntu/similar Linux systems

1. Requirements
```
sudo apt-get update
sudo apt-get install apache2 tcl libxml2-utils xsltproc apache2-suexec-custom

sudo a2enmod userdir
sudo a2enmod suexec 
```

2. Edit the file `apache2.conf` by doing
`sudo gedit /etc/apache2/apache2.conf`
add the following in the end of the file and click save.
`servername localhost`

3. Download Mooshak from [here](https://mooshak.dcc.fc.up.pt/download/mooshak-1.6.2.tgz)

4. Open a terminal and copy the following lines
```
cd ~/Downloads/mooshak-1.6.2
sudo ./install
```

5. Edit the www-data file using `sudo gedit /etc/apache2/suexec/www-data` and delete all the contents inside the file and add the following lines in it. Save and close the file.
```
/home/mooshak
/home/mooshak
```

6. Now run the following commands to create links. Execute them one by one.
```
cd /etc/apache2/mods-enabled
sudo ln -s ../mods-available/userdir.conf
sudo ln -s ../mods-available/userdir.load
sudo ln -s ../mods-available/suexec.load
```

7. Now open the file default in sites-available directory using `sudo gedit /etc/apache2/sites-available/default`
if you're going to use the system in which you're installing mooshak as a dedicated machine for only mooshak, then clear all the contents in the file default and add the following lines:
```
<VirtualHost *:80>
	DocumentRoot /home/mooshak/public_html
	SuexecUserGroup mooshak mooshak
	<Directory /home/*/public_html/cgi-bin>
	 	Options +ExecCGI -Includes -Indexes
		SetHandler cgi-script
	</Directory>
</VirtualHost>
```
save and close it.

Or 
if you wish to use the machine for two different servers or applications, then append the lines to the file default without clearing its contents.besides, edit the file ports.conf using `sudo gedit /etc/apache2/ports.conf` and add the following lines in it
```
NameVirtualHost *:8080
Listen 8080
```

8. Edit the file alias.conf using `sudo gedit /etc/apache2/mods-available/alias.conf` and replace the following line 
`Alias /icons/ "/usr/share/apache2/icons/"` with `Alias /icon/ "/usr/share/apache2/icons/"`

8.5 enter the following commands on your terminal
```
sudo adduser mooshak www-data
sudo chown -R www-data:www-data /home/mooshak/public_html
sudo chmod -R 755 /home/mooshak/public_html
```

open `sudo gedit /etc/apache2/apache2.conf` and add the following lines
```
<Directory /home/mooshak/public_html/>
	Options Indexes FollowSymLinks Includes ExecCGI
	AllowOverride None
	Require all granted
</Directory>

<Directory /home/mooshak/public_html/cgi-bin>
	Options +ExecCGI -Includes -Indexes
	SetHandler cgi-script
	Require all granted
</Directory>
```

9.  Finally restart the apache2 server to start the server with the modified configurations.
```
sudo /etc/init.d/apache2 restart
```

10. now go to `127.0.0.1/~mooshak` or `localhost/~mooshak` or machine ip address to get login page of the mooshak you've just installed.
default username's and passwords are
```
username: admin
password: admin

username: judge
password: judge

username: team
password: team
```
You can get the same page in browser of another machine connected through intranet by using the ip address of the machine you've installed mooshak in. Now you have just created a server to conduct programming contests using c, c++, java, pascal based on icpc environment.


##Contribute

0. Learn about HTML, CSS, JavaScript (W3Schools might be a good starting point)

1. Install Mooshak on your system (steps given above)
2. Understand how the platform works
3. Templates (HTML files) located in - `/home/mooshak/templates`
4. Styles(CSS stylesheets) located in - `/home/mooshak/public_html/styles`
(Will update soon)
