# Quick Process to install Lets encrypt into any cpanel account. No sudo or root access needed. 

#### Just you need to contact with your hosting provider to enable ssh connection to your cpanel account. Then get back here and follow the steps. 

Login to your account using SSH. Then 

 `curl https://get.acme.sh | sh`
 
`source ~/.bashrc`

`acme.sh --update-account --accountemail youremailaccount@yourdomain.com`

`export DEPLOY_cPanel_USER=cpanelusername`




`
### issue cpanel Lets encrypt SSL certificate 

`acme.sh --force --issue -d domain.com -d www.domain.com -d mail.domain.com  -w ~/public_html`

### For add-on Domain you might have different webroot. Then replace with public_html 

### Cpanel Only use cpanel hook to deploy SSL certificate

`acme.sh --deploy -d domain.com -d www.domain.com -d mail.domain.com --deploy-hook cpanel_uapi`


Setup cpanel cron job

`0 0 1 * * "/home/cpanelusername/.acme.sh"/acme.sh --cron --home "/home/cpanelusername/.acme.sh" > /dev/null `
#### or use this cron. Change run time to every month 

`0 1 1 * * /home/cpanelusername/.acme.sh/acme.sh --force --issue -d domain.com -d www.domain.com -d mail.domain.com  -w /home/cpanelusername/public_html`

`0 2 1 * * /home/cpanelusername/.acme.sh/acme.sh --deploy -d domain.com -d www.domain.com -d mail.domain.com --deploy-hook cpanel_uapi`

This cron will be run in every 1 months. 

Hope this will help you to understand. if you see any issue. Comment here. I will try to help you for free. :) 
