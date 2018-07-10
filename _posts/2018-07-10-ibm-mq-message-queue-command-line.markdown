---
layout: post
title: IBM MQ (Message Queue) command-line
modified:
categories: 
excerpt: command-line IBM MQ 
tags: []
image:
  feature:
date: 2018-07-10T10:05:18+07:00
---

# IBM MQ command-line

## Queue Manager
### create queue manager
```sh
$ cd /apps/ibm/mqm/900/bin/
$ ./crtmqm --queue-manager-name--
```
### Start queue manager
```sh
$ cd /apps/ibm/mqm/900/bin/
$ ./strmqsc --queue-manager-name--
```

### Run MQSC
```sh
$ cd /apps/ibm/mqm/900/bin/
$ ./runmqsc --queue-manager-name--
```

### Stop queue manager
```sh
$ cd /apps/ibm/mqm/900/bin/
$ ./endmqm --queue-manager-name--
```

### Delete queue manager
```sh
$ cd /apps/ibm/mqm/900/bin/
$ ./dltmqm --queue-manager-name--
```

# Local Queue
### Run MQSC
```sh
$ cd /apps/ibm/mqm/900/bin/
$ ./runmqsc QM_JENIUS_DEV

# Create local queue
DEFINE QLOCAL ('--local-queue-name--')
 
# Display queue
DISPLAY QUEUE ('--local-queue-name--')
 
# Clear data in local queue
CLEAR QLOCAL ('--local-queue-name--')
 
# Delete local queue
DELETE QLOCAL ('--local-queue-name--')
 
# Exit MQSC
END
```

# Topic

### Run MQSC
```sh
$ cd /apps/ibm/mqm/900/bin/
$ ./runmqsc QM_JENIUS_DEV
 
# Create topic
DEFINE TOPIC('--topic-name--') TOPICSTR('--topic-string--')
 
# Example
DEFINE TOPIC('TP.TRANSFER.RQ') TOPICSTR('TP.TRANSFER.RQ')
 
# Display topic
DISPLAY TOPIC('--topic-name--')
 
# Delete topic
DELETE TOPIC('--topic-name--')
 
# Exit MQSC
END
```

# Queue Alias
### Run MQSC
```sh
$ cd /apps/ibm/mqm/900/bin/
$ ./runmqsc QM_JENIUS_DEV
 
# Create queue alias
DEFINE QALIAS('--queue-alias-name--') TARGET('--queue-or-topic-name--') TARGTYPE (--target-type--)
 
# Example create queue alias with target type queue
DEFINE QALIAS('QA.TRANSFER.RQ') TARGET('QL.TRANSFER.RQ') TARGTYPE (QUEUE)
 
# Example create queue alias with target type topic
DEFINE QALIAS('QA.TRANSFER.RQ') TARGET('TP.TRANSFER.RQ') TARGTYPE (TOPIC)
 
# Display queue
DISPLAY QUEUE ('--queue-alias-name--')
 
# Delete queue alias
DELETE QALIAS ('--queue-alias-name--')
 
# Exit MQSC
END
```
# Transmission Queue
### Run MQSC
```sh
$ cd /apps/ibm/mqm/900/bin/
$ ./runmqsc QM_JENIUS_DEV
 
# Create transmission queue
DEFINE QLOCAL('--transmission-queue-name--') USAGE (XMITQ)
 
# Example
DEFINE QLOCAL('QT.TRANSFER’) USAGE (XMITQ)
 
# Display queue
DISPLAY QUEUE('--transmission-queue-name--')
 
# Delete transmission queue
DELETE QLOCAL('--transmission-queue-name--')
 
# Exit MQSC
END
```

# Queue Remote
### Run MQSC
```sh
$ cd /apps/ibm/mqm/900/bin/
$ ./runmqsc QM_JENIUS_DEV
 
# Create remote queue
DEFINE QREMOTE('--queue-remote-name--') RQMNAME('--remote-queue-manager-name--') RNAME('--remote-name--') XMITQ('--transmission-queue-name--')
 
# Example
DEFINE QREMOTE('QR.TRANSFER.RQ') RQMNAME('QM_MS_DEV') RNAME('QL.TRANSFER.MS.RQ') XMITQ('QT.TRANSFER.MS')
 
# Display queue
DISPLAY QUEUE('--queue-remote-name--')
 
# Delete remote queue
DELETE QREMOTE('--queue-remote-name--')
 
# Exit MQSC
END
```

# Channel
### Run MQSC
```sh
$ cd /apps/ibm/mqm/900/bin/
$ ./runmqsc QM_JENIUS_DEV
 
# Create channel server conn
DEFINE CHANNEL('--channel-name--') CHLTYPE(--channel-type--) TRPTYPE(--trp-type--) HBINT(60)
 
# Example
DEFINE CHANNEL('CH.MDW.SVRCONN') CHLTYPE(SVRCONN) TRPTYPE(TCP) HBINT(60)
 
# Create channel sender
DEFINE CHANNEL('--channel-name--') CHLTYPE(--channel-type--) TRPTYPE(--trp-type--) HBINT(60) DISCINT(0) CONNAME('--ip(port)--') XMITQ('--transmission-queue-name--')
 
# Example
DEFINE CHANNEL('CH.APIGW.RS') CHLTYPE(SDR) TRPTYPE(TCP) HBINT(60) DISCINT(0) CONNAME('10.1.83.186(2149)') XMITQ('QT.TRANSFER.MS')
 
# Create channel receiver
DEFINE CHANNEL('--channel-name--')  CHLTYPE(--channel-type--)  TRPTYPE(--trp-type--) HBINT(60)
 
# Example
DEFINE CHANNEL('CH.MQ.RS') CHLTYPE(RCVR) TRPTYPE(TCP) HBINT(60)
 
# Delete channel
Delete channel('--channel-name--')
 
# Exit MQSC
END
```

