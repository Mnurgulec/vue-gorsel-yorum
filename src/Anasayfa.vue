<template>
  <div>
    <nav class="navbar navbar-default">
      <div class="container-fluid">
        <div class="navbar-header">
          <a class="navbar-brand" href="index.html">Facebook</a>
        </div>
        <ul class="nav navbar-nav navbar-right">
          <li><a href="home.html">Anasayfa</a></li>

        </ul>
      </div>
    </nav>

    <main class="container">
      <div class="row">
        <!-- Sol Sidebar (Profil + Arkadaş İstekleri) -->
        <div class="col-md-3">

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
                  Makbule Nur GÜLEÇ tarafından gönderildi
                </span>
                <span class="pull-right">
                  <button class="btn btn-sm btn-danger" @click.prevent="deletePost(index)">Sil</button>
                </span>
              </div>
            </div>
          </div>
        </div>


        <div class="col-md-3">
          <ArkadasOnerileri />
        </div>
      </div>
    </main>

    <footer class="container text-center">
      <ul class="nav nav-pills pull-right"></ul>
    </footer>
  </div>
</template>

<script>
import ArkadasIstekleri from './components/ArkadasIstekleri.vue';
import ArkadasOnerileri from './components/ArkadasOnerileri.vue';

export default {
  name: 'App',
  components: {
    ArkadasIstekleri,
    ArkadasOnerileri
  },
  data() {
    return {
      postContent: '',
      posts: ['İlk Yorum']
    };
  },
  methods: {
    post() {
      if (this.postContent.trim() !== '') {
        this.posts.push(this.postContent.trim());
        this.postContent = '';
      }
    },
    deletePost(index) {
      this.posts.splice(index, 1);
    }
  }
};
</script>

<style>
.profil-resim {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  object-fit: cover;
  margin: 0 auto;
  display: block;
  border: 2px solid #ddd;
}

.panel-body {
  text-align: center;
}

.panel-body p {
  font-size: 16px;
  font-weight: bold;
  color: #333;
  margin-top: 8px;
}
</style>
