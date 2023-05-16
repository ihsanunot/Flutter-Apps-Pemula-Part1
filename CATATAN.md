# Flutter Project

Belajar Membuat Aplikasi Flutter paling dasar dengan studi kasus Aplikasi Sederhana.

Ingat layout yang penting :
Column, Container, Row

Alur :
Column(Row(childern:[....]))
*tegantung layout utama nya jadi banyak nesting*

Sintaks :

```
flutter run -d chrome

```

Bikin Scaffold() didalam class dan menaruh body di dalam paramete Scaffold, lalu class yang ada scaffold nya masukin ke dalam MaterialApp.

Contoh:

```
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Wisata Bandung',
      theme: ThemeData(),
      home: const DetailScreen(),
    );
  }

```

Lalu 

```
return Scaffold(
      body: Column(),
    );
```

Kita  perlu membungkus **widget Text** ke dalam **Container** supaya kita dapat memberikan property seperti margin atau padding.

Tentang EdgeInsets untuk setting ukuran Margin:
- https://api.flutter.dev/flutter/painting/EdgeInsets-class.html

---

Jika kesulitan menentukan margin atas 

khususnya pada perangkat yang memiliki notch yang umumnya memiliki status bar yang lebih besar

Anda dapat memanfaatkan widget **SafeArea**.

---

*Silakan Hot Reload*

Lalu, jangan lupa **Flutter Inspect Widget** untuk mengecek nya.

Untuk memaksimalkan ukuran lebar dari Column, tambahkan kode berikut:

```
crossAxisAlignment: CrossAxisAlignment.stretch,
```

oke karena beberapa secara vertikal selesai, saat nya membuat widget yang horizontal (Row).

tambahkan child kedua dari Column dengan sebuah Container berisi Row. 

Tambahkan juga margin pada sisi atas dan bawah untuk memberikan jarak antar widget.

---

Merapihkan Row

```
mainAxisAlignment: MainAxisAlignment.spaceEvenly,
```
perhatikan yg vertically
itu utk membuat jadi tiga column
untuk icon text keterangan dll.
---

Apabila gambar yang kita tampilkan terlalu besar sementara layar pada perangkat terlalu kecil, maka akan terlihat tampilan garis hitam-kuning yang menunjukkan terjadi overflow. Kondisi overflow ini terjadi ketika konten yang kita tampilkan melebihi luas layar yang ada.

Sebagai solusi, tentunya kita bisa mengubah ukuran dari gambar, namun tentunya tidak praktis jika kita harus mengubah ukuran setiap gambar yang ditampilkan. 

Tentu ada banyak sekali ukuran layar yang tersedia, bukan? Solusi lainnya yaitu dengan menerapkan scrolling. 

Salah satu widget scrolling yang bisa kita manfaatkan adalah SingleChildScrollView. Widget ini membutuhkan satu child yang nantinya bisa di-scroll pada layar. 

Pindahkan widget Column ke dalam SingleChildScrollView supaya nantinya bisa di-scroll.

Selanjutnya kita akan menambahkan beberapa gambar lagi yang disusun secara horizontal. 

Anda mungkin mengira untuk menggunakan widget Row supaya gambar bisa tersusun secara horizontal. Namun, perlu diingat bahwa kita juga memerlukan fitur scrolling agar tidak terjadi overflow. 

Oleh karena itu, kita akan menggunakan ListView. Widget ini memungkinkan kita untuk menerapkan scrolling terhadap beberapa item (children).

---

```
class DetailScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: SafeArea(
        child: SingleChildScrollView(
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.stretch,
            children: <Widget>[
              Image.asset('images/farm-house.jpg'),
              Container(...),
              Container(...),
              Container(...),
              ListView(
                children: [
                  Image.network(
                      'https://media-cdn.tripadvisor.com/media/photo-s/0d/7c/59/70/farmhouse-lembang.jpg'),
                  Image.network(
                      'https://media-cdn.tripadvisor.com/media/photo-w/13/f0/22/f6/photo3jpg.jpg'),
                  Image.network(
                      'https://media-cdn.tripadvisor.com/media/photo-m/1280/16/a9/33/43/liburan-di-farmhouse.jpg'),
                ],
              ),
            ],
          ),
        ),
      ),
    );
  }
```

