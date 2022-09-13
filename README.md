# Load-Balancer-Solution-With-Nginx-and-SSL-TLS

## CONFIGURE NGINX AS A LOAD BALANCER

Created an EC2 VM based on Ubuntu Server 20.04 LTS and named it Nginx-lb

![mamar](https://user-images.githubusercontent.com/94229949/189984548-7b9eef1e-01e6-4ee1-9ff9-bfa4dd705040.png)

Updated the instance and Installed Nginx using these commands 'sudo apt update ' and 'sudo apt install nginx '

![mama1](https://user-images.githubusercontent.com/94229949/189985323-5aba51ab-4d54-4141-8bf3-ad9dc60c7eb4.png)

![mama2](https://user-images.githubusercontent.com/94229949/189985372-3c29fd00-4d19-4f5e-9605-2c8cc11912e3.png)

Updated /etc/hosts file for local DNS with Web Servers’ names ( Web1 and Web2) and their local IP addresses

![mama3](https://user-images.githubusercontent.com/94229949/189985209-dd1937f1-4620-496e-ab74-00de333fe001.png)

Opened the default nginx configuration file using ' sudo vi /etc/nginx/nginx.conf ' and inserted the following configuration into the  http section

![mama7](https://user-images.githubusercontent.com/94229949/189986177-a853f31e-541d-42ff-b98f-a8b182813751.png)

Then comment out this line with an hashtag  in ' include /etc/nginx/sites-enabled/*; '

Restarted Nginx and made sure the service is up and running using 'sudo systemctl restart nginx '  and 'sudo systemctl status nginx '

![mamad](https://user-images.githubusercontent.com/94229949/189987436-3686a052-1941-4f46-93c8-b2be66014f79.png)

Registered a new domain name on AWS and created an A record for ' busolagbadero.click' and  ' www.busolagbadero.click 

![mamaf](https://user-images.githubusercontent.com/94229949/189988672-3a5d231c-fc00-482a-9105-80526c08b72c.png)

Checked if the Web Servers can be reached from the browser using new domain name using HTTP protocol 

![mama6](https://user-images.githubusercontent.com/94229949/189989514-45603b76-43e4-443a-bd15-3981cc544855.png)


To request for an SSL/TLS certificate ,i installed certbot . I checked if snapd service is active and running using command  ' sudo systemctl status snapd ' and then Installed certbot using  ' sudo snap install --classic certbot '

![mama8](https://user-images.githubusercontent.com/94229949/189991596-7769c484-ab13-48c2-ac93-823b3a1edb3a.png)

Also ran these commands  ' sudo ln -s /snap/bin/certbot /usr/bin/certbot ' and 'sudo certbot --nginx ' and followed the certbot instructions

![mama9](https://user-images.githubusercontent.com/94229949/189992706-5e0f1ba1-ff08-4f37-a475-11d69d720f73.png)

Checked to see if the website is now secure 

![mama10](https://user-images.githubusercontent.com/94229949/189993622-b984a632-1d7c-4691-b72b-cdb91596ce9e.png)

To Set up periodical renewal of  SSL/TLS certificate ,i ran a test renewal command in dry-run mode using ' sudo certbot renew --dry-run '

![mamao](https://user-images.githubusercontent.com/94229949/189996392-efa14738-096e-4463-858c-cfe01250a463.png)


configured a cronjob to run the command twice a day. Edited the crontab file with the following command: crontab -e and added the  following line: * */12 * * *   root /usr/bin/certbot renew > /dev/null 2>&1

![mama11](https://user-images.githubusercontent.com/94229949/189996837-1fc3983a-2cb3-4f94-8e4f-b272c577e8b3.png)


![mama12](https://user-images.githubusercontent.com/94229949/189996634-7f04250b-91b6-42f3-ae9b-52b0b511a6c7.png)


 I successfully implemented Nginx Load Balancing Web Solution with secured HTTPS connection with periodically updated SSL/TLS certificates.








