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
cevap: SELECT o.ograd ,o.ogrsoyad,i.atarih from ogrenci o ,islem i
WHERE i.ogrno =o.ogrno

    2) Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.
    cevap:	select k.kitapadi,t.turadi  from kitap k,tur t
    		where k.turno =t.turno
    		and t.turadi  IN('Fıkra','Hikaye')


    3) 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları listeleyin.
    cevap:	select o.ogrno ,o.ograd ,o.ogrsoyad ,k.kitapadi from ogrenci o ,kitap k, islem i
    		where k.kitapno =i.kitapno  and o.ogrno =i.ogrno and o.sinif IN ('10B','10C')

    #join ile yazın
    4) Öğrencinin adını, soyadını ve kitap aldığı tarihleri listeleyin.
    cevap:	select o.ograd ,o.ogrsoyad,i.atarih from ogrenci o
    		join islem i on i.ogrno=o.ogrno


    5) Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.
    cevap:	select k.kitapadi ,t.turadi from kitap k
    		join tur t on t.turno=k.turno
    		where t.turadi IN('Fıkra','Hikaye')

    6) 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları, öğrenci adına göre listeleyin.
    cevap:	select o.ogrno ,o.ograd ,o.ogrsoyad,k.kitapadi  from ogrenci o
    		join islem i on i.ogrno=o.ogrno
    		join kitap k on k.kitapno=i.kitapno
    		where o.sinif IN ('10B','10C')

    7) Kitap alan öğrencinin adı, soyadı, kitap aldığı tarih listelensin. Kitap almayan öğrencilerinde listede görünsün.
    cevap:	select o.ograd,o.ogrsoyad,i.atarih from ogrenci o
    		left join islem i on i.ogrno=o.ogrno

    8) Kitap almayan öğrencileri listeleyin.
    cevap:	select o.ograd,o.ogrsoyad,i.atarih from ogrenci o
    		left join islem i on i.ogrno=o.ogrno
    		where i.atarih IS NULL


    9) Alınan kitapların kitap numarasını, adını ve kaç defa alındığını kitap numaralarına göre artan sırada listeleyiniz.
    cevap:	select  k.kitapno , k.kitapadi, count(k.kitapno)as Alınma_Sayisi from kitap k
    		left Join islem i ON i.kitapno = k.kitapno
    		group by k.kitapno

    10) Alınan kitapların kitap numarasını, adını kaç defa alındığını (alınmayan kitapların yanında 0 olsun) listeleyin.
    cevap:	select  k.kitapno , k.kitapadi, count(k.kitapno)as Alınma_Sayisi from kitap k
    		left Join islem i ON i.kitapno = k.kitapno
    		group by k.kitapno

    11) Öğrencilerin adı soyadı ve aldıkları kitabın adı listelensin.
    cevap:	select o.ograd ,o.ogrsoyad ,k.kitapadi from ogrenci o
    		join islem i on o.ogrno =i.ogrno
    		join kitap k on k.kitapno=i.kitapno

    12) Her öğrencinin adı, soyadı, kitabın adı, yazarın adı soyad ve kitabın türünü ve kitabın alındığı tarihi listeleyiniz. Kitap almayan öğrenciler de listede görünsün.
    cevap:  select o.ograd ,o.ogrsoyad ,k.kitapadi,y.yazarad,y.yazarsoyad,t.turadi,i.atarih from ogrenci o
    		left join islem i on o.ogrno =i.ogrno
    		left Join kitap k on i.kitapno=k.kitapno
    		left Join yazar y on y.yazarno=k.yazarno
    		left join tur t on t.turno=k.turno

    13) 10A veya 10B sınıfındaki öğrencilerin adı soyadı ve okuduğu kitap sayısını getirin.


    14) Tüm kitapların ortalama sayfa sayısını bulunuz.
    #AVG

    15) Sayfa sayısı ortalama sayfanın üzerindeki kitapları listeleyin.


    16) Öğrenci tablosundaki öğrenci sayısını gösterin


    17) Öğrenci tablosundaki toplam öğrenci sayısını toplam sayı takma(alias kullanımı) adı ile listeleyin.


    18) Öğrenci tablosunda kaç farklı isimde öğrenci olduğunu listeleyiniz.


    19) En fazla sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.


    20) En fazla sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.


    21) En az sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.


    22) En az sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.


    23) Dram türündeki en fazla sayfası olan kitabın sayfa sayısını bulunuz.


    24) numarası 15 olan öğrencinin okuduğu toplam sayfa sayısını bulunuz.


    25) İsme göre öğrenci sayılarının adedini bulunuz.(Örn: ali 5 tane, ahmet 8 tane )


    26) Her sınıftaki öğrenci sayısını bulunuz.


    27) Her sınıftaki erkek ve kız öğrenci sayısını bulunuz.


    28) Her öğrencinin adını, soyadını ve okuduğu toplam sayfa sayısını büyükten küçüğe doğru listeleyiniz.


    29) Her öğrencinin okuduğu kitap sayısını getiriniz.
