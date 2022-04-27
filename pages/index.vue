<template>
  <div class="container">
    <b-form>
      <div class="row">
        <div class="col-md">
          <b-form-group label="Memiliki NPWP">
            <b-form-checkbox v-model="punyaNPWP"></b-form-checkbox>
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
          <b-form-group label="Gaji Pokok per bulan">
            <b-form-input required type="number" placeholder="Gaji Pokok" v-model.number="gajiPokok"></b-form-input>
          </b-form-group>
          <b-form-group label="Tunjangan">
            <b-form-input required type="number" placeholder="Tunjangan" v-model.number="tunjangan"></b-form-input>
          </b-form-group>
          <b-form-group label="Gaji yang dilaporkan di BPJS Ketenagakerjaan">
            <b-form-input required type="number" placeholder="Gaji yang dilaporkan di BPJS Ketenagakerjaan" v-model.number="gajiBPJSTk"></b-form-input>
          </b-form-group>
          <b-form-group label="BPJS Kesehatan oleh Perusahaan (4%)">
            <b-form-input readonly :value="formatCurrency(calculateBPJSKesP)"></b-form-input>
          </b-form-group>
          <b-form-group label="Resiko pekerjaan">
            <b-form-radio name="persentaseJkk" v-model.number="persentaseJkk" value="0.24">Resiko sangat rendah</b-form-radio>
            <b-form-radio name="persentaseJkk" v-model.number="persentaseJkk" value="0.54">Resiko rendah</b-form-radio>
            <b-form-radio name="persentaseJkk" v-model.number="persentaseJkk" value="0.89">Resiko sedang</b-form-radio>
            <b-form-radio name="persentaseJkk" v-model.number="persentaseJkk" value="1.27">Resiko tinggi</b-form-radio>
            <b-form-radio name="persentaseJkk" v-model.number="persentaseJkk" value="1.74">Resiko sangat tinggi</b-form-radio>
          </b-form-group>
          <b-form-group :label="'Jaminan Kecelakaan Kerja (JKK) dibayarkan oleh Perusahaan (' + persentaseJkk + '%)'">
            <b-form-input readonly :value="formatCurrency(calculateJKK)"></b-form-input>
          </b-form-group>
          <b-form-group label="Jaminan Kematian (JKM) dibayarkan oleh Perusahaan (0.3%)">
            <b-form-input readonly :value="formatCurrency(calculateJKM)"></b-form-input>
          </b-form-group>
          <b-form-group label="Total Penghasilan Bruto per Bulan">
            <b-form-input readonly  :value="formatCurrency(calculateTotalPenghasilanPerBulan)"></b-form-input>
          </b-form-group>
          <b-form-group label="Total Penghasilan Bruto per Tahun">
            <b-form-input readonly  :value="formatCurrency(calculateTotalPenghasilanBruto)"></b-form-input>
          </b-form-group>
        </div>
        <div class="col-md">
          <b-form-group label="Biaya Jabatan (5%)">
            <b-form-input readonly :value="formatCurrency(calculateBiayaJabatan)"></b-form-input>
          </b-form-group>
          <b-form-group label="Iuran Jaminan Hari Tua (JHT) dibayarkan oleh Karyawan (2%)">
            <b-form-input readonly :value="formatCurrency(calculateJHT)"></b-form-input>
          </b-form-group>
          <b-form-group label="Iuran Jaminan Pensiun (JP) oleh Karyawan (1%)">
            <b-form-input readonly :value="formatCurrency(calculateJP)"></b-form-input>
          </b-form-group>
          <b-form-group label="BPJS Kesehatan oleh Karyawan (1%)">
            <b-form-input readonly :value="formatCurrency(calculateBPJSKesK)"></b-form-input>
          </b-form-group>
          <b-form-group label="Total Pengurangan">
            <b-form-input readonly :value="formatCurrency(calculateTotalPengurangan)"></b-form-input>
          </b-form-group>
          <b-form-group label="Total Penghasilan Neto per Tahun">
            <b-form-input readonly :value="formatCurrency(calculateTotalPenghasilanNeto)"></b-form-input>
          </b-form-group>
          <b-form-group label="Penghasilan Tidak Kena Pajak (PTKP)">
            <b-form-input readonly :value="formatCurrency(calculatePTKP)"></b-form-input>
          </b-form-group>
          <b-form-group label="Penghasilan Kena Pajak (PKP)">
            <b-form-input readonly :value="formatCurrency(calculatePKP)"></b-form-input>
          </b-form-group>
          <b-form-group label="PPh 21 terutang setahun">
            <b-form-input readonly :value="formatCurrency(calculatePPh)"></b-form-input>
          </b-form-group>
          <b-form-group label="PPh 21 terutang per bulan">
            <b-form-input readonly :value="formatCurrency(calculatePPhBulanan)"></b-form-input>
          </b-form-group>
        </div>
      </div>
    </b-form>
  </div>
