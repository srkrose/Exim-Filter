# Exim-Filter
Exim MTA custom filter rules for WHM cPanel

## Overview

Exim-Filter enhances mail processing in WHM cPanel environments with custom rules, ensuring outgoing mail security. Deployed in `/usr/local/cpanel/etc/exim/sysfilter/options/`, these rules address various scenarios. If specific conditions are met, the script returns the mail to the authenticated user/sender with a modified subject containing the reason for the failure, thus ensuring proper SMTP configuration and rejecting potential issues.

## Features

### Outgoing Mail Verification Methods:

- Presence of an authenticated ID.
- Sender's IP address is equal to localhost (127.0.0.1).
- Presence of SMTP server hostname in the header From address.

### Accepted Mails:

- Mails from the `root` user.
- Mails with the local part `cpanel` in the sender's address.
- Mails with a subject starting with `<SELECTED PHRASE>`.
- Mails with the header From including the SMTP server hostname.

### Discarded Mails:

- Mails if the recipient count exceeds `90`.
- Mails with the authenticated ID not matching the sender's address.
- Mails with the authenticated ID not included in the From address.
- Mails with the authenticated ID that is not a valid email address.

## Implementation

1. Create a file in `/usr/local/cpanel/etc/exim/sysfilter/options` directory and copy the code
2. Customize rules based on your requirements
3. Navigate to WHM >> Exim Configuration Manager >> Filters
4. Scroll down and enable the custom filter by ticking `On` for `Custom Filter: CREATED_FILE_NAME`
5. Click `Save` to apply the configuration, triggering a restart of the Exim Mail Server

### Reference

- https://www.exim.org/exim-html-current/doc/html/spec_html/filter_ch-exim_filter_files.html
- https://support.cpanel.net/hc/en-us/articles/1500006376621-How-to-use-Exim-filters-to-limit-a-domain-so-that-it-cannot-send-to-or-receive-from-any-external-domains-Internal-Only-Mail
