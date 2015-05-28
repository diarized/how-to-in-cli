class: center, middle, inverse

# The terminal

---

# Why
* no distraction

???

General discussion about the history, simplicity, low-bandwith, low-resources features of terminal aka command line.

---

# Why
* .grey[no distraction]
* mouseless (keyboard only)

---

# Why
* .grey[no distraction]
* .grey[mouseless (keyboard only)]
* no resource hungry

---

# Why
* .grey[no distraction]
* .grey[mouseless (keyboard only)]
* .grey[no resource hungry]
* often implemented (even in Windows)

---

# Basic tools

## SSH
* new telnet (the idea of work on central shared systems)
* key-agent (removing authentication with password, but if  you trust source wks)

---

# Basic tools

## Tmux
* many parallel sesions
* splitting the screen
* screen sharing
* simultaneous sessions to many servers

---

# Everyday tasks

* Mail
* Chat
* Task management

---

class: center, middle, inverse

# Mail

---

class: center, middle, inverse

# Where

---

# Reading on IMAP

???

How to use Mutt to read remote inbox on Gmail server 

---

# Reading on IMAP

```
  1 source $HOME/.muttrc_common
  2 
  3 set folder = imaps://imap.gmail.com:993/
  4 set spoolfile = +INBOX
  5 set record = "+[Gmail]/Sent Mail"
  6 set postponed = "+[Gmail]/Drafts"
  7 set mbox = "+[Gmail]/All Mail"
  8 
  9 mailboxes = 'INBOX' \
 10             '=[Gmail]/Sent Mail'
 11 
 12 set smtp_url="smtp://artur@stonith.pl@smtp.gmail.com:587/"
 13 set smtp_pass = `pass show stonith`
 14 
 15 set imap_user = 'artur@stonith.pl'
 16 set imap_pass = $smtp_pass
```

---

# Password storage

* [Password-store](http://git.zx2c4.com/password-store/about/)

---

# Password storage

* .grey[Password-store]
* Combined with Pretty GNU Privacy (PGP key infrastructure + key agent)

---

# Password storage

* .grey[Password-store]
* .grey[Combined with Pretty GNU Privacy (PGP key infrastructure + key agent)]

More on PGP key agents on next slides.

---

# Source of e-mails

## Mail gathering
* Local delivery (postfix/exim server)

???

Home server, VPS. Geeks keep mail on many different systems far from Gmail/Yahoo.

---

# Source of e-mails

## Mail gathering
* .grey[Local delivery (postfix/exim server)]
* Transfering and performing other commands over IMAP(rotocol)

---

class: center, middle, inverse

# Filtering/sorting

---

# Filtering/sorting

* Procmail filters and sorts into folders with local delivery

---

# ~/.procmailrc


```
  7 LOGFILE=$MAILDIR/procmail.log
  8 VERBOSE=yes
  9 DELIVER="/usr/lib/dovecot/deliver"
 10 
 11 :0cD
 12 * ^Subject: remi
 13 | $HOME/src/reminder_client.py
 14 
 15 :0c
 16 | $HOME/local/bin/notmuch new
 17 
 18 :0w
 19 * ^X-Spam-Status: Yes
 20 | $DELIVER -m .Spam/
 21 
 22 :0
 23 * ^From.*@funfile.org
 24 .mdir-funfile/
```

---

# Procmail logs

```
procmail: [23198] Fri May 29 01:16:15 2015
procmail: No match on "^Subject: remi"
procmail: Assigning "LASTFOLDER=/home/artur/local/bin/notmuch new"
procmail: No match on "^X-Spam-Status: Yes"
procmail: No match on "^From.*@funfile.org"
procmail: No match on "^(From|To|Cc).*pgsql-hackers@postgresql.org"
procmail: No match on "^(From|To|Cc).*pgsql-announce@postgresql.org"
procmail: No match on "^(From|To|Cc).*pgsql-performance@postgresql.org"
procmail: Match on "^(From|To|Cc).*python-dev@python.org"
procmail: Executing "/home/artur/local/bin/notmuch,new"
procmail: [23198] Fri May 29 01:16:16 2015
procmail: Assigning "LASTFOLDER=.mdir-python-dev/new/1432854975.23198_0.monitor"
```

---

# Filtering/sorting

* .grey[Procmail filters and sorts into folders with local delivery]
* IMAPfilter filter and sorts e-mails on remote system using IMAProtocol

---

# Download

* OfflineIMAP