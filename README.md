# sql-to-ar-translations
From SQL to ActiveRecord and back again.


-------------------------------- SQL TO AR ------------------------------------

SELECT *
FROM
  users;

User.all



SELECT *
FROM
  users
WHERE
  user.id = 1;

User.find(1)



SELECT *
FROM
  posts
ORDER BY
  created_at DESC
LIMIT 1;

Post.last



SELECT *
FROM
  users
JOIN
  posts
ON
  posts.author_id = users.id
WHERE
  posts.created_at >= '2014-08-31 00:00:00';

User.joins('JOIN posts ON author_id = users.id').where("created_at >= '2014-08-31 00:00:00'")



SELECT
  count(*)
FROM
  users
GROUP BY
  favorite_color
HAVING
  count(*) > 1;

User.select('COUNT(*) AS count_per_color').group(:color).having(count_per_color > 1)


The most recently updated user
User.order(updated_at: :desc).limit(1)

The oldest user (by age)
User.order(age: :desc).limit(1)

all the users
User.all

all posts sorted in descending order by date created
Post.order(created_at: :desc)

-------------------------------- AR TO SQL ------------------------------------

Post.all
SELECT *
FROM posts

Post.first
SELECT *
FROM posts
LIMIT 1

Post.last
SELECT *
FROM posts
ORDER BY created_at DESC
LIMIT 1

Post.where(:id => 4)
SELECT *
FROM posts
WHERE id = 4

Post.find(4)
SELECT *
FROM posts
WHERE id = 4

User.count
SELECT COUNT(*)
FROM users

Post.select(:name).where(:created_at > 3.days.ago).order(:created_at)
SELECT name
FROM posts
WHERE created_at > 2016-11-26 00:00:00(whatever is 3 days ago)
ORDER BY created_at

Post.select("COUNT(*)").group(:category_id)
SELECT COUNT(*)
FROM posts
GROUP BY category_id

All posts created before 2014
SELECT *
FROM posts
WHERE created_at < 2014-01-01 00:00:00

A list of all (unique) first names for authors who have written at least 3 posts
SELECT DISTINCT first_name, COUNT(*) AS post_count
FROM users JOIN posts ON users.id=author_id
GROUP BY users.id
HAVING post_count >= 3


The posts with titles that start with the word "The"

Posts with IDs of 3,5,7, and 9
