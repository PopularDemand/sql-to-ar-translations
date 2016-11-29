# sql-to-ar-translations
From SQL to ActiveRecord and back again.


-------------------------------- SQL TO AR ------------------------------------

SELECT *
FROM
  users;

SELECT *
FROM
  users
WHERE
  user.id = 1;

SELECT *
FROM
  posts
ORDER BY
  created_at DESC
LIMIT 1;


SELECT *
FROM
  users
JOIN
  posts
ON
  posts.author_id = users.id
WHERE
  posts.created_at >= '2014-08-31 00:00:00';


SELECT
  count(*)
FROM
  users
GROUP BY
  favorite_color
HAVING
  count(*) > 1;


* The most recently updated user
* The oldest user (by age)
* all the users
* all posts sorted in descending order by date created

-------------------------------- AR TO SQL ------------------------------------

Post.all

Post.first

Post.last

Post.where(:id => 4)

Post.find(4)

User.count

Post.select(:name).where(:created_at > 3.days.ago).order(:created_at)

Post.select("COUNT(*)").group(:category_id)

All posts created before 2014

A list of all (unique) first names for authors who have written at least 3 posts

The posts with titles that start with the word "The"

Posts with IDs of 3,5,7, and 9
