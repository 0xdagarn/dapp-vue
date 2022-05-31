<template>
  <div>
    <h3>PLEASE USE RINKEBY TEST NETWORK</h3>
    <button @click="connect">connect</button>
    <button @click="buyDev">buyDev</button>
    <button @click="revealDev">revealDev</button>
  </div>
</template>

<script>
import { ethers } from "ethers";

// contract
const packageAddress = "0x73138087570118460Bc7ed3cE49E6CC595477875";
const packageAbi = [
  "function buyDev() payable",
  "function revealDev()",
];
const packageContract = new ethers.Contract(packageAddress, packageAbi);

// helper functions
const isConnected = async () => {
  const accounts = await window.ethereum.request({ method: 'eth_accounts' });
  return accounts.length !== 0;
}

let provider;
let signer;

export default {
  name: "Package",
  methods: {
    connect: async function () {
      if (typeof window.ethereum !== 'undefined') {
        try {
          // https://docs.ethers.io/v5/getting-started/#getting-started--connecting
          provider = new ethers.providers.Web3Provider(window.ethereum);

          await provider.send("eth_requestAccounts", []);
          signer = provider.getSigner();
        } catch (err) {
          // user rejected the request
          console.log("err: %s", err.message);
        }
      } else {
        console.log("metamask is not installed.");
      }
    },
    buyDev: async function () {
      if (!await isConnected()) return alert("CONNECT FIRST!");

      const tx = await packageContract.connect(signer).buyDev();
      console.log(tx);

      const receipt = await tx.wait();
      console.log(receipt);
    },
    revealDev: async function () {
      if (!await isConnected()) return alert("CONNECT FIRST!");

      const tx = await packageContract.connect(signer).revealDev();
      console.log(tx);

      const receipt = await tx.wait();
      console.log(receipt);
    },
  }
}
</script>

<style scoped>
</style>
