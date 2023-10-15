Penjelasan Kode dan cara menjalakan aplikasi crawler dan menggunakan container NoSQL
- Buka aplikasi atau open source python coder seperti VSC, jupyter notebook, atau google collab, dsb

- lalu install library pandas dan node js dengan perintah:

!pip install pandas
!curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -
!sudo apt-get install -y nodejs 

- menyiapkan variabel untuk menyimpan file hasil crawling dan tentukan keyword yang ingin dicari. contohnya disini saya mencari ayam geprek

filename = 'ayamgeprek.csv'
search_keyword = 'ayam geprek'
limit = 100

- jalankan tweet harvest, token yang didapatkan merupakan token akun twitter kalian (bisa didapat dengan inspect aplikasi lalu ke cookies

!npx --yes tweet-harvest@latest -o "{filename}" -s "{search_keyword}" -l {limit} --token "d0d7723a85829611db7957ec32e5f634e08cfe34"

- import panda

import pandas as pd

- lalu deklarasikan file path nya

file_path = f"tweets-data/{filename}"

- dan deklarasikan data di path tadi lalu tampilkan

df = pd.read_csv(file_path, delimiter=";")
display (df)

- merupakan command tambahan untuk menghapus data yang ingin dihilangkan

df.drop(df.columns[[3, 4, 5, 6, 7]], axis=1, inplace=True)

- tampilkan dataframe yang telah dimodifikasi
display(df)

Menyimpan sumber data 
- Buka windows powershell

- Run MongoDB Image di Docker

docker run -d --name mongodb -p 27017:27017 mongo

- Pastikan container telah running

docker ps

- Keluar dari root container

exit

- Masukkan file csv yang ingin di gunakan

#Contoh disini saya meletakkan file di folder tmp
docker cp C:\Users\ROG\Downloads\ayamgeprek_dropped_column.csv mongodb:/tmp/ayamgeprek_dropped_column.csv

- Masuk ke root container

docker exec -it f47 bash

- Masuk ke folder yang digunakan dan cek apakah sudah ada

cd tmp
ls -1

- Keluar dari folder tmp

cs ..

- Tampilkan databases

mongosh
show databases

- Gunakan databases local

use local

- Buat new collection

db.createCollection("myCollection")

- import file csv yang ingin digunakan

mongoimport --db local --collection mycollection --type csv --headerline --file /tmp/ayamgeprek_dropped_column.csv

- tampilkan new collection

db.mycollection.find()

 