# AMQP Channel
### Run MQSC
```sh
$ cd /apps/ibm/mqm/900/bin/
$ ./runmqsc QM_JENIUS_DEV
 
# Change service become part of MQ
ALTER SERVICE('SYSTEM.AMQP.SERVICE') CONTROL(QMGR)
 
# Start service AMQP
START SERVICE('SYSTEM.AMQP.SERVICE')
 
# Change channel AMQP port
ALTER CHANNEL('SYSTEM.DEF.AMQP') CHLTYPE(AMQP) PORT(1234)
 
# Start channel AMQP
START CHANNEL('SYSTEM.DEF.AMQP')
 
# Display AMQP port
DISPLAY CHANNEL(SYSTEM.DEF.AMQP) CHLTYPE(AMQP)
 
# Exit MQSC
END
```

# Listener
### Run MQSC
```sh
$ cd /apps/ibm/mqm/900/bin/
$ ./runmqsc QM_JENIUS_DEV
 
# Create port TCP listener
DEFINE LISTENER('--listener-name--') TRPTYPE(--type--) PORT(--port--)
 
# Example
DEFINE LISTENER('TCP.LS.APIGW') TRPTYPE(TCP) PORT(2149)
 
# Start port TCP listener
START LISTENER('--listener-name--')
 
# Stop port TCP listener
STOP LISTENER('--listener-name--')
 
# Delete port TCP listener
DELETE LISTENER('--listener-name--')
 
# Exit MQSC
END
```


# Authentication
### Run MQSC
```sh
$ cd /apps/ibm/mqm/900/bin/
$ ./runmqsc QM_JENIUS_DEV
 
# Set auth user for queue manager
SET AUTHREC PROFILE('QM_JENIUS_DEV') GROUP('--username--') OBJTYPE(QMGR) AUTHADD(ALL)
 
# Set auth user for queue
SET AUTHREC PROFILE('QL.TEST.ECHO.RQ') GROUP('--username--') OBJTYPE(QUEUE) AUTHADD(ALL)
 
# Set auth user for channel
SET AUTHREC PROFILE('CH.APIGW.SVRCONN') GROUP('--username--') OBJTYPE(CHANNEL) AUTHADD(ALL)
 
# Set auth hostaname for channel
SET CHLAUTH('CH.APIGW.SVRCONN') TYPE(ADDRESSMAP) ADDRESS('*') USERSRC(CHANNEL) CHCKCLNT(REQUIRED)
 
# Set auth AMQP
SET CHLAUTH('SYSTEM.DEF.AMQP') TYPE(BLOCKUSER) USERLIST('nobody') DESCR('Allow privileged users on this channel')
 
# Set auth hostaname for AMQP
SET CHLAUTH('SYSTEM.DEF.AMQP') TYPE(ADDRESSMAP) ADDRESS(*) USERSRC(CHANNEL) CHCKCLNT(REQUIRED)
 
# Set auth user for AMQP service
SET AUTHREC PROFILE('SYSTEM.AMQP.SERVICE') USER(--username--) OBJTYPE(SERVICE) AUTHADD(ALL)
 
# Set auth user for AMQP channel
SET AUTHREC PROFILE('SYSTEM.DEF.AMQP') GROUP(--username--) OBJTYPE(CHANNEL) AUTHADD(ALL)
 
# Refresh securiry type
REFRESH SECURITY TYPE(CONNAUTH)
 
# Exit MQSC
END
```

# High Availability
### Run MQSC
```sh
$ cd /apps/ibm/mqm/900/bin/
$ ./runmqsc QM_JENIUS_DEV
 
# Move to bin directory
$ cd /apps/ibm/mqm/900/bin/
 
# Create QM in active server
$ ./crtmqm -u SYSTEM.DEAD.LETTER.QUEUE -lf 16384 -x 10000 -md /shared/[env]/mqha/data -ld /shared/[env]/mqha/log -lp 30 -ls 15 -lc -t 60000 QM_[NAME]_[ENV]
 
# Display QM Information in active server
$ ./dspmqinf -o command QM_[NAME]_[ENV]
 
# Add QM information to stand by server
$ ./addmqinf -s QueueManager -v Name=QM_[NAME]_[ENV] -v Directory=QM_HA_TST -v Prefix=/var/mqm -v DataPath=/shared/[env]/mqha/data/QM_[NAME]_[ENV]
 
# Start the QM in active server first then follow at standby server
$ ./strmqm -x QM_[NAME]_[ENV]
 
# Exit MQSC
END
```
