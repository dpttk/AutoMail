# AutoMail

A complete mail server solution using Postfix, Dovecot, and Roundcube webmail, deployed with Ansible.

## Why do you need to host your own mail server? 

Well, it gives you an infinite number of valid email addresses ending with @yourdomain. And I see many benefits in it

### Anti-leak
If you register on services with unique emails, it would be hard to match your data between the data leaks

### Trial period abuse
Some services ask only for email confirmation to register and get a trial period. With your own server, a new email is already there

### It's cool 
I mean, the email mr@dpttk.ru looks much better than jH0n-wH1cKKK1320-0@gmail.com

### It's convenient 
I would suggest connecting your mail server to your current email service provider. All major providers support adding third-party email servers to your mailbox. And so, you will have an infinite number of addresses plus your good old current email from one page. Awesome! 


## Prerequisites

### The Mail Server:

* Ubuntu 20.04 server configured with a Fully Qualified Domain Name (FQDN)
* A non-root user with sudo privileges
* Domain name with proper DNS records (A, MX, and optionally SPF, DKIM, DMARC)

### Control Machine:

* Ansible installed (version 2.9 or higher)
* Required Ansible collections:
  * `ansible-galaxy collection install community.general`
  * `ansible-galaxy collection install community.mysql`

## Installation

1. Clone this repository:
   ```
   git clone https://github.com/yourusername/AutoMail.git
   cd AutoMail
   ```

2. Update the inventory file with your server information:
   ```
   nano inventory/hosts.ini
   ```

3. Configure variables for your environment:
   ```
   nano group_vars/all.yaml
   nano group_vars/vault.yaml
   ansible-vault encrypt group_vars/vault.yaml
   ```

4. Run the playbook:
   ```
   ansible-playbook -i inventory/hosts.ini site.yaml --ask-vault-pass
   ```

## Configuration

The main configuration variables are stored in `group_vars/all.yaml`:

* `domain`: Your domain name
* `email`: Email for Let's Encrypt certificate
* `collector_name`: The username receiving all mail
* `mail_password`: Password for the mailbox
* `mariadb_password`: MariaDB root password (if using MariaDB instead of SQLite)
* `roundcube_db_password`: Roundcube database password

## Usage

After installation:

1. Access webmail at `https://your-domain/roundcube`
2. Configure mail clients using IMAP/SMTP with your domain credentials
3. All emails to the domain will be collected in the specified collector mailbox

## Troubleshooting

* Check mail logs: `tail -f /var/log/mail.log`
* Verify Postfix configuration: `postfix check`
* Test Dovecot with: `telnet localhost 143` (IMAP) or `telnet localhost 110` (POP3)
* Examine Apache logs: `tail -f /var/log/apache2/error.log`

## Security

* All passwords should be changed from defaults
* Use Ansible Vault for sensitive information


## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the WTFPL
