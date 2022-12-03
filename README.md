# function-lambda
Latihan menggunakan Function dan Lambda pada python dan membuat program crud sederhana
1. Pertama kita buat folder 11-function-lambda dan didalam file tersebut kita buat file Latihan.py dan Praktikum6.py.
![sabtu](https://user-images.githubusercontent.com/115931631/205458234-1a4e05c4-ed59-4d32-93b4-f8e302624052.png)

2. Lalu buka Latihan.py dan input codingan sebagai berikut lalu run dengan mengetikan perintah berikut diterminal python Latihan.py
          import math

          def a(n): return lambda x: x**n
          lambdaA = a(4)
          print(lambdaA(4))

          def b(i, j):
              return lambda x, y: math.sqrt(x**i + y**j)

          lambdaB = b(4, 0)
          print(lambdaB(3, 0))

          def c (*args):
              return lambda *params: sum(args) / len(params)

          lambdaC = c(1, 2, 3, 4, 5)
          print(lambdaC(2, 2, 5))

          def d(firstname):
              return lambda *Lastname: "".join(set(firstname)) + "".join(set(Lastname))

          lambdaD = d("Adria")
          print(lambdaD("Vanza"))

Dan hasilnya seperti berikut ini :


![Latihan](https://user-images.githubusercontent.com/115931631/205458294-cd0b1470-be76-490f-8b3a-5ce007b0b1e0.png)

3. Selanjutnya kita akan membuat program crud sederhana dan berikut flowchart program yang akan kita buat.
![Flow](https://user-images.githubusercontent.com/115931631/205458349-68054e29-f4ac-4e8f-87aa-ef901175f5a5.png)

4. Langkah selanjutnya buka file Praktikum6.py dan masukan inputan sebagai berikut lalu run dengan mengetikan perintah berikut terminal python Praktikum6.py :
          
          from tabulate import tabulate

          # Buat dictionary yang memiliki value berupa list
          data = {'nama' : [], 'nilai': [] }

          def tampilkan():
              # variabel i untuk membuat penomoran data ketika dibuat tabel
              i = range(1, len(data['nama'])+1)
              # membuat list header kolom yang akan ditampilkan
              headers = ["No", "Nama", "Nilai"]

              # data dapat ditampilkan jika variabel data terisi minimal satu data
              if len(data['nama']) > 0:
                  print(tabulate(data, headers, showindex=i,tablefmt="rounded_outline"))

              # jika tidak ada data, maka tampilkan pesan
              else:
                  print("\nTidak Ada Data \n")


          def tambah():
              # buat inputan untuk mengisi nim
              nama = input("Masukkan Nama : ")

              # jika nim yang di input tersedia pada variabel data, cetak pesan lalu lakukan input ulang
              while nama in data['nama']:
                  print("Mahasiswa dengan nama yang sama sudah ada")
                  nama = input("Masukkan Nama : ")

              nilai = input("masukkan nilai : ")
              while not nilai.isnumeric():
                  nilai = input("masukkan nilai : ")

              data['nama'].append(nama)
              data['nilai'].append(int(nilai))
              print("Data Berhasil Ditambah!!")


          def hapus(nama):
              if nama in data['nama']:
                  # buat dictionary kosong untuk menampilkan data yang cocok sesuai input NIM
                  dataMhs = {}
                  index = data['nama'].index(nama)

                  # lakukan pengisian data yang cocok ke dalam variabel dataMhs
                  for key in data.keys():
                      dataMhs[key] = []
                      dataMhs[key].append(data[key][index])
                  print(tabulate(dataMhs, headers="keys", tablefmt="rounded_outline"))
                  # lakukan konfirmasi penghapusan
                  confirm = input("anda yakin ingin menghapus data ini?? (y/t)")

                  # jika input selain y atau t lakukan konfirmasi berulang
                  while (confirm not in ['y', 't']):
                      print("input salah")
                      confirm = input("anda yakin ingin menghapus data ini?? (y/t)")

                  # jika konfirmasi selesai dilakukan, maka hapus data mahasiswa pada variabel data
                  if confirm == "y":
                      for key in data.keys():
                          data[key].pop(index)
                      print("Data Berhasil Dihapus!!\n")

              else:
                  print("data nama tidak ditemukan!!")


          def ubah(nama):
              if nama in data['nama']:
                  # buat dictionary kosong untuk menampilkan data yang cocok sesuai input nama
                  dataMhs = {}
                  index = data['nama'].index(nama)
                  # lakukan pengisian data yang cocok ke dalam variabel dataMhs
                  for key in data.keys():
                      dataMhs[key] = []
                      dataMhs[key].append(data[key][index])

                  print(tabulate(dataMhs, headers="keys", tablefmt="rounded_outline"))
                  # lakukan input data apa yang akan diubah
                  pilihan = input("pilih field yang akan diubah : \n1.Nama\n2.Nilai\n")
                  # lakukan pengecekan pada variabel pilihan yang dikonversi menjadi nilai integer
                  match int(pilihan):
                      case 1:
                          print("data nama sebelumnya : " + dataMhs['nama'][0])
                          nama = input("Masukkan nama Baru : ")
                          while nama in data['nama']:
                              if nama == dataMhs['nama'][0]:
                                  break
                              print("Mahasiswa dengan nama yang sama sudah ada")
                              nama = input("Masukkan nama Baru : ")
                          data['nama'][index] = nama

                      case 2:
                          print("data nilai sebelumnya :" , dataMhs['nilai'][0])
                          nilai = input("Masukkan nilai baru : ")
                          data['nilai'][index] = nilai

                  for key in data.keys():
                      dataMhs[key] = []
                      dataMhs[key].append(data[key][index])
                  print(tabulate(dataMhs, headers="keys", tablefmt="rounded_outline"))

              else:
                  print("data nama tidak ditemukan!")

          while True:
              print("[ (l)ihat , (t)ambah, (u)bah, (h)apus, (k)eluar ] \n")
              tanya = input("Masukkan Pilihan : ")
              match tanya:
                  case "l":
                      tampilkan()
                  case "t":
                      tambah()
                  case "u":
                      tampilkan()
                      if len(data['nama']) > 0:
                          nama = input("masukkan nama siswa yang akan diubah : ")
                          ubah(nama)
                  case "h":
                      tampilkan()
                      if len(data['nama']) > 0:
                          nama = input("masukkan nama siswa yang akan dihapus : ")
                          hapus(nama)
                  case "k":
                      print("anda sudah Keluar dari program")
                      break
                  case _:
                      print("Tidak Sesuai Pilihan, Silahkan Pilih Kembali!!\n")
                      continue


Dan berikut ini adalah hasilnya :

Jika kita memilih opsi T = menambah data maka akan tampil hasil seperti berikut ini :

![(t)](https://user-images.githubusercontent.com/115931631/205458470-3143cec5-a318-4433-838a-2a9969ddac0e.png)

Jika kita memilih opsi L = Melihat semua data maka akan tanpil hasil seperti berikut ini :

![(l)](https://user-images.githubusercontent.com/115931631/205458491-dc490378-6bfe-4efb-9d4d-c0329b5029e1.png)

Jika kita memilih opsi U = mengupdate data maka akan tampil hasil seperti berikut ini :

![(u)](https://user-images.githubusercontent.com/115931631/205458511-73a8eb40-621f-47f3-9b40-68f46656a785.png)

Jika kita memilih opsi H = menghapus data maka akan tampil hasil seperti berikut ini :

![(h)](https://user-images.githubusercontent.com/115931631/205458530-5f33ccf6-7b0f-4114-9b37-ed29e97eb623.png)

Jika kita memilih opsi K = keluar program maka akan tampil hasil seperti berikut ini :

![(k)](https://user-images.githubusercontent.com/115931631/205458548-3541ef1e-b814-467c-8d97-ba4ef754e52e.png)

  ### SELESAI
Demikianlah sedikit penjelasan dari saya tentang program crud sederhana.

mohon maaf jika ada kesalahan, kurang lebihnya mohon maaf
  ### TerimaKasih
