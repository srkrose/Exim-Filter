# Exim-Filter
Exim MTA custom filter rules for WHM cPanel

## Overview

Exim-Filter enhances mail processing in WHM cPanel environments with custom rules, ensuring outgoing mail security. Deployed in `/usr/local/cpanel/etc/exim/sysfilter/options/`, these rules address various scenarios. If specific conditions are met, the script returns the mail to the authenticated user/sender with a modified subject containing the reason for the failure, thus ensuring proper SMTP configuration and rejecting potential issues.

## Features

### 1. Different Authenticated Mail Check

- Verify outgoing mails by checking the presence of an authenticated ID
- Exclude checks for mails from the `root` user
- Exclude checks for mails with the local part `cpanel` in the sender's address
- Allow mails with the authenticated ID matching the sender's address
- Allow mails with a subject starting with `Cron <$sender_ident@`

### 2. Recipient Count Check

- Verify outgoing mails by checking the presence of an authenticated ID
- Discard mails if the recipient count exceeds 90

### 3. Root Mail Check

- Verify outgoing mails using the SMTP server hostname by checking the header From address
- Exclude checks for mails from the `root` user
- Exclude checks for mails with the local part `cpanel` in the sender's address
- Allow mails if the recipient is the same as the sender for internal server communication
- Allow mails with a subject starting with `Cron <$sender_ident@`

### 4. Unauthenticated Mail Check

- Verify outgoing unauthenticated mails by checking the sender's IP address against localhost (127.0.0.1)
- Exclude check mails where the header From includes the SMTP server hostname
- Allow mails with the authenticated ID matching the sender's address

## Implementation

1. Create a file in `/usr/local/cpanel/etc/exim/sysfilter/options` directory and copy the code
2. Customize rules based on your requirements
3. Navigate to WHM >> Exim Configuration Manager >> Filters
4. Scroll down and enable the custom filter by ticking `On` for `Custom Filter: CREATED_FILE_NAME`
5. Click `Save` to apply the configuration, triggering a restart of the Exim Mail Server

### Reference

- https://www.exim.org/exim-html-current/doc/html/spec_html/filter_ch-exim_filter_files.html
- https://support.cpanel.net/hc/en-us/articles/1500006376621-How-to-use-Exim-filters-to-limit-a-domain-so-that-it-cannot-send-to-or-receive-from-any-external-domains-Internal-Only-Mail
