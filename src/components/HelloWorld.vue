<template>
  <div>
    <h1>User Profile</h1>
    <div v-if="user">
      <p>Name: {{ user[0].name }}</p>
      <p>Email: {{ user[0].id }}</p>
    </div>
    <div v-else>
      <p>Loading...</p>
    </div>
  </div>
</template>

<script>
import { collection, getDocs } from "firebase/firestore";

import { db } from "../firebase";

export default {
  name: "HelloWorld",
  data() {
    return {
      user: null,
    };
  },
  async created() {
    const movieCollectionRef = collection(db, "users");
    try {
      const data = await getDocs(movieCollectionRef);
      console.log(data.doc);
      const filteredData = data.docs.map((doc) => {
        console.log(doc.data());
        return { ...doc.data(), id: doc.id };
      });
      this.user = filteredData;
    } catch (err) {
      console.error(err);
    }
  },
};
</script>

<style></style>
