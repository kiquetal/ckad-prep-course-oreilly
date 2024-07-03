### Creating a job

1 - Create a Job named random-hash. that executes the shell command echo $RANDOM | base64 | head -c 20. Configure the Job to execute with two pods in paralle.
The number of complpetions should be set to five.

2 - Identify the Pods that executed the shell command. How many Podws do expect to exist? 

3 - Retrieve the generated hash from one of the Pods.

4 - Delete the job. Will the corresponding pods continue to exist?
