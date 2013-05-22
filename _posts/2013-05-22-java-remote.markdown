---
layout: post
title:  "Program Remote dalam Java"
date:   2013-05-22 18:11:00
categories: programming
---
>salam. saya diwajibkan menggunakan java untuk control other pc like send 
>message , terminate pc .. tapi saya blank .. mohon tunjuk ajar.

Memang agak blank kalau nak selesaikan masalah ni sekali gus. Cuba pecahkan kepada beberapa masalah kecil. Asas penyelesaian masalah (problem solving 101). Perkara pertama yang anda perlu faham bila cuba selesaikan masalah ini adalah ia memerlukan satu komputer berhubung dengan komputer yang lain. Ini asas, kalau ini pun anda sukar hendak faham maka memang mustahil nak selesaikannya.

Setelah anda faham bahawa ia memerlukan komputer A berhubung dengan komputer B, soalan kedua adalah bagaimana komputer ini berhubung ? Saya andaikan anda mengikuti kursus Sains Komputer atau IT dan kalau tak silap saya kedua-dua kursus ini mempunyai subjek yang dinamakan Data Communication. Untuk teori, masa untuk belek kembali buku rujukan Data Communication anda. Utk praktikal, sambungkan je komputer A dan B ke Wifi access point dan configure apa yang patut. Hasil akhir, komputer A perlu ada IP address dan komputer B juga perlu ada IP address dan anda boleh ping komputer A dari komputer B, vice-versa.

Setelah komputer A dan komputer B boleh saling berhubung (boleh ping), masa utk anda fikirkan bagaimana hendak hantar arahan dari komputer A ke komputer B. Ada disebut pasal socket programming sebelum ini. Komputer berhubung antara satu sama lain melalui socket.  Socket ni umpama tingkap dengan komputer mempunyai pelbagai tingkap yang mungkin terbuka dan tertutup. Tingkap yang terbuka membolehkan data dihantar kepadanya. Saya hendak menulis post ini pun memerlukan saya hantar bait-bait string ini melalui wifi komputer ke wifi akses point, kemudian melalui jaringan ISP, seterusnya melalui kabel dasar laut merentasi lautan pasifik ke server facebook di US, yang menerimanya pada tingkap yang dinamakan HTTP nombor 80. Begitu juga apabila anda hendak berhubung antara komputer A dan B.

Untuk menghantar arahan dari komputer A ke B, B perlu bertindak sebagai server dan A sebagai client. Untuk itu, B perlu membuka tingkap khas, mungkin bernombor 8000. Kod pseudo utk program server B mungkin seperti berikut:-

sock = socket.listen('192.168.0.1', 8000)
connection = sock.accept()
while True: data = connection.receive(1024); connection.send(data)

Andaikan 192.168.0.1 adalah IP address utk komputer B, ia kini membuka tingkap (socket) pada port 8000, bersedia menerima 1024 bytes data pada satu2 masa dan apabila mendapat data tersebut, hantar balik data tersebut kepada penghantar.

Seterusnya anda perlu tulis program utk client yang akan dijalankan pada komputer A. Kod pseudo bagi client mungkin spt berikut:-

sock = socket.connect('192.168.0.1', 8000)
sock.send('hello')
response = sock.receive(1024)

Kod utk Java semestinya lebih panjang namun apa yang saya cuba sampaikan adalah konsep asas kepada socket programming di mana satu program listen pada port tertentu, satu program lain pula connect dan hantar data ke port tersebut. Setelah anda dapat hantar data melalui socket, anda boleh mula merancang logik yang hendak dijalankan utk melaksanakan arahan seperti shutdown. Contohnya apabila menerima string 'shutdown', call function utk shutdown dan bukannya hantar balik string tu spt di atas.

Berkaitan shutdown atau apa-apa bentuk arahan yang melibatkan kawalan kepada sistem operasi komputer, anda perlu belajar satu lagi konsep iaitu system call utk membolehkan program java anda melaksanakan arahan spt shutdown, create folder, copy file dsbnya. Sudah agak panjang jadi saya sambung dengan link kepada google - https://encrypted.google.com/search?hl=en&q=java%20system%20call

Penerangan terlalu over simplified dan saya mohon maaf utk itu namun tugas anda sekarang adalah membentuk persoalan berasaskan rangka saya saya gariskan di atas. Harap berguna.