Jika Anda menjalankan aplikasi atau melakukan hot reload, aplikasi Anda akan menjadi blank dan muncul pesan eror pada log. 

Kenapa ya? ListView diletakkan di dalam Column, di mana keduanya sama-sama memiliki atribut height yang memakan space di sepanjang layar. 

Sebagai solusi kita perlu memberikan ukuran tinggi yang statis terhadap ListView. Namun ListView tidak memiliki parameter height, lantas bagaimana nih? Caranya, gunakan widget lain yang memiliki parameter height. 

Anda dapat membungkus widget ListView ke dalam Container atau pun SizedBox. Ukuran tinggi ini nantinya juga digunakan sebagai tinggi Image yang tampil.

```
class DetailScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: SafeArea(
        child: SingleChildScrollView(
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.stretch,
            children: <Widget>[
              Image.asset('images/farm-house.jpg'),
              Container(...),
              Container(...),
              Container(...),
              SizedBox(
                height: 150,
                child: ListView(
                  children: [
                    Image.network(
                        'https://media-cdn.tripadvisor.com/media/photo-s/0d/7c/59/70/farmhouse-lembang.jpg'),
                    Image.network(
                        'https://media-cdn.tripadvisor.com/media/photo-w/13/f0/22/f6/photo3jpg.jpg'),
                    Image.network(
                        'https://media-cdn.tripadvisor.com/media/photo-m/1280/16/a9/33/43/liburan-di-farmhouse.jpg'),
                  ],
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

Jika Anda memiliki beberapa teks dengan style yang sama, Anda dapat menggunakan variabel untuk menyimpan TextStyle dan meringkas kode.

```
var informationTextStyle = const TextStyle(fontFamily: 'Oxygen');
```

variabel diatas bisa digunakan di class Text() dll.

Contoh :

```
Column(
 children: <Widget>[
const Icon(Icons.access_time),
const SizedBox(height: 8.0),
Text(
'09:00 - 20:00',
style: informationTextStyle,
)
]),
```

Di dalam body dari Scaffold kita bisa memakai **widget card**. 

Widget ini adalah widget material design yang menghasilkan tampilan seperti kartu dengan ujung yang membulat dan bayangan di belakang.

Kemudian susun **Row dan Column** seperti contoh untuk menyusun child dari Card. 

di Scaffold biasa nya harus ada appBar dan Body.

Jika pas di running muncul overflow karena aset gambar yang terlalu besar, kita bisa gunakan Expanded
untuk mengatasi nya.



Expanded juga membuat tampilan dapat menyesuaikan di perangkat yang lebih besar atau kecil. 
Bungkus masing-masing item dari widget Row ke dalam Expanded. 
Berikan parameter flexyang menurut Anda cocok.

Item pertama Anda sudah siap. 

Selanjutnya kita akan membuat kartu ini bisa diklik untuk berpindah ke halaman detail. 

Kita bisa menggunakan widget InkWell yang menyediakan parameter onTap. 
Pindahkan widget Card Anda menjadi child dari InkWell.

Parameter onTap menerima argumen berupa sebuah fungsi lambda. 
Di sini kita akan menambahkan Navigator untuk berpindah ke halaman detail.

Contoh:

```
onTap: () {
  Navigator.push(context, MaterialPageRoute(builder: (context) {
    return DetailScreen();
  }));
},
```

**Jalankan aplikasi. Seharusnya sampai langkah ini aplikasi Anda sudah dapat berpindah halaman ketika item diklik.**

Selanjutnya kita akan menampilkan beberapa item ke *MainScreen*. 

kita masih menggunakan data statis dan lokal yang disimpan pada objek List. 
Sebelumnya, buatlah kelas sebagai blueprint untuk menyimpan objek tempat wisata. 

Buat folder baru di dalam folder lib lalu berikan nama **model**. 

Di dalam folder model buat berkas dart bernama **tourism_place.dart**.

```
class TourismPlace {
  String name;
  String location;
  String description;
  String openDays;
  String openTime;
  String ticketPrice;
  String imageAsset;
  List<String> imageUrls;
 
