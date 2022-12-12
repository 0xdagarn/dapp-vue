<template>
  <div>
    Test
  </div>
</template>

<script>
import { Seaport } from "@opensea/seaport-js";
import { ethers } from "ethers";

const provider = new ethers.providers.Web3Provider(window.ethereum);
const seaport = new Seaport(provider);

export default {
  name: "Seaport",
  methods: {
  },
}
</script>

<style scoped>
</style>
