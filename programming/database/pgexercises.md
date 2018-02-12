# PostgreSQL Exercises

## Basic

```sql
-- select all
select * from cd.facilities;

-- select column
select name, membercost from cd.facilities;

-- where
select * from cd.facilities where membercost > 0;

select facid, name, membercost, monthlymaintenance
	from cd.facilities
	where
		membercost > 0 and
		(membercost < monthlymaintenance/50.0);

-- where like
select *
	from cd.facilities
	where
		name like '%Tennis%';

-- where in
select *
	from cd.facilities
	where
		facid in (1,5);

-- classify (case)
select name,
	case when (monthlymaintenance > 100) then
		'expensive'
	else
		'cheap'
	end as cost
	from cd.facilities;

-- date
select memid, surname, firstname, joindate
	from cd.members
	where joindate >= '2012-09-01';

-- distinct, order by, limit
select distinct surname
	from cd.members
order by surname
limit 10;

-- union
-- it combines the results of two SQL queries into a single table.
-- both results from the two queries must have the same number of columns and compatible data types.
select surname
	from cd.members
union
select name
	from cd.facilities;

-- aggregation
select max(joindate) as latest
	from cd.members;

select firstname, surname, joindate
	from cd.members
	where joindate =
		(select max(joindate) from cd.members);
```

## Joins and Subqueries

```sql
-- inner join
select bks.starttime
	from
		cd.bookings bks
		inner join cd.members mems
			on mems.memid = bks.memid
	where
		mems.firstname='David'
		and mems.surname='Farrell';

-- different syntax
select bks.starttime
  from
    cd.bookings bks,
    cd.members mems
  where
    mems.firstname='David'
    and mems.surname='Farrell'
    and mems.memid = bks.memid;


select bks.starttime as start, facs.name as name
	from
		cd.facilities facs
		inner join cd.bookings bks
			on facs.facid = bks.facid
	where
		facs.facid in (0,1) and
		bks.starttime >= '2012-09-21' and
		bks.starttime < '2012-09-22'
order by bks.starttime;

-- recursive join
select distinct recs.firstname as firstname, recs.surname as surname
	from
		cd.members mems
		inner join cd.members recs
			on recs.memid = mems.recommendedby
order by surname, firstname;

-- left outer join
-- 매칭되지 않아도 않은 채로 row 반환
select
	mems.firstname as memfname,
	mems.surname as memsname,
	recs.firstname as recfname,
	recs.surname as recsname
from
	cd.members mems
	left outer join cd.members recs
	on recs.memid = mems.recommendedby
order by memsname, memfname;

-- three join
select distinct mems.firstname || ' ' || mems.surname as member, facs.name as facility
	from
		cd.members mems
		inner join cd.bookings bks
			on mems.memid = bks.memid
		inner join cd.facilities facs
			on bks.facid = facs.facid
	where
		bks.facid in (0,1)
order by member;

select mems.firstname || ' ' || mems.surname as member,
	facs.name as facility,
	case
		when mems.memid = 0 then
			bks.slots*facs.guestcost
		else
			bks.slots*facs.membercost
	end as cost
        from
                cd.members mems
                inner join cd.bookings bks
                        on mems.memid = bks.memid
                inner join cd.facilities facs
                        on bks.facid = facs.facid
        where
		bks.starttime >= '2012-09-14' and
		bks.starttime < '2012-09-15' and (
			(mems.memid = 0 and bks.slots*facs.guestcost > 30) or
			(mems.memid != 0 and bks.slots*facs.membercost > 30)
		)
order by cost desc;

-- subquery
select distinct mems.firstname || ' ' || mems.surname as member,
	(
    select recs.firstname || ' ' || recs.surname as recommender
      from cd.members recs
      where recs.memid = mems.recommendedby
	)
	from
		cd.members mems
order by member;

select member, facility, cost from (
  select
  	mems.firstname || ' ' || mems.surname as member,
  	facs.name as facility,
  	case
  		when mems.memid = 0 then
  			bks.slots*facs.guestcost
  		else
  			bks.slots*facs.membercost
  	end as cost
  	from
  		cd.members mems
  		inner join cd.bookings bks
  			on mems.memid = bks.memid
  		inner join cd.facilities facs
  			on bks.facid = facs.facid
 	where
  		bks.starttime >= '2012-09-14' and
  		bks.starttime < '2012-09-15'
 	) as bookings
	where cost > 30
order by cost desc;
```

