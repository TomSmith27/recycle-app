<template>
  <div class="main">
    <nav class="navbar navbar-expand-md navbar-dark bg-secondary">
      <a class="navbar-brand" href="#">Recycle Sheffield</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarsExampleDefault"
        aria-controls="navbarsExampleDefault"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarsExampleDefault">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
            <a class="nav-link" href="#">
              Home
              <span class="sr-only">(current)</span>
            </a>
          </li>
        </ul>
      </div>
    </nav>

    <main role="main" class="container">
      <div class="starter-template">
        <div class="container">
          <div class="row">
            <div class="col-xl-9 mx-auto">
              <h1 class="mb-5 text-light">Where can I recycle?...</h1>
              <select class="form-control form-control-lg" v-model="selectedItem">
                <option value disabled selected>-- select an option --</option>
                <option>Eggs</option>
                <option>Plastic</option>
              </select>
              <h2 class="text-light">in</h2>
              <select placeholder="item" class="form-control form-control-lg">
                <option value>Sheffield</option>
              </select>
            </div>
          </div>
          <div class="pt-4 row">
            <div class="col-xl-9 mx-auto">
              <b-button block variant="primary">Search</b-button>
            </div>
          </div>
          <div v-if="selectedItem">
            <div class="mt-5 row">
              <div class="col-xl-9 mx-auto">
                <h2 class="text-light">{{results.length}} Results for {{selectedItem}}</h2>
              </div>
            </div>
            <div class="row" v-if="results.length > 0">
              <div class="col-xl-9 mx-auto">
                <b-card-group deck>
                  <b-card :key="res.name" v-for="res in results" no-body class="overflow-hidden">
                    <b-row no-gutters>
                      <b-col md="6">
                        <b-card-img :src="res.img" class="rounded-0" style="width : 100px; height :100px"></b-card-img>
                      </b-col>
                      <b-col md="6">
                        <b-card-body :title="res.name">
                          <b-card-text>
                            <b-badge class="mx-2 py-2" :key="tag" v-for="tag in res.tags" variant="primary">{{tag}}</b-badge>
                          </b-card-text>
                        </b-card-body>
                      </b-col>
                    </b-row>
                  </b-card>

                  <!--    <b-card :key="res.name" v-for="res in results" :title="res.name" :img-src="res.img" img-alt="Image" img-top tag="article" style="max-width: 15rem;" class="mb-2">
                    <b-card-text>
                      <b-badge class="mx-2 py-2" :key="tag" v-for="tag in res.tags" variant="primary">{{tag}}</b-badge>
                    </b-card-text>
                  </b-card>-->
                </b-card-group>
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>
<script>
import data from "./data.json";
export default {
  name: "App",
  data() {
    return {
      selectedItem: ""
    };
  },
  computed: {
    results() {
      return data.filter(t => t.tags.includes(this.selectedItem));
    }
  }
};
</script>

<style lang="scss">
body {
  background-color: #343a40 !important;
}
main {
  margin-top: 20px;
  text-align: center;
}
</style>
