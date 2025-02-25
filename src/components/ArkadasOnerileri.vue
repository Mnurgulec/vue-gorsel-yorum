<template>
    <div class="panel panel-default">
        <div class="panel-body">
        <h4>Arkadaş Önerileri</h4>
        <ul class="arkadas-listesi">

        <li v-for="(arkadas, index) in arkadaslar" :key="index">
          <span class="isim">{{ arkadas.isim }}</span>
          <button v-if="!arkadas.istekGonderildi" class="btn btn-soft" @click="istekGonder(index)">İstek Gönder
          </button>
          <span v-else class="istek-gonderildi"> istek gönderildi</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      arkadaslar: this.rastgeleArkadaslar()
    };
  },
  methods: {

    rastgeleArkadaslar()
     {

      const isimler = ["Ahmet", "zeynep", "mehmet", "elif", "burak", "merve", "talat", ];
      let liste = [];
      for (let i = 0; i < 3; i++) {
        let secilen = isimler[Math.floor(Math.random() * isimler.length)];
        liste.push({ isim: secilen, istekGonderildi: false });
      }

      return liste;
    },
    istekGonder(index) {
      this.arkadaslar[index].istekGonderildi = true;
    }
  }
};


</script>

<style scoped>
.panel {
  margin-top: 10px;
}

.arkadas-listesi {
  list-style: none;
  padding: 0;
}

.arkadas-listesi li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 8px;
  border-bottom: 1px solid #ddd;
}

.isim {
  font-weight: 500;
  color: #333;
}

.btn-soft {
  background-color: #e3f2fd;
  color: #1976d2;
  border: none;
  padding: 6px 12px;
  border-radius: 6px;
  cursor: pointer;
  transition: 0.3s ease;
  font-size: 14px;
}

.btn-soft:hover {
  background-color: #bbdefb;
}

.istek-gonderildi {
  color: #ff9800;
  font-weight: bold;
  font-size: 14px;
}
</style>
