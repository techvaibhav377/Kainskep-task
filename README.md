# CSV Server Setup

Before you begin, ensure that you have Docker installed on your machine.

## Docker Images

Pull the required Docker images using the following commands:

```bash
docker pull infracloudio/csvserver:latest
docker pull prom/prometheus:v2.22.0



##verify Docker images using the following command

docker images

##Create a Bash script named gencsv.sh with the following content:
#!/bin/bash

RANDOM=$$
for i in `seq 10`
do
    echo $((i++)), $RANDOM >> inputdata
done



##Generate input data using the script:
./gencsv.sh


##Verify the generated input data:
1, 4807
2, 5190
3, 20188
4, 10304
5, 13997
6, 30370
7, 19196
8, 3112
9, 15143
10, 8948




##Run the CSV server container using the following command:
docker run -d --name csvserver -e CSVSERVER_BORDER='Orange' -v ${PWD}/inputdata:/csvserver/inputdata -p 9393:9300 infracloudio/csvserver


##Access the CSV server UI at http://localhost:9393 to interact with the CSV server.
