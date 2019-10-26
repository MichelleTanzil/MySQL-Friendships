Write a SQL query that returns a list of users along with their friends' names.

SELECT *
FROM users
LEFT JOIN friendships ON users.id = friendships.user_id
LEFT JOIN users AS users2 ON users2.id = friendships.friend_id; 

1. Return all users who are friends with Kermit, make sure their names are displayed in results.

SELECT users.first_name, users.last_name, users2.first_name AS friend_first_name, users2.last_name AS friend_last
FROM users
LEFT JOIN friendships ON users.id = friendships.user_id
LEFT JOIN users AS users2 ON users2.id = friendships.friend_id 
WHERE friend_id = 4 OR users.id = 4;

2. Return the count of all friendships

SELECT COUNT(friend_id)
FROM users
LEFT JOIN friendships ON users.id = friendships.user_id
LEFT JOIN users AS users2 ON users2.id = friendships.friend_id;

3. Find out who has the most friends and return the count of their friends.

SELECT users.first_name, users.last_name, COUNT(friend_id) AS friend_num
FROM users
LEFT JOIN friendships ON users.id = friendships.user_id
LEFT JOIN users AS users2 ON users2.id = friendships.friend_id
GROUP BY user_id
ORDER BY friend_num DESC;

4. Create a new user and make them friends with Eli Byers, Kermit The Frog, and Marky Mark

INSERT INTO users(first_name, last_name, created_at, updated_at)
VALUES ('Kobe', 'Bryant', NOW(), NOW());

INSERT INTO friendships(user_id, friend_id, created_at, updated_at)
VALUES (6, 2, NOW(), NOW());

INSERT INTO friendships(user_id, friend_id, created_at, updated_at)
VALUES (6, 4, NOW(), NOW());

INSERT INTO friendships(user_id, friend_id, created_at, updated_at)
VALUES (6, 5, NOW(), NOW());

5. Return the friends of Eli in alphabetical order

SELECT users.first_name, users.last_name, users2.first_name AS friend_first_name, users2.last_name AS friend_last
FROM users
LEFT JOIN friendships ON users.id = friendships.user_id
LEFT JOIN users AS users2 ON users2.id = friendships.friend_id 
WHERE friendships.friend_id = 2 OR users.id = 2;

6. Remove Marky Mark from Eli’s friends.

DELETE FROM friendships
WHERE friendships.id = 5;

7. Return all friendships, displaying just the first and last name of both friends

SELECT users.first_name, users.last_name, users2.first_name AS friend_first_name, users2.last_name AS friend_last
FROM users
LEFT JOIN friendships ON users.id = friendships.user_id
LEFT JOIN users AS users2 ON users2.id = friendships.friend_id 