## Modifying

```sql
-- insert
insert into cd.facilities
    (facid, name, membercost, guestcost, initialoutlay, monthlymaintenance)
    values (9, 'Spa', 20, 30, 100000, 800);

insert into cd.facilities
    (facid, name, membercost, guestcost, initialoutlay, monthlymaintenance)
    values
        (9, 'Spa', 20, 30, 100000, 800),
        (10, 'Squash Court 2', 3.5, 17.5, 5000, 80);

-- use select to supply dynamic data
insert into cd.facilities
    (facid, name, membercost, guestcost, initialoutlay, monthlymaintenance)
    select (select max(facid) from cd.facilities)+1, 'Spa', 20, 30, 100000, 800;

-- update
update cd.facilities
    set initialoutlay = 10000
    where facid = 1;

update cd.facilities
    set
        membercost = 6,
        guestcost = 30
    where facid in (0,1);

update cd.facilities facs
    set
        membercost = (select membercost * 1.1 from cd.facilities where facid = 0),
        guestcost = (select guestcost * 1.1 from cd.facilities where facid = 0)
    where facs.facid = 1;

-- delete
delete from cd.bookings;

-- truncate
truncate cd.bookings;

delete from cd.members where memid = 37;

delete from cd.members where memid not in (select memid from cd.bookings);

-- more performance
delete from cd.members mems where not exists (select 1 from cd.bookings where memid = mems.memid);
```

## Aggregates

```sql
-- count
select count(*) from cd.facilities;

-- COUNT(*) simply returns the number of rows
-- COUNT(address) counts the number of non-null addresses in the result set.
-- COUNT(DISTINCT address) counts the number of different addresses in the facilities table.

-- group by
select recommendedby, count(*)
	from cd.members
	where recommendedby is not null
	group by recommendedby
order by recommendedby;

-- sum
select facid, sum(slots) as "Total Slots"
	from cd.bookings
	group by facid
order by facid;

-- extract
select facid, extract(month from starttime) as month, sum(slots) as "Total Slots"
	from cd.bookings
	where
		starttime >= '2012-01-01'
		and starttime < '2013-01-01'
	group by facid, month
order by facid, month;

-- distinct
select count(distinct memid) from cd.bookings;

-- having
-- aggregate functions are not allowed in WHERE
-- The behaviour of HAVING is easily confused with that of WHERE. The best way to think about it is that in the context of a query with an aggregate function, WHERE is used to filter what data gets input into the aggregate function, while HAVING is used to filter the data once it is output from the function.
select facid, sum(slots) as "Total Slots"
  from cd.bookings
  group by facid
  having sum(slots) > 1000
order by facid;

select facs.name, sum(slots * case
			when memid = 0 then facs.guestcost
			else facs.membercost
		end) as revenue
	from cd.bookings bks
	inner join cd.facilities facs
		on bks.facid = facs.facid
	group by facs.name
order by revenue;

-- subquery in FROM must have an alias
-- Postgres, unlike some other RDBMSs like SQL Server and MySQL, doesn't support putting column names in the HAVING clause.
select name, revenue from (
	select facs.name, sum(case
				when memid = 0 then slots * facs.guestcost
				else slots * membercost
			end) as revenue
		from cd.bookings bks
		inner join cd.facilities facs
			on bks.facid = facs.facid
		group by facs.name
	) as agg where revenue < 1000
order by revenue;

-- Common Table Expressions(CTEs)
-- CTEs can be thought of as allowing you to define a database view inline in your query.
select facid, sum(slots) as totalslots
	from cd.bookings
	group by facid
	having sum(slots) = (select max(sum2.totalslots) from
		(select sum(slots) as totalslots
		from cd.bookings
		group by facid
		) as sum2);
-- to
with sum as (select facid, sum(slots) as totalslots
	from cd.bookings
	group by facid
)
select facid, totalslots
	from sum
	where totalslots = (select max(totalslots) from sum);


```