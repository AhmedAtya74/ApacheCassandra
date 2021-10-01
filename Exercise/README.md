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
   
