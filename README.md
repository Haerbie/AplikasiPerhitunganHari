# Tugas 4: Aplikasi Perhitungan Hari

### Pembuat
- **Nama**: Muhammad Irwan Habibie
- **NPM**: 2210010461

---

## 1. Deskripsi Program
Aplikasi ini memungkinkan pengguna untuk:
- Memilih bulan dan memasukkan tahun menggunakan **JComboBox** dan **JSpinner**.
- Menggunakan **JCalendar** untuk memilih bulan dan tahun secara langsung.
- Menghitung jumlah hari dalam bulan tertentu pada tahun yang dipilih.
- Menampilkan hasil perhitungan setelah tombol **Hitung Jumlah Hari** ditekan.

## 2. Komponen GUI
- **JFrame**: Window utama aplikasi.
- **JPanel**: Panel untuk menampung komponen.
- **JLabel**: Label untuk menunjukkan informasi jumlah hari, hari pertama, dan hari terakhir.
- **JComboBox**: Dropdown untuk memilih bulan.
- **JSpinner**: Input angka untuk memilih tahun.
- **JButton**: Tombol untuk memulai perhitungan jumlah hari.
- **JCalendar**: Kalender untuk memilih tanggal secara interaktif.

## 3. Logika Program
- Menggunakan API **LocalDate** untuk menghitung jumlah hari dalam bulan dan tahun yang dipilih.
- Menghitung apakah tahun yang dipilih adalah tahun kabisat.
- Mendapatkan hari pertama dan hari terakhir dari bulan yang dipilih, serta menampilkannya dalam bahasa Indonesia.

## 4. Events
Menggunakan **ActionListener** dan **ChangeListener** untuk menangani interaksi pengguna:

### A. Tombol Hitung
Menghitung jumlah hari dalam bulan yang dipilih, hari pertama, hari terakhir, dan menampilkan informasi tambahan jika tahun adalah tahun kabisat.

    private void HitungActionPerformed(java.awt.event.ActionEvent evt) {                                       
        String bulan = bulanComboBox.getSelectedItem().toString();
        int tahun = (int) tahunSpinner.getValue();
        int bulanIndex = bulanComboBox.getSelectedIndex() + 1;

        java.time.YearMonth yearMonth = java.time.YearMonth.of(tahun, bulanIndex);
        int jumlahHari = yearMonth.lengthOfMonth();
        java.time.LocalDate hariPertama = yearMonth.atDay(1);
        java.time.LocalDate hariTerakhir = yearMonth.atEndOfMonth();

        boolean isLeapYear = java.time.Year.isLeap(tahun);
        String kabisatMessage = isLeapYear ? " (Tahun Kabisat)" : "";
        String hariPertamaIndonesia = getHariDalamBahasaIndonesia(hariPertama.getDayOfWeek());
        String hariTerakhirIndonesia = getHariDalamBahasaIndonesia(hariTerakhir.getDayOfWeek());

        String hasilPesan = String.format(
            "Jumlah hari: %d%s\nHari pertama: %s\nHari terakhir: %s",
            jumlahHari, kabisatMessage, hariPertamaIndonesia, hariTerakhirIndonesia
        );
        JOptionPane.showMessageDialog(this, hasilPesan);
    }  

### B. ChangeListener pada JSpinner
Mendeteksi perubahan tahun untuk memperbarui kalender secara dinamis.

## 5. Variasi
Aplikasi ini memiliki variasi tambahan berikut:

### A. Hari Pertama dan Hari Terakhir
Menampilkan informasi hari pertama dan hari terakhir dari bulan yang dipilih dalam bahasa Indonesia.

      private String getHariDalamBahasaIndonesia(java.time.DayOfWeek dayOfWeek) {
        switch (dayOfWeek) {
            case MONDAY:
                return "Senin";
            case TUESDAY:
                return "Selasa";
            case WEDNESDAY:
                return "Rabu";
            case THURSDAY:
                return "Kamis";
            case FRIDAY:
                return "Jumat";
            case SATURDAY:
                return "Sabtu";
            case SUNDAY:
                return "Minggu";
            default:
                return "";
        }
    }
    String hariPertamaIndonesia = getHariDalamBahasaIndonesia(hariPertama.getDayOfWeek());
    String hariTerakhirIndonesia = getHariDalamBahasaIndonesia(hariTerakhir.getDayOfWeek());

### B. Menghitung Selisih Hari antara Dua Tanggal
Menambahkan fitur untuk menghitung selisih hari antara dua tanggal yang dipilih di **JCalendar**.

    private void hitungSelisihButtonActionPerformed(java.awt.event.ActionEvent evt) {                                                    
        java.util.Date tanggalMulai = jCalendarMulai.getDate();
        java.util.Date tanggalAkhir = jCalendarAkhir.getDate();

        if (tanggalMulai != null && tanggalAkhir != null) {
            java.time.LocalDate mulai = tanggalMulai.toInstant().atZone(java.time.ZoneId.systemDefault()).toLocalDate();
            java.time.LocalDate akhir = tanggalAkhir.toInstant().atZone(java.time.ZoneId.systemDefault()).toLocalDate();

            long selisihHari = java.time.temporal.ChronoUnit.DAYS.between(mulai, akhir);
            String hasilPesan = "Selisih hari: " + Math.abs(selisihHari) + " hari";
            hasilLabel.setText(hasilPesan);
            JOptionPane.showMessageDialog(this, hasilPesan, "Hasil Selisih Hari", JOptionPane.INFORMATION_MESSAGE);
        } else {
            JOptionPane.showMessageDialog(this, "Pilih tanggal mulai dan akhir terlebih dahulu.", "Kesalahan", JOptionPane.WARNING_MESSAGE);
        }
    }  

## 6. Tampilan Aplikasi Saat di Run
![TampilanPerhitunganHari](https://github.com/user-attachments/assets/4af886fb-08aa-4dcd-9a25-2f54a6d5d8ae)

## 7. Indikator Penilaian

| No  | Komponen          | Persentase |
| :-: | ------------------ | :--------: |
|  1  | Komponen GUI      |     10%    |
|  2  | Logika Program    |     20%    |
|  3  | Events            |     20%    |
|  4  | Kesesuaian UI     |     20%    |
|  5  | Memenuhi Variasi  |     30%    |
|     | **TOTAL**         |  **100%**  |

--- 
