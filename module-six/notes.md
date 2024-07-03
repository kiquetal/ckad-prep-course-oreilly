### JOB and CronJOB


- Pod: continuos operation of an application kept running without interrupts if possible


- Job: runs functionality until a specifcied number of completions has been reached, for a one-time operations

- Cron Job: essentially a job but itś run periodically based on a schedule


#### CronJob

A CronJob is essentislly a Job with similar characterisics

kubectl create cronjob curren-date 
--schedule="* * * * *"
--image=nginx:1.24.0
-- /bin/sh -c 'echo "$curendate"


