<template>
  <div class="container">
    <b-form>
      <b-form-group label="NPWP">
        <b-form-checkbox></b-form-checkbox>
      </b-form-group>
      <b-form-group label="Status Perkawinan">
        <b-form-radio name="statusPerkawinan">Kawin</b-form-radio>
        <b-form-radio name="statusPerkawinan">Tidak Kawin</b-form-radio>
      </b-form-group>
      <b-form-group label="Jumlah Tanggungan">
        <b-form-radio name="jumlahTanggungan">0</b-form-radio>
        <b-form-radio name="jumlahTanggungan">1</b-form-radio>
        <b-form-radio name="jumlahTanggungan">2</b-form-radio>
        <b-form-radio name="jumlahTanggungan">3</b-form-radio>
      </b-form-group>
      <b-form-group label="Gaji Pokok">
        <b-form-input required placeholder="Gaji Pokok"></b-form-input>
      </b-form-group>
      <b-form-group label="Tunjangan">
        <b-form-input required placeholder="Tunjangan"></b-form-input>
      </b-form-group>
      <b-form-group label="BPJS Kesehatan oleh Perusahaan (4%)">
        <b-form-input readonly></b-form-input>
      </b-form-group>
      <b-form-group label="Jaminan Kecelakaan Kerja (JKK) oleh Perusahaan (0.24%)">
        <b-form-input readonly></b-form-input>
      </b-form-group>
      <b-form-group label="Jaminan Kematian (JK) oleh Perusahaan (0.3%)">
        <b-form-input readonly></b-form-input>
      </b-form-group>
      <b-form-group label="Total Penghasilan Bruto per Bulan">
        <b-form-input readonly></b-form-input>
      </b-form-group>
      <b-form-group label="Total Penghasilan Bruto per Tahun">
        <b-form-input readonly></b-form-input>
      </b-form-group>
      <b-form-group label="BPJS Kesehatan oleh Karyawan (1%)">
        <b-form-input readonly></b-form-input>
      </b-form-group>
      <b-form-group label="Iuran Jaminan Hari Tua (JHT) oleh Karyawan (2%)">
        <b-form-input readonly>
        </b-form-input>
      </b-form-group>
      <b-form-group label="Iuran Jaminan Pensiun (JP) oleh Karyawan (1%)">
        <b-form-input readonly>
        </b-form-input>
      </b-form-group>
      <b-form-group label="Penghasilan Tidak Kena Pajak (PTKP)">
        <b-form-input readonly>
        </b-form-input>
      </b-form-group>
      <b-form-group label="Penghasilan Kena Pajak (PKP)">
        <b-form-input readonly>
        </b-form-input>
      </b-form-group>
      <b-form-group label="PPh 21 terutang setahun">
        <b-form-input readonly>
        </b-form-input>
      </b-form-group>
      <b-form-group label="PPh 21 terutang per bulan">
        <b-form-input readonly>
        </b-form-input>
      </b-form-group>
    </b-form>
  </div>
</template>

<script>
export default {}
</script>


