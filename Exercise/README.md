Installing and using keyspace, column families and sets with Cassandra.

1. Create a Keyspace called test with a replication factor 1 and simple strategy
   - ```` CREATE KEYSPACE test with REPLICATION = {'class' : 'SimpleStrategy', 'replication_factor': 1};  ```` 

 
 2. Go to the keyspace test
    - ```` Use test; ````

 
 
 3. Create a column family (table) called person with id text, email text, name text, surname text and id as primary key
    - ```` CREATE TABLE person ( id text, email text, name text, surname text, PRIMARY KEY (id) ); ````



4. check the schema of the column family person
    - ```` DESCRIBE person; ````

5. Populate person column family
    - ```` INSERT INTO person (id, name, surname, email) VALUES ('002', 'John', 'Doe', 'john@example.com'); ````
    - ```` INSERT INTO person (id, name, surname, email) VALUES ('003', 'Harry', 'Potter', 'harry@example.com'); ````
    - ```` INSERT INTO person (id, name, surname, email) VALUES ('001', 'Shalabh', 'Aggarwal', 'contact@shalabhaggarwal.com'); ````


6. Get all information from person 
    - ```` SELECT * FROM person; ````


7. create a column family users using the sentence columnfamily with the following columns key varchar PRIMARY KEY, full_name varchar, birth_date int, state varchar, and a set of text called emails emails set<text>
  
    - ```` CREATE COLUMNFAMILY users ( key varchar PRIMARY KEY, full_name varchar, birth_date int, state varchar, emails set<text>); ```` 
 
8. create an index on users with column birth_date and other index on state
      - ```` CREATE INDEX ON users (birth_date); ````
      - ```` CREATE INDEX ON users (state); ````
 
9. populate users columnfamily with the following data
      - ```` INSERT INTO users (key, full_name, birth_date, state, emails) VALUES ('pangeles', 'Pilar Angeles', 1975, 'UT',{'plang@gmail.com','mpa@hotmail.com'}); ````
      - ```` INSERT INTO users (key, full_name, birth_date, state, emails) VALUES ('asmith', 'Alice Smith', 1973, 'WI', {'asmith@Gmail.com'}); ````
      - ```` INSERT INTO users (key, full_name, birth_date, state, emails) VALUES ('htayler', 'Howard Tayler', 1968, 'UT', {'hty@Hotmail.com', 'otheremail@Gmail.com'}); ````
  
10. Get full name and emails for Pilar Angeles
    - ```` SELECT full_name, emails FROM users WHERE key = 'pangeles';  ````
  
  
11. Get key and state from users 
    - ````  SELECT key, state FROM users; ````

12. Get all users that live in UT and were born after 1970
    - ```` SELECT * FROM users WHERE state = 'UT' AND birth_date > 1970 ALLOW FILTERING; ````
   
````
cqlsh> CREATE KEYSPACE test with REPLICATION = {'class' : 'SimpleStrategy', 'replication_factor': 1};
cqlsh> Use test;
cqlsh:test> CREATE TABLE person ( id text, email text, name text, surname text, PRIMARY KEY (id) );
cqlsh:test> DESCRIBE person;

CREATE TABLE test.person (
    id text PRIMARY KEY,
    email text,
    name text,
    surname text
) WITH bloom_filter_fp_chance = 0.01
    AND caching = {'keys': 'ALL', 'rows_per_partition': 'NONE'}
    AND comment = ''
    AND compaction = {'class': 'org.apache.cassandra.db.compaction.SizeTieredCompactionStrategy', 'max_threshold': '32', 'min_threshold': '4'}
    AND compression = {'chunk_length_in_kb': '64', 'class': 'org.apache.cassandra.io.compress.LZ4Compressor'}
    AND crc_check_chance = 1.0
    AND dclocal_read_repair_chance = 0.1
    AND default_time_to_live = 0
    AND gc_grace_seconds = 864000
    AND max_index_interval = 2048
    AND memtable_flush_period_in_ms = 0
    AND min_index_interval = 128
    AND read_repair_chance = 0.0
    AND speculative_retry = '99PERCENTILE';

cqlsh:test> INSERT INTO person (id, name, surname, email) VALUES ('001', 'Shalabh', 'Aggarwal', 'contact@shalabhaggarwal.com');
cqlsh:test> INSERT INTO person (id, name, surname, email) VALUES ('002', 'John', 'Doe', 'john@example.com');
cqlsh:test> INSERT INTO person (id, name, surname, email) VALUES ('003', 'Harry', 'Potter', 'harry@example.com');
cqlsh:test> SELECT * FROM person;

 id  | email                       | name    | surname
-----+-----------------------------+---------+----------
 002 |            john@example.com |    John |      Doe
 001 | contact@shalabhaggarwal.com | Shalabh | Aggarwal
 003 |           harry@example.com |   Harry |   Potter

(3 rows)
cqlsh:test> CREATE COLUMNFAMILY users ( key varchar PRIMARY KEY, full_name varchar, birth_date int, state varchar, emails set<text>);
cqlsh:test> CREATE INDEX ON users (birth_date);
cqlsh:test> CREATE INDEX ON users (state);
cqlsh:test> INSERT INTO users (key, full_name, birth_date, state, emails) VALUES ('pangeles', 'Pilar Angeles', 1975, 'UT', {'plang@gmail.com','mpa@hotmail.com'});
cqlsh:test> INSERT INTO users (key, full_name, birth_date, state, emails) VALUES ('asmith', 'Alice Smith', 1973, 'WI', {'asmith@Gmail.com'});
cqlsh:test> INSERT INTO users (key, full_name, birth_date, state, emails) VALUES ('htayler', 'Howard Tayler', 1968, 'UT', {'hty@Hotmail.com', 'otheremail@Gmail.com'});
cqlsh:test> SELECT full_name, emails FROM users WHERE key = 'pangeles';

 full_name     | emails
---------------+----------------------------------------
 Pilar Angeles | {'mpa@hotmail.com', 'plang@gmail.com'}

(1 rows)
cqlsh:test> SELECT key, state FROM users;

 key      | state
----------+-------
  htayler |    UT
   asmith |    WI
 pangeles |    UT

(3 rows)
cqlsh:test> SELECT * FROM users WHERE state = 'UT' AND birth_date > 1970 ALLOW FILTERING;

 key      | birth_date | emails                                 | full_name     | state
----------+------------+----------------------------------------+---------------+-------
 pangeles |       1975 | {'mpa@hotmail.com', 'plang@gmail.com'} | Pilar Angeles |    UT

(1 rows)
 ````
 
![1](https://user-images.githubusercontent.com/64374947/135725796-b9b92081-e54b-4c1d-a0c2-dd339702e04f.JPG)
![2](https://user-images.githubusercontent.com/64374947/135725799-54835de4-299c-4aeb-96b2-a9b28b0b3c75.JPG)

