MARIADB
=========

Bu rol wordpress için gerekli olan veritabanı inşası için oluşturulmuştur. 
Mariadb veritabanının sistem deposundaki son versionunu indirir ve konuk kullanıcı ve test veritabanlarını silerek root için parola atamasını gerçekleştirir. 
Son olarka wordpress için gerekli veritabanı ve kullanıcıyı oluşturup bunların üzerindeki yetkilendirmeleri yapar.

Herhangi bir bağımlılığı yoktur. Kendi başına çalıştırılarak bir veritabanı kurulumu yapılabilir. Ancak şuan (11.10.2020) değişkenler rollerin dışında bulunan main.yaml dosyası aracılığıyla alındığı için role içerisinde bazı düzenlemeler yapmak gerekecektir. 

Bununla ilgili aksiton alındığında buraya not düşeceğim.