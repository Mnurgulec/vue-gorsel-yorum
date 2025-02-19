<template>
  <div>
    <!-- NAVBAR -->
    <nav class="navbar navbar-default">
      <div class="container-fluid">
        <div class="navbar-header">
          <a class="navbar-brand" href="index.html">Facebook</a>
        </div>
        <ul class="nav navbar-nav navbar-right">
          <li><a href="home.html">Anasayfa</a></li>
          <li><a href="profile.html">Profil</a></li>
          <li><a href="#">Çıkış Yap</a></li>
        </ul>
      </div>
    </nav>

    <!-- MAIN -->
    <main class="container">
      <div class="row">
        <div class="col-md-3">
          <!-- Profile Brief -->
          <div class="panel panel-default">
            <div class="panel-body">
              <h4>Hoş Geldin</h4>
             <a href="profile.html">
                <img 
                  src="./assets/img/ben.jpg" 
                  alt="Makbule Nur GÜLEÇ" 
                  class="profil-resim"
                />
              </a>
              <p>Makbule Nur GÜLEÇ</p>
            </div>
          </div>
          <!-- Arkadaş İstekleri: Import edilen bileşeni kullanıyoruz -->
          <ArkadasIstekleri />
        </div>

        <div class="col-md-6">
          <!-- Post Form -->
          <form @submit.prevent="post">
            <div class="input-group">
              <input
                v-model="postContent"
                class="form-control"
                type="text"
                name="content"
                placeholder="Bir şeyler yaz."
              />
              <span class="input-group-btn">
                <button class="btn btn-success" type="submit" name="post">
                  Yayınla
                </button>
              </span>
            </div>
          </form>
          <hr />
          <!-- Feed -->
          <div>
            <div
              class="panel panel-default"
              v-for="(post, index) in posts"
              :key="index"
            >
              <div class="panel-body">
                <p>{{ post }}</p>
              </div>
              <div class="panel-footer">
                <span>
                  posted 2017-5-27 20:45:01 by nicholaskajoh
                </span>
                <span class="pull-right">
                  <a class="text-danger" href="#" @click.prevent="deletePost(index)">[delete]</a>
                </span>
              </div>
            </div>
          </div>
        </div>

        <div class="col-md-3">
          <!-- Add Friend -->
          <div class="panel panel-default">
            <div class="panel-body">
              <h4>Arkadaş Önerileri</h4>
              <ul>
                <li>
                  <a href="#">alberte</a>
                  <a href="#">[add]</a>
                </li>
              </ul>
            </div>
          </div>         
        </div>
      </div>
    </main>

    <!-- FOOTER -->
    <footer class="container text-center">
      <ul class="nav nav-pills pull-right">
      </ul>
    </footer>
  </div>
</template>

<script>
// ArkadasIstekleri bileşeni import ediliyor
import ArkadasIstekleri from './components/ArkadasIstekleri.vue';

export default {
  name: 'App',
  components: {
    // Bileşeni components içine ekleyerek kullanıma hazır hale getiriyoruz
    ArkadasIstekleri
  },
  data() {
    return {
      postContent: '',
      posts: ['Hello people! This is my first FaceClone post. Hurray!!!']
    }
  },
  methods: {
    post() {
      if (this.postContent.trim() !== '') {
        this.posts.push(this.postContent.trim())
        this.postContent = ''
      }
    },
    deletePost(index) {
      this.posts.splice(index, 1)
    }
  }
}
</script>

<style>
.profil-resim {
  width: 100px;
  height: auto;
  margin-bottom: 10px;
  align-center:
}
</style>
