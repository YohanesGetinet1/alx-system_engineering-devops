### Issue Summary:
From November 6 12:30 p.m to November 7 9:30 p.m Requests to the website responded with an ERROR 500, this affected 35% of users since the requests corresponded to a query module. The users could not access to the web page and the services associated because the apache server was down. The suspension was due to an incorrect file name in the last update.

### TimeLine 
* November 6
* 12:30 p.m : Code push to server
* 1:30 p.m : Deploy code
* 1:45 p.m : Outage begins
* 1:50 p.m : Masive Customers complaints
* 2:00 p.m : Customer services create a ticket
* 2:10 p.m : The support engineer receive the ticket and start to attend the issue
* 2:30 a.m: Check http requests. Why a 500 error?
* 3:00 a.m : Check the apache server configuration files line by line. sites-available, /etc/apache2/, /var/www/html/.

* November 7
* 8:00 a.m: Check the logs associated (error logs, access logs)
* 10:00 a.m: Use the ps aux comand to detect what process are associated to the apache server. apache2. 
* 10:30 a.m: Use the strace command to the root apache server process with null result for every line. -root 
* 11:00 a.m: Use the strace command to the data apache server process with a long list of return -1 errors. 

### Root cause and Resolution 
The root of the problem was due to an incorrect file name in the last update of the site, specifically in the extension of the updated php module.

Initially it was verified that the files were in the appropriate apache path “sites / available”, with the ps aux command the processes associated with apache were verified, then with the strace command the returns were checked the file was identified, a script was generated to correct the problem, it was validated with the curl command and access from the browser. 

### Corrective and Preventative Measures 
In light of the incident in the last two days, an evaluation and review of the update process carried out was made, it was determined that stages were omitted for the release of this module to production, to prevent future incidents, the following improvements were implemented:

* A QA team was formed that will be in charge of validating and testing changes and updates
* A QA environment was created where pre-production integration tests are carried out
* Github CI/CD services were integrated to deployment updates and code revisions