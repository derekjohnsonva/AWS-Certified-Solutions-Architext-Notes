Guard Duty is an automatic threat detection service which reviews data from supported services and attempts to identify any events outside of the 'norm' for a given AWS account or Accounts.

It is a continuous security monitoring service that constantly reviews certain Data Sources using ML for threats

GuardDuty will learn what type of activity is normal and will flag things that are not in that pattern

If it finds something (Finding) then it will notify someone ([[Simple Notification Service|SNS]]) or perform some sort of event ([[Lambda]])

You can have a **Master** account that manages GuardDuty and **Member** accounts that get secured 
