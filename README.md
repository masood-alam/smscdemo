Orchastrates three Docker instances
1. ubuntu-jboss-smsc ( smsc gateway)
2. ubuntu-jboss-hlr  (network services)
3. cassandra:2.2.13  (smsc gateway database storage)

Git clone the smscgateway (ubuntu-jboss-smsc) and network services (ubuntu-jboss-hlr)
Git clone the smscgateway and network services docker repository and build the docker.

How to Run:


1. Create instances of the all three dockers
	~$ docker-compose up
   If smsc does not up with services then do this:
Press ctrl-C ^C to end the process.
2. Start the instances again
	~$ docker-compose start
3. Stop the smsc docker
   Because smsc will fail due to slow start of cassandra, we stop it now
	$ docker stop smscdemo_smsc_1
4. we check cassandra is ready
	$ docker logs smscdemo_cassandra_1 -f

5. When cassanra docker is ready, we create the key space
	$ docker exec -it smscdemo_cassandra_1 cqlsh 172.18.0.10
   when cqlsh prompt appears

cqlsh>CREATE KEYSPACE "RestCommSMSC" WITH REPLICATION = {'class' : 'SimpleStrategy', 'replication_factor': 1};

cqlsh>exit

6. Now we can start smsc docker
	$ docker start smscdemo_smsc_1


