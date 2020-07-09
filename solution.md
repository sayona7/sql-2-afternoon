-- Practice join 

-- 1.
select *
from invoice
join invoice_line i2 on i2.invoice_id = invoice.invoice_id
where i2.unit_price > 0.99

-- 2.
select invoice.invoice_date, customer.first_name, customer.last_name, invoice.total
from invoice
join customer on invoice.customer_id = customer.customer_id;

-- 3.
select c.first_name, c.last_name, e.first_name, e.last_name
from customer c
join employee e on c.support_rep_id = e.employee_id;

-- 4.
select album.title, artist.name
from album
join artist on album.artist_id = artist.artist_id;

-- 5.
select pt.track_id
from playlist_track pt
join playlist p on p.playlist_id = pt.playlist_id
where p.name = 'Music';

-- 6.
select track.name
from track
join playlist_track on playlist_track.track_id = track.track_id
where playlist_track.playlist_id = 5;

-- 7.
-- select track.name, playlist.name
-- from track
-- join playlist_track on track.track_id = playlist_track.track_id
-- join playlist on playlist_track.playlist_id = playlist.playlist_id;

-- 8.
-- select track.name, album.title
-- from track
-- join album on track.album_id = album.album_id
-- join genre on genre.genre_id = track.genre_id
-- where genre.name = 'Alternative & Punk';

-- Practice nested queries

-- 1. 
select *
from invoice
where invoice_id in (select invoice_id from invoice_line where unit_price > 0.99);

-- 2.
select *
from playlist_track
where playlist_id in (select playlist_id from playlist where name = 'Music');

-- 3.
select name
from track
where track_id in (select track_id from playlist_track where playlist_id = 5);

-- 4.
select *
from track
where genre_id in (select genre_id from genre where name = 'Comedy');

-- 5. 
select * 
from track
where album_id in (select album_id from album where title = 'Fireball');

-- 6.
select * 
from track
where album_id in (
	select album_id from album where artist_id in (select artist_id from artist where name = 'Queen')
);

-- Practice updating Rows

-- 1.
update customer
set fax = null
where fax is not null;

-- 2.
update customer
set company = 'Self'
where company is null;

-- 3.
update customer
set last_name = 'Thompson'
where first_name = 'Julia' and last_name = 'Barnett';

-- 4.
update customer
set support_rep_id = 4
where email = 'luisrojas@yahoo.cl';

-- 5.
update track
set composer = 'The darkness around us'
where composer is null and 
			genre_id = (select genre_id from genre where name = 'Metal');


-- Group by

-- 1.
select count(*), genre.name
from track
join genre on track.genre_id = genre.genre_id
group by genre.name;

-- 2.
select count(*), genre.name
from track
join genre on genre.genre_id = track.genre_id
where genre.name = 'Pop' or genre.name = 'Rock'
group by genre.name;

-- 3.
select count(*), artist.name
from album
join artist on artist.artist_id = album.artist_id
group by artist.name;


-- Use Distinct

-- 1.select distinct composer
from track;

-- 2.
select distinct billing_postal_code
from invoice;

-- 3.
select distinct company
from customer;


-- Delete Rows

-- 1.
-- delete from practice_delete
-- where type = 'bronze';

-- 2.
-- delete from practice_delete
-- where type = 'silver';

-- 3.

-- delete from practice_delete
-- where value = 150;