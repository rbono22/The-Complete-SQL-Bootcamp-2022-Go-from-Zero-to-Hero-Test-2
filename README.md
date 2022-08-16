# The-Complete-SQL-Bootcamp-2022-Go-from-Zero-to-Hero-Test-2

## How can you retrieve all the information from the cd.facilities table?
SELECT * FROM cd.facilities; 

## You want to print out a list of all of the facilities and their cost to members. How would you retrieve a list of only facility names and costs?
SELECT name, membercost FROM cd.facilities;

## How can you produce a list of facilities that charge a fee to members?
SELECT * FROM cd.facilities<br>
WHERE membercost > 0;

## How can you produce a list of facilities that charge a fee to members, and that fee is less than 1/50th of the monthly maintenance cost? Return the facid, facility name, member cost, and monthly maintenance of the facilities in question.
SELECT facid, name, membercost, monthlymaintenance<br>
FROM cd.facilities<br>
WHERE membercost > 0 AND (membercost < monthlymaintenance/50.0);

## How can you produce a list of all facilities with the word 'Tennis' in their name?
SELECT * FROM cd.facilities<br>
WHERE name LIKE '%Tennis%';

## How can you retrieve the details of facilities with ID 1 and 5? Try to do it without using the OR operator.
SELECT * FROM cd.facilities WHERE facid IN (1,5);

## How can you produce a list of members who joined after the start of September 2012? Return the memid, surname, firstname, and joindate of the members in question.
SELECT memid, surname, firstname, joindate<br>
FROM cd.members WHERE joindate >= '2012-09-01';

## How can you produce an ordered list of the first 10 surnames in the members table? The list must not contain duplicates.
SELECT DISTINCT surname FROM cd.members<br>
ORDER BY  surname LIMIT 10;

## You'd like to get the signup date of your last member. How can you retrieve this information?
SELECT MAX(joindate) AS latest_signup FROM cd.members;

#### The answer is: 2012-09-26 18:08:45

## Produce a count of the number of facilities that have a cost to guests of 10 or more.
SELECT COUNT(*) FROM cd.facilities<br>
WHERE guestcost >= 10;

#### The Count is 6

## Produce a list of the total number of slots booked per facility in the month of September 2012. Produce an output table consisting of facility id and slots, sorted by the number of slots.
SELECT facid, sum(slots) AS "Total Slots" FROM cd.bookings<br>
WHERE starttime >= '2012-09-01' AND starttime < '2012-10-01'<br>
GROUP BY facid ORDER BY SUM(slots);

## Produce a list of facilities with more than 1000 slots booked. Produce an output table consisting of facility id and total slots, sorted by facility id.
SELECT facid, sum(slots) AS total_slots FROM cd.bookings<br>
GROUP BY facid HAVING SUM(slots) > 1000<br>
ORDER BY facid;

## How can you produce a list of the start times for bookings for tennis courts, for the date '2012-09-21'? Return a list of start time and facility name pairings, ordered by the time.
SELECT cd.bookings.starttime AS start, cd.facilities.name AS name<br>
FROM cd.facilities<br>
INNER JOIN cd.bookings<br>
ON cd.facilities.facid = cd.bookings.facid<br>
WHERE cd.facilities.facid IN (0,1)<br>
AND cd.bookings.starttime >= '2012-09-21' <br>
AND cd.bookings.starttime < '2012-09-22' <br>
ORDER BY cd.bookings.starttime;

## How can you produce a list of the start times for bookings by members named 'David Farrell'?
SELECT cd.bookings.starttime <br>
FROM cd.bookings <br>
INNER JOIN cd.members ON <br>
cd.members.memid = cd.bookings.memid <br>
WHERE cd.members.firstname='David' <br>
AND cd.members.surname='Farrell';

#### This produces 34 rows of timestamps
