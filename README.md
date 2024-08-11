## prereqs:

#### The mail machine:

* An Ubuntu 20.04 server configured with a Fully Qualified Domain Name (FQDN).
* A non-root user with sudo privileges.

#### Worker:

* has ansible installed
* community.general module is installed. If doesn't:
  `ansible-galaxy collection install community.general`
* `ansible-galaxy  collection  install  community.mysql**`

## Variables

* domain - your domain
* password - password for mailbox collector_name@domain
* email - your email for certbot
* collector_name - the username part of email, you want to recieve all the mails

## Troubleshooting

If you facing problems with permissions, be sure that user you chose has sudo permissions.
If it doesn't help, try to allow this user to use sudo without password.

## Contribution

There is no spam filter yet
