
<template>
  <div class="wrapper flex">
    <div class="box-panel">
      <h1>Romaji 2 Kana</h1>
      <form>
        <div class="col">
          <label>Romaji</label>
          <input class="input" id="romaji" name="romaji" v-model="romajiInput" v-on:keyup="convert" />
        </div>

        <div class="col">
          <label>Hiragana</label>
          <div class="output">{{output.h}}</div>
        </div>

        <div class="col">
          <label>Katakana</label>
          <div class="output">{{output.k}}</div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>

const kanaHash = require("@/assets/kana.json");
export default {
  name: "Romaji2Kana",
  methods: {
    findHash() {
      while (this.hashMaxLen > 0 && !this.hashExists) {
        const end = this.start + this.hashMaxLen,
          hashKey = this.romaji.substring(this.start, end),
          hashItem = this.kanaHash[hashKey];

        if (hashItem != null) {
          this.input.h += hashItem.h;
          this.input.k += hashItem.k;
          this.start += this.hashMaxLen;
          this.hashExists = true;
        }

        this.hashMaxLen--;
      }
    },

    resetVars() {
      this.romaji = this.romajiInput.toLowerCase();
      this.start = 0;
      this.input = {
        h: "",
        k: ""
      };
      this.romaji = this.romaji.toLowerCase();
    },

    assignVars() {
      this.input.h += this.romaji.charAt(this.start);
      this.input.k += this.romaji.charAt(this.start);
      this.start++;
    },
    ensureVarsRange() {
      if (this.romaji.length - this.start < this.hashMaxLen) {
        this.hashMaxLen = this.romaji.length - this.start;
      }
    },

    convert() {
      this.resetVars();

      const inputArr = [...this.romaji];

      inputArr.forEach(() => {
        this.hashMaxLen = 5;
        this.hashExists = false;
        this.ensureVarsRange();
        this.findHash();
        if (!this.hashExists) {
          this.assignVars();
        }
      });

      this.output.h = this.input.h;
      this.output.k = this.input.k;
    }
  },
  data() {
    return {
      kanaHash,
      romajiInput: "",
      romaji: "",
      start: 0,
      hashMaxLen: 5,
      hashExists: false,
      output: {
        h: "",
        k: ""
      },
      input: {
        h: "",
        k: ""
      }
    };
  }
};
</script>

<style>
:root {
  --light-gray: #cbd5e0;
}
body * {
  box-sizing: border-box;
}
.wrapper {
  height: 100vh;
}
.flex {
  display: -webkit-box;
  display: flex;
  -webkit-box-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  align-items: center;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  flex-direction: column;
}
.box-panel {
  width: 600px;
  padding: 2rem 4rem 4rem 4rem;
  border: 1px solid var(--light-gray);
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
}
h1 {
  margin: 0 auto 2rem auto;
}
label {
  width: 100%;
  display: block;
  padding: 10px;
  text-align: center;
  font-size: 1.2rem;
  font-weight: bold;
}

.input {
  display: block;
  text-align: center;
  margin: 0 auto;
  padding: 10px;
  width: 100%;
  height: 3rem;
  font-size: 1.2rem;
  line-height: 1.6rem;
}
.output {
  width: 100px;
  border: 1px solid var(--light-gray);
  width: 100%;
  height: 3rem;
  font-size: 1.2rem;
  line-height: 3rem;
}
</style>
