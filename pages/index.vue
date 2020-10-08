<template>
  <div class="container">
    <b-form>
      <b-form-group label="Memiliki NPWP">
        <b-form-checkbox v-model="hasNPWP"></b-form-checkbox>
      </b-form-group>
      <b-form-group label="Status Perkawinan">
        <b-form-radio name="statusPerkawinan" v-model="statusPerkawinan" value="0">Tidak Kawin</b-form-radio>
        <b-form-radio name="statusPerkawinan" v-model="statusPerkawinan" value="1">Kawin</b-form-radio>
      </b-form-group>
      <b-form-group label="Jumlah Tanggungan">
        <b-form-radio name="jumlahTanggungan" v-model="jumlahTanggungan" value="0">0</b-form-radio>
        <b-form-radio name="jumlahTanggungan" v-model="jumlahTanggungan" value="1">1</b-form-radio>
        <b-form-radio name="jumlahTanggungan" v-model="jumlahTanggungan" value="2">2</b-form-radio>
        <b-form-radio name="jumlahTanggungan" v-model="jumlahTanggungan" value="3">3</b-form-radio>
      </b-form-group>
      <b-form-group label="Gaji Pokok">
        <b-form-input required type="number" placeholder="Gaji Pokok" v-model.number="gajiPokok"></b-form-input>
      </b-form-group>
      <b-form-group label="Tunjangan">
        <b-form-input required type="number" placeholder="Tunjangan" v-model.number="tunjangan"></b-form-input>
      </b-form-group>
      <b-form-group label="Gaji yang dilaporkan di BPJS Ketenagakerjaan">
        <b-form-input required type="number" placeholder="Gaji yang dilaporkan di BPJS Ketenagakerjaan" v-model.number="gajiBPJSTk"></b-form-input>
      </b-form-group>
      <b-form-group label="BPJS Kesehatan oleh Perusahaan (4%)">
        <b-form-input readonly v-model="calculateBPJSKesP"></b-form-input>
      </b-form-group>
      <b-form-group label="Jaminan Kecelakaan Kerja (JKK) dibayarkan oleh Perusahaan (0.24%)">
        <b-form-input readonly v-model="jkk"></b-form-input>
      </b-form-group>
      <b-form-group label="Jaminan Kematian (JK) dibayarkan oleh Perusahaan (0.3%)">
        <b-form-input readonly v-model="jk"></b-form-input>
      </b-form-group>
      <b-form-group label="Total Penghasilan Bruto per Tahun">
        <b-form-input readonly v-model="totalBruto"></b-form-input>
      </b-form-group>
      <b-form-group label="Biaya Jabatan (5%)">
        <b-form-input readonly v-model="biayaJabatan"></b-form-input>
      </b-form-group>
      <b-form-group label="BPJS Kesehatan dibayarkan oleh Karyawan (1%)">
        <b-form-input readonly v-model="calculateBPJSKesK"></b-form-input>
      </b-form-group>
      <b-form-group label="Iuran Jaminan Hari Tua (JHT) dibayarkan oleh Karyawan (2%)">
        <b-form-input readonly v-model="jht"></b-form-input>
      </b-form-group>
      <b-form-group label="Iuran Jaminan Pensiun (JP) oleh Karyawan (1%)">
        <b-form-input readonly v-model="jp"></b-form-input>
      </b-form-group>
      <b-form-group label="Total Pengurangan">
        <b-form-input readonly v-model="totalPengurangan"></b-form-input>
      </b-form-group>
      <b-form-group label="Penghasilan Tidak Kena Pajak (PTKP)">
        <b-form-input readonly v-model="calculatePTKP"></b-form-input>
      </b-form-group>
      <b-form-group label="Penghasilan Kena Pajak (PKP)">
        <b-form-input readonly v-model="pkp"></b-form-input>
      </b-form-group>
      <b-form-group label="PPh 21 terutang setahun">
        <b-form-input readonly v-model="pphSetahun"></b-form-input>
      </b-form-group>
      <b-form-group label="PPh 21 terutang per bulan">
        <b-form-input readonly v-model="pphSebulan"></b-form-input>
      </b-form-group>
    </b-form>
  </div>
</template>

<script>
export default {
  data () {
    return {
      hasNPWP: true,
      statusPerkawinan: 0,
      jumlahTanggungan: 0,
      gajiPokok: 0,
      tunjangan: 0,
      gajiBPJSTk: 0,
      bpjskesP: 0,
      jkk: 0,
      jk: 0,
      totalBruto: 0,
      biayaJabatan: 0,
      bpjskesK: 0,
      jht: 0,
      jp: 0,
      totalPengurangan: 0,
      ptkp: 0,
      pkp: 0,
      pphSetahun: 0,
      pphSebulan: 0
    }
  },
  computed: {
    calculatePTKP() {
      const ptkp = 54000000
      const tambahan = 4500000
      const total = ptkp + this.jumlahTanggungan * tambahan
      if (this.statusPerkawinan == 1)
        return total + tambahan
      else 
        return total
    },
    calculateGajiBPJSKes() {
      const limitGajiBPJSKes = 12000000
      let gaji = this.gajiPokok + this.tunjangan
      if (gaji > limitGajiBPJSKes)
        return limitGajiBPJSKes
      else return gaji
    },
    calculateBPJSKesP() {
      return this.calculateGajiBPJSKes * 4/100
    },
    calculateBPJSKesK() {
      return this.calculateGajiBPJSKes * 1/100
    }
  }
}
</script>


