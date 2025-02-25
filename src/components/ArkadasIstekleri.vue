<template>

  <div class="panel panel-default">
    <div class="panel-body">
      <h4>Arkadaş İstekleri</h4>
      <ul class="arkadas-listesi">
        <li v-for="(istek, i) in arkadasIstekleri" :key="i">
          <span class="isim">{{ istek.isim }}</span>
          <div class="butonlar">
             <button v-if="!istek.kabulEdildi" class="btn-soft btn-yesil" @click.prevent="kabul(i)">Kabul Et</button>
            <button v-if="!istek.kabulEdildi" class="btn-soft btn-kirmizi" @click.prevent="reddet(i)">Reddet</button>
            <span v-else class="kabul-edildi"> istek kabul edildi</span>
          </div>
        </li>
      </ul>
    </div>

  </div>

</template>

<script setup>
import { ref, onMounted } from 'vue'
const arkadasIstekleri = ref([])
const kaydet = () => localStorage.setItem('arkadasIstekleri', JSON.stringify(arkadasIstekleri.value))
const kabul = i => { arkadasIstekleri.value[i].kabulEdildi = true; kaydet() }
const reddet = i => { arkadasIstekleri.value.splice(i, 1); kaydet() }

const isimler = ['Umut', 'Kürşat', 'Talat', 'Nur', 'Makbule']

onMounted(() => {
  const kayit = localStorage.getItem('arkadasIstekleri')
  arkadasIstekleri.value = kayit ? JSON.parse(kayit) : [{ isim: 'John Doe', kabulEdildi: false }, { isim: 'Jane Doe', kabulEdildi: false }]
 
  arkadasIstekleri.value.push({ isim: isimler[Math.floor(Math.random() * isimler.length)], kabulEdildi: false })
  kaydet()
})
</script>

<style scoped>
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

.butonlar {
  display: flex;
  gap: 8px;
}

.btn-soft {
  background-color: #e3f2fd;
  border: none;
  padding: 6px 12px;
  border-radius: 6px;
  cursor: pointer;
  transition: 0.3s ease;
  font-size: 14px;
  font-weight: 500;
  text-align: center;
}


.btn-yesil {
  color: #4caf50;
  border: 1px solid #4caf50;
}

.btn-yesil:hover {
  background-color: #4caf50;
  color: white;
}


.btn-kirmizi {
  color: #f44336;
  border: 1px solid #f44336;
}

.btn-kirmizi:hover {
  background-color: #f44336;
  color: white;
}

.kabul-edildi {
  color: #4caf50;
  font-weight: bold;
  font-size: 14px;
}
</style>
