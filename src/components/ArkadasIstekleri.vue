<template>
  <div class="panel panel-default">
    <div class="panel-body">
      <h4>Arkadaş İstekleri</h4>
      <ul>
        <li v-for="(istek, i) in arkadasIstekleri" :key="i">
          <a href="#">{{ istek.isim }}</a>
          <template v-if="!istek.kabulEdildi">
            <a class="text-success" href="#" @click.prevent="kabul(i)">[Kabul Et]</a>
            <a class="text-danger" href="#" @click.prevent="reddet(i)">[Reddet]</a>
          </template>
          <template v-else>
            <span class="text-success">[Kabul Edildi]</span>
          </template>
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
const isimler = ['umut','kürşat','talat','nur','makbule']

onMounted(() => {
  const kayit = localStorage.getItem('arkadasIstekleri')
  arkadasIstekleri.value = kayit ? JSON.parse(kayit) : [{ isim: 'johndoe', kabulEdildi: false }, { isim: 'janedoe', kabulEdildi: false }]
 
  arkadasIstekleri.value.push({ isim: isimler[Math.floor(Math.random() * isimler.length)], kabulEdildi: false })
  kaydet()
})
</script>

<style scoped>
ul { 
    padding: 0; list-style: none; 
    }

li { 
    margin-bottom: 8px; 
    }
    
.text-success, .text-danger {
    display: inline-block; padding: 5px 10px; margin-left: 10px;
    border: 1px solid; border-radius: 4px; text-decoration: none;
}

.text-success { 
    border-color: green; color: green;
     }
.text-danger {
     border-color: red; color: red; 
     }

.text-success:hover { 
    background: green; color: white; 
    }
.text-danger:hover { 
    background: red; color: white;
     }


</style>
