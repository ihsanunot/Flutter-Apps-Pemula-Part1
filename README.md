# Belajar Flutter Aplikasi Sederhana

![versi mobile 1](https://github.com/ihsanunot/Flutter-Basic-Apps-Pertama/assets/127992374/16f2fd09-3043-4898-af0e-89ecc8ddc616)

![versi web 1](https://github.com/ihsanunot/Flutter-Basic-Apps-Pertama/assets/127992374/a4bfa9be-1941-4571-a712-a63517bcd9b8)

![versi mobile 2](https://github.com/ihsanunot/Flutter-Basic-Apps-Pertama/assets/127992374/98c44c7e-8d35-4cd6-8cd0-9316cf46ba53)

![versi web 2](https://github.com/ihsanunot/Flutter-Basic-Apps-Pertama/assets/127992374/342f9412-69a7-4cc5-9dce-6be8899ffa48)


Belajar untuk Layout, Widget di Flutter Dan jadikan aplikasi tentang wisata.
Tinggal di build apk/ios, atau ke web atau Desktop, tapi ini cuma contoh sederhana saja. terima kasih :)

---

## Catatan

Untuk lebih jelas soal code nya bisa cek di **CATATAN.md** tapi maaf Docs nya berantakan banget.


---

## Development

**Build APK**

Build APK adalah proses membungkus aplikasi flutter menjadi format .apk

- AndroidManifest.xml

Sebelum mem-build APK, kita akan mengatur berkas android/app/src/main/AndroidManifest.xml. AndroidManifest.xml merupakan sebuah berkas yang berisikan informasi mengenai aplikasi Android yang akan di-build. 

Informasi-informasi tersebut berupa nama aplikasi, ikon, permission, screen orientation, dan lain-lain. Isi dari AndroidManifest.xml seperti berikut:

```
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="id.eudeka.samples">
    <application
        android:name="io.flutter.app.FlutterApplication"
        android:label="samples"
        android:icon="@mipmap/ic_launcher">
        <activity
            android:name=".MainActivity"
            android:launchMode="singleTop"
            android:theme="@style/LaunchTheme"
            android:configChanges="orientation|keyboardHidden|keyboard|screenSize|smallestScreenSize|locale|layoutDirection|fontScale|screenLayout|density|uiMode"
            android:hardwareAccelerated="true"
            android:windowSoftInputMode="adjustResize">
            <meta-data
              android:name="io.flutter.embedding.android.NormalTheme"
              android:resource="@style/NormalTheme"
              />
            <meta-data
              android:name="io.flutter.embedding.android.SplashScreenDrawable"
              android:resource="@drawable/launch_background"
              />
            <intent-filter>
                <action android:name="android.intent.action.MAIN"/>
                <category android:name="android.intent.category.LAUNCHER"/>
            </intent-filter>
        </activity>
        <meta-data
            android:name="flutterEmbedding"
            android:value="2" />
    </application>
</manifest>
```

- Setting Nama Aplikasi
Untuk mengatur nama aplikasi, kita cukup mengubah properti android:label yang ada pada file AndroidManifest.xml

```
<application
        android:name="io.flutter.app.FlutterApplication"
        android:label="Nama Aplikasi"
        android:icon="@mipmap/ic_launcher">
```

Yang  android:label="common_widget" bisa di ganti sesuai nama aplikasi yang di inginkan.

- Setting Ikon Aplikasi
Secara default ikon aplikasi Flutter kita adalah ikon Flutter. 
Untuk mengubah icon aplikasi dengan mudah, kita akan mengganti gambar ic_launcher.png yang berada pada 
folder **android/app/src/main/res/** yang terbagi menjadi berbagai mipmap (ukuran resolusi ikon).


Hal yang pertama kita lakukan adalah membuat ikon aplikasi dengan Android Asset Studio :
* https://romannurik.github.io/AndroidAssetStudio/icons-launcher.html



Dengan Android Asset Studio, kita dapat membuat ikon aplikasi dengan mudah dan nantinya akan terbuat dalam berbagai resolusi (mipmap). Setelah membuat ikon sesuai dengan keinginan, tekan tombol download yang ada di kanan atas.

Setelah mengunduh, unzip-lah berkas tersebut dan temukan folder res/ di dalamnya.

Lalu copy folder **res/ ke android/app/src/main/res/** untuk mengganti ic_launcher.png pada setiap mipmap dengan ikon aplikasi yang baru. Atau Anda bisa gunakan library berikut untuk menghasilkan icon launcher dari pubspec.yaml.

- Setting Perizinan Aplikasi
Ketika aplikasi dalam mode debug atau profil, perizinan internet akan secara otomatis ditambahkan. Namun ketika Anda ingin menjalankan atau membuatnya dalam mode rilis, Anda perlu menambahkan semua perizinan yang dibutuhkan pada AndroidManifest.

Untuk menambahkan perizinan pada aplikasi Android, Anda bisa menambahkan tag uses-permission pada AndroidManifest, di dalam tag manifest dan sejajar tag application. Contohnya seperti di bawah ini:

```
<uses-permission android:name="android.permission.INTERNET"/>
```

### Melakukan Build APK

3 Jenis Mode Aplikasi :

**debug, profile, dan release.**

APK debug umumnya digunakan untuk pengujian dan penggunaan aplikasi secara internal. Mode debug digunakan secara default ketika menjalankan aplikasi menggunakan perintah flutter run. 

Sementara untuk bisa dirilis melalui Google Play Store, Anda perlu membuat APK release. 
Sedangkan mode profile sama hal nya dengan release hanya saja tetap dapat di-debug menggunakan tools seperti DevTools dan tidak dapat dijalankan di emulator atau simulator.

Caranya ialah menggunakan terminal pada Android Studio. Tekan tombol Terminal yang ada pada pojok kiri bawah.

Bila menggunakan Visual Studio Code pilih menu terminal yang ada pada menu kiri atas. Lalu pilih new terminal.

Jika terminal telah muncul, tuliskan perintah berikut:

```
flutter build apk --debug
```

Tunggu hingga proses build berhasil. 

Setelah berhasil, hasil build yang berupa berkas apk-debug.apk akan terletak di folder 
**build/app/outputs/apk/debug/** 

atau akan muncul direktori tempat tersimpannya berkas ketika proses build selesai pada Terminal.

Untuk bisa mem-build apk release dan mengunggahnya melalui Google Play Store, Anda memerlukan signing key. Signing key ini digunakan sebagai tanda tangan supaya aplikasi Anda lebih aman. 

Secara default Flutter menggunakan debug key sebagai signing key sehingga Anda sebenarnya bisa membuat apk release dengan menjalankan perintah berikut:

```
flutter build apk
```

Cara untuk membuat signing key dan membuat apk release dapat Anda baca pada tautan dokumentasi berikut: 
- https://flutter.dev/docs/deployment/android.

## Build IPA

**Catatan**: Build .IPA hanya bisa dijalankan dengan mendaftar akun Apple Developer Program. 
Silakan baca informasi tentang **Apple Developer Program** di sini https://developer.apple.com/programs/

Setting Nama Aplikasi
Untuk mengatur nama aplikasi buka berkas Info.plist pada direktori /ios/Runner/. Konfigurasi untuk nama aplikasi dapat Anda temukan dan ubah pada key Bundle Name.

```
<key>CFBundleName</key>
<string>builder</string>
```

atau bisa pakai https://pub.dev/packages/flutter_launcher_name

**Setting Ikon Aplikasi**

Sama seperti perangkat Android, layar untuk perangkat iPhone juga terbagi ke dalam berbagai ukuran. Sehingga diperlukan juga ukuran ikon yang berbeda. Untuk membuat berbagai ukuran ikon untuk iOS, Anda dapat memanfaatkan website seperti https://appicon.co/ atau yang lainnya.

Ketika Anda klik Generate, browser akan mengunduh berkas yang Anda butuhkan. Ikon untuk aplikasi iOS bisa Anda dapatkan pada folder Assets.xcassets.

Selanjutnya Anda dapat mengganti folder Assets.xcassets yang ada pada direktori /ios/Runner/ dengan hasil ikon yang sudah Anda generate

Atau Anda bisa menggunakan library berikut:

* https://pub.dev/packages/flutter_launcher_icons

untuk men-generate ikon aplikasi melalui pubspec.yaml

Melakukan build IPA
File IPA juga terbagi menjadi debug, profile, dan release. Namun untuk melakukan build aplikasi Flutter menjadi IPA hanya bisa dilakukan pada device macOS.

```
flutter build ios
```

Secara default perintah di atas akan menghasilkan ipa release, sedangkan jika Anda ingin membuat versi debug atau profile, gunakan perintah:

```
flutter build ios --debug
```

Namun, bagi Anda yang tidak mempunyai perangkat Apple jangan khawatir, 
Anda tetap dapat men-deploy project Anda ke iOS menggunakan CI/CD seperti Codemagic dan Bitrise.

- https://blog.codemagic.io/getting-started-with-codemagic/
- https://devcenter.bitrise.io/getting-started/getting-started-with-flutter-apps/


## Web Deployment
Pada materi ini kita akan mempelajari bagaimana melakukan build aplikasi flutter untuk platform web. Sama seperti platform android dan ios, informasi untuk pengaturan aplikasi berada pada folder web.



Setting Nama Aplikasi
Untuk mengatur nama aplikasi, kita bisa membuka berkas manifest.json. Konfigurasi untuk nama aplikasi dapat Anda temukan dan ubah pada key name dan short_name.

```
{
    "name": "wisata_bandung",
    "short_name": "wisata_bandung"
}
```


Setting Icon Aplikasi
Platform web juga membutuhkan icon dalam berbagai ukuran. Icon untuk web dapat Anda taruh pada folder /web/icons. Kemudian, Anda perlu mendaftarkannya pada berkas manifest.json.

```
{
    ...
    "icons": [
        {
            "src": "icons/Icon-192.png",
            "sizes": "192x192",
            "type": "image/png"
        },
        {
            "src": "icons/Icon-512.png",
            "sizes": "512x512",
            "type": "image/png"
        }
    ]
}

```

Melakukan build web
Sama seperti build aplikasi android dan ios, untuk mem-build aplikasi Flutter web kita menjalankan perintah flutter web. Perintah selengkapnya adalah seperti ini:

flutter build web
Sama seperti ketika menjalankan flutter web, ketika melakukan build, kita juga bisa menentukan renderer yang ingin digunakan. Untuk menentukan renderer yang digunakan, tambahkan parameter --web-renderer pada perintah flutter build. Jika tidak mendefinisikan parameter --web-renderer maka mode auto yang akan digunakan.

Hasil build akan Anda temukan pada folder /build/web. 
Folder inilah yang nantinya bisa Anda deploy ke sebuah web hosting atau web server.

**Beberapa opsi hosting yang bisa Anda gunakan, antara lain:**

- Firebase Hosting
- GitHub Pages
- Google Cloud Hosting

Informasi terkait aplikasi Android yang ingin di-build tersedia pada berkas android/app/src/main/AndroidManifest.xml. Pada berkas ini kita bisa mengatur nama, ikon, perizinan aplikasi, dll. 

Ada dua format build Android yang bisa dibuat, yaitu .apk dan .aab. Untuk melakukan build jalankan perintah berikut:

```
flutter build apk        // Untuk format apk
flutter build appbundle // untuk format aab
```

Konfigurasi untuk aplikasi iOS tersedia pada berkas **ios/Runner/Info.plist**.

```
flutter build ios
```

```
flutter build web
```

--- 

**Ihsanunot** (wisatabumi)
