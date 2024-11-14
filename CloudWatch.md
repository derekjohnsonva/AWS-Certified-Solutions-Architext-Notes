Collects and manages operation data - some examples of this are view counts and site visitors

Some things will need the cloudwatch agent in order to log data

Stores...
* metrics - time ordered set of data points. Each data point consists of a timestamp and a value
* logs - 
* event - 
![[Pasted image 20240910194734.png || 400]]

There is a lot of different data that is going to be in CloudWatch. In order to get around this, we will use *Namespaces*
*Namespaces* are like container for data in CloudWatch (related metrics)

## CloudWatch Logs
Public service - usable from AWS or on-prem
Allows you to store, monitor, and access logging data
A log is normally a timestamp and some data
CloudWatch integrates with lost of other services
To use it with data not coming from AWS, use the Unified CloudWatch Agent (or AWS devkits)
Can be used to generate metrics based on logs

Log events = individual logs
Log stream = log events coming from a source
Log groups = a group of log streams. This is also where we store our data settings. Also where we define our metric filters.
![[Pasted image 20240916120421.png | 400]]

## CloudWatch Events
The functionality of CloudWatch Events will be covered by EventBridge
Let you watch perform the following actions
	If X happens do Z
	At Y time do Z
An event bus is the place where events are stored before being processed