  TourismPlace({
    required this.name,
    required this.location,
    required this.description,
    required this.openDays,
    required this.openTime,
    required this.ticketPrice,
    required this.imageAsset,
    required this.imageUrls,
  });
}
```

Siapkan data statis yang ingin ditampilkan Anda dapat menyalin kode berikut dan taruh di berkas tourism_place.dart paling bawah.

```
var tourismPlaceList = [
  TourismPlace(
    name: 'Farm House Lembang',
    location: 'Lembang',
    description:
        'Berada di jalur utama Bandung-Lembang, Farm House menjadi objek wisata yang tidak pernah sepi pengunjung. Selain karena letaknya strategis, kawasan ini juga menghadirkan nuansa wisata khas Eropa. Semua itu diterapkan dalam bentuk spot swafoto Instagramable.',
    openDays: 'Open Everyday',
    openTime: '09:00 - 20:00',
    ticketPrice: 'Rp 25000',
    imageAsset: 'images/farm-house.jpg',
    imageUrls: [
      'https://media-cdn.tripadvisor.com/media/photo-s/0d/7c/59/70/farmhouse-lembang.jpg',
      'https://media-cdn.tripadvisor.com/media/photo-w/13/f0/22/f6/photo3jpg.jpg',
      'https://media-cdn.tripadvisor.com/media/photo-m/1280/16/a9/33/43/liburan-di-farmhouse.jpg'
    ],
  ),
  TourismPlace(
    name: 'Observatorium Bosscha',
    location: 'Lembang',
    description:
        'Memiliki beberapa teleskop, antara lain, Refraktor Ganda Zeiss, Schmidt Bimasakti, Refraktor Bamberg, Cassegrain GOTO, dan Teleskop Surya. Refraktor Ganda Zeiss adalah jenis teleskop terbesar untuk meneropong bintang. Benda ini diletakkan pada atap kubah sehingga saat teropong digunakan, atap tersebut harus dibuka. Observatorium Bosscha boleh dikunjungi oleh siapa pun, tanpa tiket. Namun, bagi yang ingin menggunakan teleskop Zeiss, wajib mendaftarkan diri. Untuk instansi atau lembaga pendidikan, diberikan jadwal hari Selasa sampai Jumat. Sementara itu, kunjungan individu dibuka setiap hari Sabtu.',
    openDays: 'Open Tuesday - Saturday',
    openTime: '09:00 - 14:30',
    ticketPrice: 'Rp 20000',
    imageAsset: 'images/bosscha.jpg',
    imageUrls: [
      'https://media-cdn.tripadvisor.com/media/photo-o/12/6b/63/0b/bosscha-observatory.jpg',
      'https://media-cdn.tripadvisor.com/media/photo-p/0d/6a/88/9b/photo3jpg.jpg',
      'https://media-cdn.tripadvisor.com/media/photo-o/11/3f/04/39/p-20171111-110220-largejpg.jpg',
    ],
  ),
  TourismPlace(
    name: 'Jalan Asia Afrika',
    location: 'Kota Bandung',
    description:
        'Jalan Asia Afrika di Bandung memiliki kaitan yang sangat erat dengan pendirian kota Kembang ini. Karena pada saat itu, Gubernur Jenderal Herman Willem Deaendels dari Belanda menancapkan tongkatnya saat memerintahkan pendirian kota ini, yang kemudian diabadikan menjadi tugu Bandung Nol Kilometer.',
    openDays: 'Open Everyday',
    openTime: '24 hours',
    ticketPrice: 'Free',
    imageAsset: 'images/jalan-asia-afrika.jpg',
    imageUrls: [
      'https://media-cdn.tripadvisor.com/media/photo-o/0d/c2/e7/e6/quotes-kota-bandung.jpg',
      'https://media-cdn.tripadvisor.com/media/photo-w/17/f4/44/01/jalan-asia-afrika.jpg',
      'https://media-cdn.tripadvisor.com/media/photo-s/0a/ef/36/e2/jalan-asia-afrika.jpg',
    ],
  ),
  TourismPlace(
    name: 'Stone Garden',
    location: 'Padalarang',
    description:
        'Stone Garden atau Taman Batu di Padalarang – Bandung ini adalah nama secara harafiah untuk apa yang akan kita lihat jika berada di sana. Hamparan batu yang artistik membuat kita merasa tidak sedang berada di Bandung, apalagi di Padalarang. Hamparan batu yang dimaksud bukan terhampar begitu saja di atas tanah luas yang menjadi permukaannya. Batu-batu besar yang ukuran pastinya bervariasi tersusun seperti memiliki suatu formasi matematis.',
    openDays: 'Open Everyday',
    openTime: '06:00 - 17:00',
    ticketPrice: 'Rp 3000',
    imageAsset: 'images/stone-garden.jpg',
    imageUrls: [
      'https://media-cdn.tripadvisor.com/media/photo-o/15/01/d7/4b/p-20180510-153310-01.jpg',
      'https://media-cdn.tripadvisor.com/media/photo-w/15/68/00/32/stone-garden-citatah.jpg',
      'https://media-cdn.tripadvisor.com/media/photo-o/0d/a2/cb/05/stone-garden-citatah.jpg',
    ],
  ),
  TourismPlace(
    name: 'Taman Film Pasopati',
    location: 'Kota Bandung',
    description:
        'Menjadi salah satu tempat wisata di Bandung yang favorit, tentu Taman Film ini memiliki fasilitas cukup memadai. Pemberian fasilitas ini memiliki harapan para pengunjung akan merasa nyaman dan tak segan2 untuk kembali berkunjung terus menerus kesini. Beberapa fasilitas taman yang bisa kamu nikmati diantaranya seperti layar videotron besar berukuran 4×8 untuk memutar berbagai macam pilihan film seperti Film Indonesia, Bollywood, Korea, ataupun Indie Bandung.',
    openDays: 'Open Everyday',
    openTime: '24 hours',
    ticketPrice: 'Free',
    imageAsset: 'images/taman-film.jpg',
    imageUrls: [
      'https://media-cdn.tripadvisor.com/media/photo-o/08/8b/87/50/bandung-movie-park.jpg',
      'https://media-cdn.tripadvisor.com/media/photo-o/17/67/d5/53/img-20190505-114509-largejpg.jpg',
      'https://media-cdn.tripadvisor.com/media/photo-w/09/73/33/05/taman-film-pasopati.jpg',
    ],
  ),
  TourismPlace(
    name: 'Museum Geologi',
    location: 'Kota Bandung',
    description:
        'Museum Geologi didirikan pada tanggal 16 Mei 1929. Museum ini telah direnovasi dengan dana bantuan dari JICA (Japan International Cooperation Agency). Setelah mengalami renovasi, Museum Geologi dibuka kembali dan diresmikan oleh Wakil Presiden RI, Megawati Soekarnoputri pada tanggal 23 Agustus 2000. Sebagai salah satu monumen bersejarah, museum berada di bawah perlindungan pemerintah dan merupakan peninggalan nasional. Dalam Museum ini, tersimpan dan dikelola materi-materi geologi yang berlimpah, seperti fosil, batuan, mineral. Kesemuanya itu dikumpulkan selama kerja lapangan di Indonesia sejak 1850.',
    openDays: 'Open Saturday - Thursday',
    openTime: '09:00 - 15:30',
    ticketPrice: 'Rp 3000',
    imageAsset: 'images/museum-geologi.jpg',
    imageUrls: [
      'https://media-cdn.tripadvisor.com/media/photo-w/19/1c/8e/f7/geology-museum.jpg',
      'https://media-cdn.tripadvisor.com/media/photo-o/11/a7/35/b7/geology-museum.jpg',
      'https://media-cdn.tripadvisor.com/media/photo-s/1a/55/e0/dc/geology-museum.jpg',
    ],
  ),
  TourismPlace(
    name: 'Floating Market',
    location: 'Lembang',
    description:
        'Tempat wisata ini sepertinya memang ditujukan untuk wisata keluarga di Bandung. Di sini kita bisa menikmati suasana kawasan yang tertata rapi dan alami. Pada awalnya, floating market Lembang tidak begitu luas. Tapi sekarang sudah ekspansi dan memiliki banyak objek menarik baru. Nama floating market ini sepertinya merujuk pada stand tempat jualan makanan yang berada dalam perahu.',
    openDays: 'Open Everyday',
    openTime: '09:00 - 17:00',
    ticketPrice: 'Rp 20000',
    imageAsset: 'images/floating-market.png',
    imageUrls: [
      'https://media-cdn.tripadvisor.com/media/photo-o/17/f9/ff/f8/floating-market-bandung.jpg',
      'https://media-cdn.tripadvisor.com/media/photo-p/1a/86/d3/cd/20200103-125059-largejpg.jpg',
      'https://media-cdn.tripadvisor.com/media/photo-p/19/ce/b4/9b/img20181224120857-largejpg.jpg',
    ],
  ),
  TourismPlace(
    name: 'Kawah Putih',
    location: 'Ciwidey',
    description:
        'Kawah Putih adalah tempat wisata di Bandung yang paling terkenal. Berlokasi di Ciwidey, Jawa Barat, kurang lebih sekitar 50 KM arah selatan kota Bandung, Kawah Putih adalah sebuah danau yang terbentuk akibat dari letusan Gunung Patuha. Sesuai dengan namanya, tanah yang ada di kawasan ini berwarna putih akibat dari pencampuran unsur belerang.',
    openDays: 'Open Everyday',
    openTime: '07:00 - 17:00',
    ticketPrice: 'Rp 15000',
    imageAsset: 'images/kawah-putih.jpg',
    imageUrls: [
      'https://media-cdn.tripadvisor.com/media/photo-o/0b/6e/7c/ce/rocks-sticking-out-of.jpg',
      'https://media-cdn.tripadvisor.com/media/photo-p/0b/35/30/14/white-crater.jpg',
      'https://media-cdn.tripadvisor.com/media/photo-o/0a/8b/9a/79/2945-t00572-www-initempatwisat.jpg',
    ],
  ),
  TourismPlace(
    name: 'Ranca Upas',
    location: 'Ciwidey',
    description:
        'Ranca Upas Ciwidey adalah kawasan bumi perkemahan di bawah pengelolaan perhutani. Tempat ini berada di kawasan wisata Bandung Selatan, satu lokasi dengan kawah putih, kolam Cimanggu dan situ Patenggang. Banyak hal yang bisa dilakukan di kawasan wisata ini, seperti berkemah, berinteraksi dengan rusa, sampai bermain di water park dan mandi air panas.',
    openDays: 'Open Everyday',
    openTime: '24 hours',
    ticketPrice: 'Rp 20000',
    imageAsset: 'images/ranca-upas.jpg',
    imageUrls: [
      'https://media-cdn.tripadvisor.com/media/photo-o/1a/e0/7f/9c/kampung-cai-ranca-upas.jpg',
      'https://media-cdn.tripadvisor.com/media/photo-w/13/ee/2f/87/ranca-upas.jpg',
      'https://media-cdn.tripadvisor.com/media/photo-w/13/ee/27/0a/ranca-upas.jpg',
    ],
  ),
];
```

Jangan lupa untuk menambahkan import berkas tourism_place.dart pada file main_screen.dart.

Sekarang kita pakai **ListView**

Untuk menampilkan variabel tourismPlaceList di atas menjadi item card yang dapat diklik. 
Tambahkan widget ListView sebagai body dari Scaffold. 

Pindahkan widget FlatButton dan seluruh konten di dalamnya sebagai widget dari setiap item di dalam tourismPlaceList.

```
class MainScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Wisata Bandung'),
      ),
      body: ListView.builder(
        itemBuilder: (context, index) {
          final TourismPlace place = tourismPlaceList[index];
          return InkWell(
            onTap: () {
              Navigator.push(context, MaterialPageRoute(builder: (context) {
                return DetailScreen();
              }));
            },
            child: Card(
              ......
              child: Image.asset(place.imageAsset),
```

Jangan lupa untuk mengganti tampilan item secara dinamis sesuai data dari objek TourismPlace. Jalankan aplikasi untuk melihat hasil perubahan.

Agar halaman detail bisa menampilkan informasi sesuai tempat wisata yang dipilih, kita perlu mengirimkan data TourismPlace melalui constructor. 

Buka berkas detail_screen.dart lalu tambahkan variabel serta constructor-nya.

Tambahkan keyword required agar parameter place wajib disertakan ketika membuat objek DetailScreen. Sesuaikan juga informasi yang ditampilkan dengan property yang didapat dari constructor.

Jangan lupa untuk menambahkan data place pada constructor.

```
Navigator.push(context, MaterialPageRoute(builder: (context) {
  return DetailScreen(place: place);
}));
```

Selanjutnya, kita akan menambahkan tombol navigasi untuk kembali ke halaman daftar tempat wisata. Tombol ini akan kita taruh di atas gambar utama atau gambar dari aset. Kita akan menggunakan widget Stack. Widget ini digunakan untuk menyusun widget seperti Column atau Row, bedanya widget pada Stack disusun secara bertumpuk (stacked). Ubah kode Anda menjadi seperti berikut:

```
Stack(
  children: <Widget>[
    Image.asset(place.imageAsset),
    IconButton(icon: const Icon(Icons.arrow_back), onPressed: () {})
  ],
),
```

Tambahkan fungsionalitas agar ketika icon back ini diklik akan kembali ke halaman sebelumnya.

```
IconButton(
  icon: const Icon(Icons.arrow_back),
  onPressed: () {
    Navigator.pop(context);
  },
),
```
Jika Anda jalankan aplikasi, ikon ini akan sedikit menabrak notification bar pada perangkat Android. Hal ini akan semakin terlihat apabila Anda menggunakan perangkat yang memiliki notch.

? Kita akan memanfaatkan widget SafeArea yang akan memberikan padding sesuai dengan sistem operasi yang digunakan sehingga widget akan berada di area yang aman. Buat widget SafeArea lalu pindahkan IconButton ke dalamnya.

```
SafeArea(
  child: IconButton(
    icon: Icon(Icons.arrow_back),
    onPressed: () {
      Navigator.pop(context);
    },
  ),
),
```

kita bisa optimasi utk tampilan web nya

pertama coba kita edit title di dalam appbar:

```
AppBar(
  title:
      Text('Wisata Bandung. Size: ${MediaQuery.of(context).size.width}'),
),
```

Lalu kita coba running withoud debug,
lalu kita rumah2 ukuran window broser kita
terus kita coba cari breakpoint atau titik yang berada di berapa
contoh pas di 600px tampilan nya sudah di renponsive atau jadi berantakan.

berarti ukuran lebar 600 sebagai batas breakpoint ukuran mobile.

Pada ukuran lebar di atas 600 kita akan buat tampilan yang berbeda menggunakan grid. Sebelumnya, mari pindahkan tampilan ListView menjadi widget tersendiri.

Kemudian buat widget baru untuk menampilkan GridView

Selanjutnya ubah body dari MainScreen untuk menampilkan TourismPlaceList atau TourismPlaceGrid. Kita akan memanfaatkan widget LayoutBuilder untuk mendapatkan ukuran layar.

```
body: LayoutBuilder(
        builder: (BuildContext context, BoxConstraints constraints) {
          if (constraints.maxWidth <= 600) {
            return TourismPlaceList();
          } else {
            return TourismPlaceGrid();
          }
```

Berikut ini adalah tampilan untuk Card

```
GridView.count(
  crossAxisCount: 4,
  children: tourismPlaceList.map((place) {
    return InkWell(
      onTap: () {
        Navigator.push(context, MaterialPageRoute(builder: (context) {
          return DetailScreen(place: place);
        }));
      },
      child: Card(
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.stretch,
          children: [
            Expanded(
              child: Image.asset(
                place.imageAsset,
                fit: BoxFit.cover,
              ),
            ),
            const SizedBox(height: 8),
            Padding(
              padding: const EdgeInsets.only(left: 8.0),
              child: Text(
                place.name,
                style: const TextStyle(
                  fontSize: 16.0,
                  fontWeight: FontWeight.bold,
                ),
              ),
            ),
            Padding(
              padding: const EdgeInsets.only(left: 8.0, bottom: 8.0),
              child: Text(
                place.location,
              ),
            ),
          ],
        ),
      ),
    );
  }).toList(),
),
```

Tambahkan lagi kondisi pada LayoutBuilder. Kita akan menentukan jumlah kolom yang digunakan melalui parameter constructor.

```
LayoutBuilder(
  builder: (BuildContext context, BoxConstraints constraints) {
    if (constraints.maxWidth <= 600) {
      return TourismPlaceList();
    } else if (constraints.maxWidth <= 1200) {
      return TourismPlaceGrid(gridCount: 4);
    } else {
      return TourismPlaceGrid(gridCount: 6);
    }
  },
),
```

Tambahkan constructor pada kelas TourismPlaceGrid

```
class TourismPlaceGrid extends StatelessWidget {
  final int gridCount;
 
  const TourismPlaceGrid({Key? key, required this.gridCount}) : super(key: key);
 
  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: const EdgeInsets.all(16.0),
      child: GridView.count(
        crossAxisCount: gridCount,
        children: tourismPlaceList.map((place) {
          return InkWell(...);
        }).toList(),
      ),
    );
  }
}
```

Tambahkan lagi kondisi pada LayoutBuilder. Kita akan menentukan jumlah kolom yang digunakan melalui parameter constructor.

```
LayoutBuilder(
  builder: (BuildContext context, BoxConstraints constraints) {
    if (constraints.maxWidth <= 600) {
      return TourismPlaceList();
    } else if (constraints.maxWidth <= 1200) {
      return TourismPlaceGrid(gridCount: 4);
    } else {
      return TourismPlaceGrid(gridCount: 6);
    }
  },
),
```

### Rangkuman :

Rangkuman Materi
Selamat! Anda telah belajar banyak di modul ini. Ayo kita ingat dan ulas kembali apa saja yang sudah kita pelajari.

Pada Flutter, semuanya adalah widget. Widget merupakan komponen yang perlu saling disusun untuk membangun aplikasi Flutter.

Widget pada Flutter terbagi menjadi StatelessWidget dan StatefulWidget. 

State sendiri merupakan data yang ada pada suatu widget dan dapat berubah sesuai interaksi pengguna.

Scaffold merupakan sebuah widget yang digunakan untuk membuat tampilan dasar atau kerangka material design pada aplikasi Flutter. Di dalam Scaffold, kita bisa menambahkan widget AppBar, Body, dan FloatingActionButton.

Container merupakan widget yang digunakan untuk menampung widget lain. Di dalam Container kita bisa menambahkan style, shape (bentuk), dan dekorasi lain pada child widget-nya.

Widget Padding sesuai namanya merupakan widget untuk menambahkan padding atau jarak antara konten dengan border-nya.

Center digunakan untuk membuat child widget berada di posisi tengah.

Widget Row dan Column digunakan untuk menyusun beberapa widget secara horizontal atau vertikal.
Flutter menyediakan beberapa tampilan tombol (button), seperti ElevatedButton, TextButton, OutlinedButton, IconButton, dan DropdownButton.
Terdapat beberapa widget yang dapat digunakan untuk menerima input dari pengguna, di antaranya adalah TextField, Switch, Radio, dan Checkbox.

Widget Image digunakan untuk menampilkan gambar dari internet atau aset proyek.
Kita dapat menambahkan font sendiri sebagai aset lalu menampilkannya menggunakan widget TextStyle.

ListView digunakan untuk menampilkan beberapa item dalam bentuk baris atau kolom yang bisa di-scroll.

Flutter menyediakan widget Flexible dan Expanded yang dapat memberikan ukuran secara fleksibel dan menempati ruang yang tersedia.
Kita dapat memanfaatkan MediaQuery atau widget LayoutBuilder untuk mendapatkan ukuran layar aplikasi yang dijalankan. Dengan ini, kita bisa menentukan breakpoint untuk membuat tampilan yang responsif.

Flutter dapat melakukan navigasi antar halaman dengan memanfaatkan Navigator

---

**Ihsanunot (wisatabumi)**