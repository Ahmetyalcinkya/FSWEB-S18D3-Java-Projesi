# SQL Sorgu Alıştırmaları

Bu hafta SQL sorguları üzerine çalışıyorsunuz. Bugünkü alıştırmada sizin için hazırladığımız veritabanında aşağıda istediğimiz sonuçları elde etmenize yarayan SQL sorgularını oluşturacaksınız.

## Proje Kurulumu

Projeyi forklayın ve clonlayın. Tamamladığınızda da pushlayın.

### Kütüphane Bilgi Sistemi

Bu veritabanı, bir okulun kütüphanesinden öğrencilerin aldıkları kitapların bilgisini barındırmaktadır.

#### Tablolar

`ogrenci` tablosu öğrencilerin listesini tutar.
`islem` tablosu öğrencilerin kütüphaneden aldıkları kitapların bilgilerini tutar
`kitap` tablosu kütüphanedeki kitapların bilgisini tutar
`yazar` tablosu kitapların yazarları bilgisini tutar
`tur` tablosu kitapların türlerini tutar.

Tablo ilişiklerini görmek için [ktphn.png] dosyasına göz atın.

Yazdığınız sorguları buradan test edebilirsiniz: [https://ergineer.com/assets/materials/fkg36so5-kutuphanebilgisistemi-sql/]

##### Görevler

Aşağıda istenilen sonuçlara ulaşabilmek için gerekli SQL sorgularını yazın.

MIN-MAX, COUNT-AVG-SUM, GROUP BY, JOINS (INNER, OUTER, LEFT, RIGHT
#ilk 3 soruyu join kullanmadan yazın. 1) Öğrencinin adını, soyadını ve kitap aldığı tarihleri listeleyin.
CEVAP : select ograd, ogrsoyad, i.atarih from ogrenci as o , islem as i where o.ogrno = i.ogrno 2) Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.
CEVAP : select k.kitapadi, t.turadi from kitap as k, tur as t where k.turno = t.turno and turadi in ('Fıkra', 'Hikaye') 3) 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları listeleyin.
CEVAP : select o.ogrno, o.ograd, o.ogrsoyad, o.sinif, k.kitapadi from ogrenci as o, kitap as k, islem as i where o.ogrno = i.ogrno and i.kitapno = k.kitapno and o.sinif in ('10B','10C')

    #join ile yazın
    4) Öğrencinin adını, soyadını ve kitap aldığı tarihleri listeleyin.

    	CEVAP :  select o.ograd, o.ogrsoyad, i.atarih from ogrenci as o inner join islem as i on o.ogrno = i.ogrno


    5) Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.

    	CEVAP :  select k.kitapadi, t.turadi from kitap as k inner join tur as t on k.turno = t.turno where t.turadi in ('Fıkra','Hikaye')


    6) 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları, öğrenci adına göre listeleyin.

    	CEVAP :  select o.ogrno, o.ograd, o.ogrsoyad, k.kitapadi from ogrenci as o inner join islem as i on o.ogrno = i.ogrno inner join kitap as k on i.kitapno = k.kitapno where o.sinif in ('10B','10C') order by o.ograd, o.ogrsoyad


    7) Kitap alan öğrencinin adı, soyadı, kitap aldığı tarih listelensin. Kitap almayan öğrencilerinde listede görünsün.

    	CEVAP :  select o.ograd, o.ogrsoyad, i.atarih from ogrenci as o left join islem as i on o.ogrno = i.ogrno


    8) Kitap almayan öğrencileri listeleyin.

    	CEVAP :  select o.ograd, o.ogrsoyad, i.atarih from ogrenci as o left join islem as i on o.ogrno = i.ogrno where i.atarih is null
    			 select * from ogrenci where ogrno not in (select ogrno from islem)

    9) Alınan kitapların kitap numarasını, adını ve kaç defa alındığını kitap numaralarına göre artan sırada listeleyiniz.

    	CEVAP :  select k.kitapno,k.kitapadi, count(i.kitapno) from kitap as k inner join islem as i on i.kitapno = k.kitapno group by k.kitapno, k.kitapadi having count(i.kitapno) > 40 order by k.kitapno asc


    10) Alınan kitapların kitap numarasını, adını kaç defa alındığını (alınmayan kitapların yanında 0 olsun) listeleyin.

    	CEVAP :  select k.kitapno, k.kitapadi, count(i.kitapno) from kitap as k left join islem as i on k.kitapno = i.kitapno group by k.kitapno, k.kitapadi order by k.kitapno asc


    11) Öğrencilerin adı soyadı ve aldıkları kitabın adı listelensin.

    	CEVAP :  select o.ograd, o.ogrsoyad, k.kitapadi from ogrenci as o inner join islem as i on o.ogrno = i.ogrno inner join kitap as k on i.kitapno = k.kitapno order by o.ograd, o.ogrsoyad


    12) Her öğrencinin adı, soyadı, kitabın adı, yazarın adı soyad ve kitabın türünü ve kitabın alındığı tarihi listeleyiniz. Kitap almayan öğrenciler de listede görünsün.

    	CEVAP :  select o.ogrno, o.ograd, o.ogrsoyad, k.kitapadi, y.yazarad, y.yazarsoyad, t.turadi, i.atarih from ogrenci as o left join islem as i on o.ogrno = i.ogrno left join kitap as k on i.kitapno = k.kitapno left join yazar as y on k.yazarno = y.yazarno left join tur as t on k.turno = t.turno order by o.ograd, o.ogrsoyad


    13) 10A veya 10B sınıfındaki öğrencilerin adı soyadı ve okuduğu kitap sayısını getirin.

    	CEVAP :  select o.ograd, o.ogrsoyad, count(i.ogrno) from ogrenci as o inner join islem as i on o.ogrno = i.ogrno where o.sinif in('10A','10B') group by o.ograd, o.ogrsoyad


    14) Tüm kitapların ortalama sayfa sayısını bulunuz.
    #AVG

    	CEVAP :  select avg(sayfasayisi) from kitap


    15) Sayfa sayısı ortalama sayfanın üzerindeki kitapları listeleyin.

    	CEVAP :  select * from kitap where sayfasayisi > (select avg(sayfasayisi) from kitap)


    16) Öğrenci tablosundaki öğrenci sayısını gösterin

    	CEVAP :  select count(*) from ogrenci


    17) Öğrenci tablosundaki toplam öğrenci sayısını toplam sayı takma(alias kullanımı) adı ile listeleyin.

    	CEVAP :  select count(*) as 'total' from ogrenci


    18) Öğrenci tablosunda kaç farklı isimde öğrenci olduğunu listeleyiniz.

    	CEVAP :  select count(distinct ograd) from ogrenci


    19) En fazla sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.

    	CEVAP :  select max(sayfasayisi) from kitap


    20) En fazla sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.

    	CEVAP :  select * from kitap order by sayfasayisi desc limit 1


    21) En az sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.

    	CEVAP :  select min(sayfasayisi) from kitap


    22) En az sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.

    	CEVAP :  select * from kitap order by sayfasayisi asc limit 1


    23) Dram türündeki en fazla sayfası olan kitabın sayfa sayısını bulunuz.

    	CEVAP :  select max(k.sayfasayisi) from kitap as k inner join tur as t on k.turno = t.turno where t.turadi = trim('Dram ')


    24) numarası 15 olan öğrencinin okuduğu toplam sayfa sayısını bulunuz.

    	CEVAP :  select sum(k.sayfasayisi) from kitap as k inner join islem as i on k.kitapno = i.kitapno where i.ogrno = 15


    25) İsme göre öğrenci sayılarının adedini bulunuz.(Örn: ali 5 tane, ahmet 8 tane )

    	CEVAP :  select ograd, count(ogrno) from ogrenci group by ograd


    26) Her sınıftaki öğrenci sayısını bulunuz.

    	CEVAP :  select sinif, count(ogrno) from ogrenci where sinif is not null group by sinif


    27) Her sınıftaki erkek ve kız öğrenci sayısını bulunuz.

    	CEVAP :  select sinif, cinsiyet, count(ogrno) from ogrenci where sinif is not null and cinsiyet is not null group by sinif, cinsiyet


    28) Her öğrencinin adını, soyadını ve okuduğu toplam sayfa sayısını büyükten küçüğe doğru listeleyiniz.

    	CEVAP :  select o.ograd, o.ogrsoyad, sum(k.sayfasayisi) from ogrenci as o inner join islem as i i.ogrno = o.ogrno inner join kitap as k on k.kitapno = i.kitapno group by o.ograd, o.ogrsoyad order by sum(k.sayfasayisi) desc


    29) Her öğrencinin okuduğu kitap sayısını getiriniz.

    	CEVAP :  select o.ograd,o.ogrsoyad, count(i.islemno) from ogrenci as o inner join islem as i on o.ogrno = i.ogrno group by o.ograd, o.ogrsoyad order by count(i.islemno) desc
