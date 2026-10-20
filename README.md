# Dashboard Harga Batubara

Dashboard web publik untuk memantau tren **HBA** (Harga Batubara Acuan, Kementerian ESDM) dan **ICI** (Argus/Coalindo, data publik) periode 2023–2026, menghitung **HPB** dari parameter kualitas, membandingkan harga jual aktual perusahaan, serta menyimulasikan harga 3, 6, dan 12 bulan ke depan.

Semuanya ada dalam satu file `index.html`, tanpa server dan tanpa database.

## Fitur

- **Tren & perbandingan**: filter *Time from / Time to (mm/yy)*, pilih seri HBA, HBA I–III, dan ICI 1–5, input harga jual aktual perusahaan (manual atau tempel/impor CSV), serta tabel selisih dan rasio terhadap benchmark.
- **Price simulation**: skenario Bearish / Base / Bullish, slider faktor penentu (impor China dan India, pasokan Indonesia, LNG JKM, freight, cuaca), pita ketidakpastian 80%, dan tabel validasi model (backtest).
- **Kalkulator HPB**: hitung Harga Patokan Batubara dari GAR, TM, TS dan Ash berdasarkan HBA periode terpilih (interpolasi kalori antar-kategori HBA, koreksi kualitas opsional), lalu simpan hasilnya ke kurva. HPB perusahaan juga bisa diinput manual per bulan.
- **Data & sumber**: tabel HBA per periode Kepmen, ICI dari sumber yang sudah dipublikasikan terbuka, dan indikator konteks pasar beserta sumbernya.

## Privasi data perusahaan

Harga jual aktual dan HPB yang dimasukkan **hanya disimpan di browser perangkat masing-masing** (localStorage). Data itu tidak dikirim ke server, tidak masuk ke repository ini, dan tidak terlihat oleh pengguna lain.

- **Jangan** menambahkan data penjualan perusahaan ke repository ini, karena repository-nya publik.
- Isi harga lewat kartu **Input harga jual aktual perusahaan** di tab *Tren & perbandingan* (bulan mm/yy, harga, volume, GAR), atau tempel/impor banyak baris sekaligus dalam format `mm/yy,harga,volume,gar`.
- Gunakan **Ekspor CSV** untuk cadangan atau memindahkan data ke perangkat lain.
- Data ICI di situs ini hanya berasal dari sumber yang sudah dipublikasikan terbuka (lihat kolom Sumber di tab *Data & sumber*); data ICI berlangganan dan HPB internal tidak dimuat.
- Kalkulator HPB adalah alat bantu estimasi. Koefisien koreksi kualitas perlu dicocokkan dengan lampiran Kepmen ESDM 72.K/MB.01/MEM.B/2025 (diubah 268.K/MB.01/MEM.B/2025) sebelum dipakai untuk royalti atau kontrak.

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
