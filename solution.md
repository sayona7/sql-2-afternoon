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