# ApacheCassandra


I Used Apache Cassandra Installation from Debian packages.

How to intsall it from from Debian packages ?
- ```` echo "deb https://downloads.apache.org/cassandra/debian 40x main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list ````
- Add the Apache Cassandra repository keys 
  - ```` curl https://downloads.apache.org/cassandra/KEYS | sudo apt-key add - ```` 
- Update the repositories
  - ```` sudo apt-get update ```` 
 
- Then add the public key A278B781FE4B2BDA as follows
  - ```` sudo apt-key adv --keyserver pool.sks-keyservers.net --recv-key A278B781FE4B2BDA ````  
 
- Install Cassandra
  - ```` sudo apt-get install cassandra ```` 


You can start Cassandra with ```` sudo service cassandra start ```` and stop it with ```` sudo service cassandra stop ````

Verify that Cassandra is running by invoking ```` nodetool status ```` from the command line

To connected to cluster use ```` cqlsh ````

- [Download reference](https://cassandra.apache.org/_/download.html)
- [CQL reference](https://docs.datastax.com/en/archived/cql/3.1/cql/cql_reference/cqlReferenceTOC.html)

