Record configuration changes over time on resources
All this info is stored regionally in an S3 config bucket

AWS Config is capable of checking for compliance .. and generating notifications and events based on compliance. However, it can't stop you from doing changes

Can generate events with [[Simple Notification Service|SNS]] and events with [[Lambda]]


