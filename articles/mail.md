## Setup email client for development purpose on ubuntu.

My setup involves two parties:

 - postfix
 - mailtrap
 
Postfix is a [mail transfer agent](https://en.wikipedia.org/wiki/Message_transfer_agent)(mta) that recieves mails
from either another MTA or from a [mail client](https://en.wikipedia.org/wiki/Email_client).

The transmission details are specified by the SMTP protocol. When a
recipient mailbox of a message is not hosted locally(eg. if I'm sending an email from localhost to gmail.com),the message is relayed, that is, forwarded to another MTA(which is going to be mailtrap in our case).

postfix only sends emails but does not store them in a mailbox(AFAIK), so I can't read the emails. That is why I'm relaying the messages to mailtrap.
Mailtrap in the other hand, has a mailserver and "traps" the email for visualization, not attempting to deliver it to the final receipient.

### Setup postfix
- disable whatever mailservice you might have running. eg.

        sudo service sendmail stop
        
- install postfix

        sudo apt-get install postfix

Configuration for postfix should be prompted automatically, if not, run:

        sudo dpkg-reconfigure postfix
        
During the configuration, the only thing I had to select was to use internet site as the general configuration as in the following image:

![image](https://i.postimg.cc/Wp6mpmqm/Selection-083.png)

The rest I left as it was, a sample of my current config is(I hope I didn't expose anything unsafe here ;) ):

        smtpd_relay_restrictions = permit_mynetworks permit_sasl_authenticated defer_unauth_destination
        myhostname = ux-osvaldo
        alias_maps = hash:/etc/aliases
        alias_database = hash:/etc/aliases
        mydestination = $myhostname, ux-osvaldo, localhost.localdomain, , localhost
        relayhost =
        mynetworks = 127.0.0.0/8 [::ffff:127.0.0.0]/104 [::1]/128
        mailbox_size_limit = 0
        recipient_delimiter = +
        inet_interfaces = all
        inet_protocols = all
        
        
### setup mailtrap

[mailtrap](https://mailtrap.io) which provides a fake smtp server to which you can send emails.
mailtrap also offers a web interface that can be used as a mailclient.

To use it, Create an account and use the given setup instructions.\

### Refferences

- https://en.wikipedia.org/wiki/Postfix_(software)

- https://en.wikipedia.org/wiki/Message_transfer_agent

- https://www.digitalocean.com/community/questions/use-postfix-instead-of-sendmail

- https://ubuntuforums.org/showthread.php?t=1605548

- 