</template>

<script>
export default {
  data () {
    return {
      punyaNPWP: true,
      statusPerkawinan: 0,
      jumlahTanggungan: 0,
      gajiPokok: 0,
      tunjangan: 0,
      gajiBPJSTk: 0,
      bpjskesP: 0,
      persentaseJkk: 0.24,
      jkk: 0,
      jkm: 0,
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
  methods: {
    formatCurrency(amount) {
      return new Intl.NumberFormat('id-ID', { style: 'currency', currency: 'IDR' }).format(amount)
    }
  },
  computed: {
    calculateTotalGaji() {
      return this.gajiPokok + this.tunjangan
    },
    calculatePTKP() {
      const ptkp = 54_000_000
      const tambahan = 4_500_000
      const total = ptkp + this.jumlahTanggungan * tambahan
      if (this.statusPerkawinan == 1)
        return total + tambahan
      else 
        return total
    },
    calculateGajiBPJSKes() {
      const limitGajiBPJSKes = 12_000_000
      if (this.calculateTotalGaji > limitGajiBPJSKes)
        return limitGajiBPJSKes
      else 
        return this.calculateTotalGaji
    },
    calculateBPJSKesP() {
      return Math.floor(this.calculateGajiBPJSKes * 4/100)
    },
    calculateBPJSKesK() {
      return Math.ceil(this.calculateGajiBPJSKes * 1/100)
    },
    calculateJKK() {
      return Math.ceil(this.calculateTotalGaji * this.persentaseJkk/100)
    },
    calculateJKM() {
      return Math.ceil(this.calculateTotalGaji * 0.3/100)
    },
    calculateTotalPenghasilanPerBulan(){
      return (this.calculateTotalGaji + this.calculateBPJSKesP + this.calculateJKK + this.calculateJKM)
    },
    calculateTotalPenghasilanBruto() {
     return this.calculateTotalPenghasilanPerBulan * 12
    },
    calculateBiayaJabatan() {
      const biayaJabatan = this.calculateTotalPenghasilanBruto * 0.5/100 * 12
      const limitBiayaJabatan = 6000000
      if (biayaJabatan > limitBiayaJabatan)
        return limitBiayaJabatan
      else
        return biayaJabatan
    },
    calculateJHT() {
      return Math.ceil(this.calculateTotalGaji * 2/100)
    },
    calculateJP() {
      return (this.gajiPokok > 9_077_600 ? 9_077_600 : this.gajiPokok) * 1/100
    },
    calculateTotalPengurangan() {
      return this.calculateBiayaJabatan + (this.calculateJHT + this.calculateJP) * 12
    },
    calculateTotalPenghasilanNeto() {
      return this.calculateTotalPenghasilanBruto - this.calculateTotalPengurangan
    },
    calculatePKP() {
      if (this.calculateTotalPenghasilanNeto <= this.calculatePTKP )
        return 0
      else
        return Math.floor((this.calculateTotalPenghasilanNeto - this.calculatePTKP) / 1000) *   1000
    },
    calculatePPh() {

      const tarif = [5/100, 15/100, 25/100, 30/100, 35/100]
      const pkp = this.calculatePKP
      const penghasilan = [60_000_000, 250_000_000, 500_000_000, 5000_000_000]
      let pph = 0

      if (pkp <= penghasilan[0])
        pph = pkp * tarif[0] 
      else if (pkp > penghasilan[0] && pkp <= penghasilan[1])
        pph = (penghasilan[0] * tarif[0]) + ((pkp - penghasilan[0]) * tarif[1])
      else if (pkp > penghasilan[1] && pkp <= penghasilan[2])
        pph = (penghasilan[0] * tarif[0]) + ((pkp - penghasilan[0]) * tarif[1]) 
              + ((pkp - penghasilan[0] - penghasilan[1]) * tarif[2])
      else if (pkp > penghasilan[2])
        pph = (penghasilan[0] * tarif[0]) + ((pkp - penghasilan[0]) * tarif[1]) 
              + ((pkp - penghasilan[0] - penghasilan[1]) * tarif[2]) 
              + (pkp - penghasilan[0] - penghasilan[1] - penghasilan[2]) * tarif[3]

      //Untuk Wajib Pajak yang tidak memiliki NPWP, dikenai tarif 20% lebih tinggi dari mereka yang memiliki NPWP.
      if (this.punyaNPWP == 0)
        pph = pph * 120/100
      
      return pph
    },
    calculatePPhBulanan() {
      return Math.ceil(this.calculatePPh / 12)
    }
  }
}
</script>


