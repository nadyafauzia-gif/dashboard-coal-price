# Dashboard Harga Batubara

Dashboard web publik untuk memantau tren **HBA** (Harga Batubara Acuan, Kementerian ESDM) dan **ICI** (Argus/Coalindo, data publik) periode 2023–2026, menghitung **HPB** dari parameter kualitas, membandingkan harga jual aktual perusahaan, serta menyimulasikan harga 3, 6, dan 12 bulan ke depan.

Semuanya ada dalam satu file `index.html`, tanpa server dan tanpa database.

## Fitur

- **Tren & perbandingan**: filter *Time from / Time to (mm/yy)*, pilih seri HBA, HBA I–III, dan ICI 1–5, input harga jual aktual perusahaan (manual atau tempel/impor CSV), serta tabel selisih dan rasio terhadap benchmark.
- **Price simulation**: skenario Bearish / Base / Bullish, slider faktor penentu (impor China dan India, pasokan Indonesia, LNG JKM, freight, cuaca), pita ketidakpastian 80%, dan tabel validasi model (backtest).
- **Kalkulator HPB**: hitung Harga Patokan Batubara dari GAR, TM, TS dan Ash (basis ar, atau adb + IM yang dikonversi otomatis). Formula dipilih otomatis sesuai rezim periode HBA: Kepmen 41.K/2023 dan 227.K/2023 (satu kategori HBA) sampai Feb 2025, interpolasi kalori antar-kategori sejak Mar 2025 (Kepmen 72.K/2025 jo. 268.K/2025). Isi tanggal B/L untuk memilih periode HBA (Periode I/II) otomatis. HPB perusahaan juga bisa diinput manual per bulan.
- **Royalti** (tab tersendiri): royalti = tonase × [maks(harga jual, HPB) − biaya barging/transhipment yang diakui] × tarif. Tarif otomatis menurut tanggal B/L (PP 26/2022 atau PP 19/2025), kelas kalori, tier HBA dan **metode tambang (open pit / underground)** yang dipilih pengguna; hasil dan perbandingan kedua metode tampil berdampingan dengan input (di HP muncul bilah ringkas di bawah layar), dengan daftar pengapalan dan ekspor CSV. Dari tab Kalkulator HPB, tombol **Hitung royalti →** membawa HPB, GAR dan tanggal B/L langsung ke tab Royalti.
- **Data & sumber**: tabel HBA per periode Kepmen, ICI dari sumber yang sudah dipublikasikan terbuka, dan indikator konteks pasar beserta sumbernya.

## Bahasa / Language

Dashboard tersedia dalam bahasa Indonesia (default) dan Inggris. Gunakan tombol **ID | EN** di pojok kanan atas; pilihan tersimpan di browser. Untuk membagikan tautan langsung berbahasa Inggris, tambahkan `?lang=en` di akhir alamat, misalnya `https://namaakun.github.io/dashboard-batubara/?lang=en`.

## Privasi data perusahaan

Harga jual aktual dan HPB yang dimasukkan **hanya disimpan di browser perangkat masing-masing** (localStorage). Data itu tidak dikirim ke server, tidak masuk ke repository ini, dan tidak terlihat oleh pengguna lain.

- **Jangan** menambahkan data penjualan perusahaan ke repository ini, karena repository-nya publik.
- Isi harga lewat kartu **Input harga jual aktual perusahaan** di tab *Tren & perbandingan* (bulan mm/yy, harga, volume, GAR), atau tempel/impor banyak baris sekaligus dalam format `mm/yy,harga,volume,gar`.
- Gunakan **Ekspor CSV** untuk cadangan atau memindahkan data ke perangkat lain.
- Data ICI di situs ini hanya berasal dari sumber yang sudah dipublikasikan terbuka (lihat kolom Sumber di tab *Data & sumber*); data ICI berlangganan dan HPB internal tidak dimuat.
- Estimasi royalti dan daftar pengapalan juga hanya tersimpan di browser masing-masing.
- Kalkulator HPB dan royalti adalah alat bantu estimasi, bukan pengganti perhitungan e-PNBP. Koefisien koreksi kualitas perlu dicocokkan dengan lampiran Kepmen ESDM 72.K/MB.01/MEM.B/2025 (diubah 268.K/MB.01/MEM.B/2025) sebelum dipakai untuk royalti atau kontrak. Acuan HBA untuk tier tarif royalti (HBA utama atau HBA kategori) juga perlu dikonfirmasi.

## Memperbarui data HBA

Data tertanam di `index.html`, pada baris yang diawali `window.__DATA__ = {...}`.

Setiap ESDM merilis HBA baru (periode I sekitar tanggal 1, periode II sekitar tanggal 15):

1. Di `hba_periods`, tambahkan satu baris periode baru beserta sumbernya.
2. Di `hba_monthly`, perbarui nilai bulan tersebut. Nilai bulanan adalah rata-rata periode I dan II.
3. Di `model_params`, perbarui nilai `cutoff`.
4. Klik **Commit changes**. Situs akan ter-update dalam 1–2 menit.

## Catatan metodologi

- Simulasi berbasis HBA. Newcastle dipakai sebagai jangkar melalui kurva futures ICE.
- Data model dimulai Sep 2023, setelah HBA beralih ke formula 4 kategori kalori.
- Elastisitas faktor adalah asumsi analis, bukan hasil estimasi statistik.
- Hasil simulasi adalah alat bantu perencanaan, bukan prediksi pasti atau saran investasi.
- Data ICI tidak lengkap karena ICI adalah data berlangganan Argus/Coalindo.

Cut-off data: HBA Periode I Oktober 2026 (Kepmen ESDM 384.K/MB.01/MEM.B/2026).
