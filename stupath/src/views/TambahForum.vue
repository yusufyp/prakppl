<template>
  <div>
    <Navbar />
    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="display-4">Tambah Topik Forum</h1>
        <p class="lead">
          Forum yang akan digunakan
          <br />
          untuk berdiskusi seputar pekerjaan / materi sesama pengguna
        </p>
      </div>
    </div>

    <div class="tambah-diskusi">
      <p>Nama Pekerjaan</p>
      <input
        v-model="dataForum.pekerjaan"
        type="text"
        placeholder="Nama Pekerjaan"
        name="judul"
        required
      />

      <p>Judul</p>
      <input
        v-model="dataForum.judul"
        type="text"
        placeholder="Judul"
        name="judul"
        required
      />

      <p>Deskripsi</p>
      <textarea
        v-model="dataForum.deskripsi"
        placeholder="Deskripsi"
        name="isidiskusi"
      ></textarea>

      <button @click="tambahForum">Tambahkan Topik</button>
    </div>
  </div>
</template>

<script>
import Navbar from "../components/Navbar";
import firebase from "../firebase";
import { mapState } from "vuex";

export default {
  components: {
    Navbar
  },

  data() {
    return {
      dataForum: {
        judul: "",
        deskripsi: "",
        pekerjaan: "",
        username: "",
        balasan: []
      }
    };
  },

  methods: {
    async tambahForum() {
      this.dataForum.username = this.userProfile.username;
      let data = this.dataForum;

      try {
        await firebase.db
          .collection("forum")
          .doc()
          .set(data);
      } catch (error) {
        console.log(error);
      }

      this.dataForum.judul = "";
      this.dataForum.deskripsi = "";
      this.dataForum.pekerjaan = "";
      this.$router.push("/forum");
    }
  },
  computed: mapState(["userProfile"])
};
</script>

<style scoped>
.judul-halaman {
  font-size: 50px;
  color: white;
  font-weight: bold;
  margin-top: -85px;
  margin-left: 95px;
}

.tambah-diskusi {
  margin-top: -65px;
  padding: 80px;
}
.tambah-diskusi p {
  font-weight: 900;
  font-size: 26px;
  line-height: 56px;
  color: #000000;
  margin: 25px 0px;
}
.tambah-diskusi input {
  outline: none;
  width: 70%;
  height: 70px;
  font-weight: normal;
  font-size: 20px;
  border: none;
  color: #000000;
  padding-left: min(5%, 38px);
  background: #f7f7f7;
}
.tambah-diskusi textarea {
  font-family: "Roboto", sans-serif;
  width: 70%;
  height: 200px;
  font-weight: normal;
  font-size: 18px;
  line-height: 21px;
  color: #000000;
  background: #f7f7f7;
  border: none;
  padding: 37px;
}
.tambah-diskusi button {
  display: flex;
  margin-top: 50px;
  font-weight: bold;
  font-size: 22px;
  border: none;
  line-height: 42px;
  padding: 10px 40px;
  color: #ffffff;
  background: #00918e;
  border-radius: 12px;
}
</style>
