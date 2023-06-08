<!-- eslint-disable max-len -->
<template>
  <div>
    <div class="header w-[100%]">
      <div class="containerr w-[100%]">
        <div class="logo">Posts</div>
        <label for="inputPost">
          <input
            eslint-disable-next-line
            max-len
            class="h-[30px] bg-[#eeb2d5] mr-1 rounded-md min-w-[350px] max-w-[500px] border-2 border-black p-1"
            type="text"
            placeholder="No one will do it but You"
            :value="inputValue"
            @input="inpValueNow"
            @keypress.enter="addPost"
        /></label>
        <input
          class="w-12 justify-center border-2 border-black h-[30px]"
          id="buttonAddPost"
          type="button"
          value="Add"
          @click="addPost"
        />
      </div>
    </div>
    <ul class="ulTo">
      <li
        class="border-default border-2 p-3"
        v-for="(elem, indexElem) in this.$store.state.listPostsVuex"
        :key="indexElem.id"
      >
        {{ elem }}
        <div class="flex ml-[80%]">
          <button class="btnEdit" @click="editPost(indexElem)">Edit</button>
          <button class="btnDelete" @click="deletePost(indexElem)">
            Delete
          </button>
        </div>
      </li>
    </ul>
    <div v-if="this.$store.state.listPostsVuex.length" class="sumPosts">
      <div>
        <hr v-if="this.$store.state.listPostsVuex.length" class="mt-3" />
      </div>
      <div>Counter posts: {{ this.$store.state.listPostsVuex.length }}</div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputValue: '',
    };
  },
  methods: {
    addPost() {
      if (this.inputValue !== '') {
        this.$store.state.listPostsVuex.push(this.inputValue);
        this.inputValue = '';
      }
    },
    inpValueNow(event) {
      this.inputValue = event.target.value;
    },
    editPost(indexElem) {
      const userInput = prompt('Enter a new text', 'New text');
      if (userInput !== null) {
        this.$store.state.listPostsVuex[indexElem] = userInput;
      }
    },
    deletePost(indexElem) {
      this.$store.state.listPostsVuex.splice(indexElem, 1);
    },
  },
};
</script>

<style>
html,
body {
  margin: 0;
  padding: 0;
  background-color: rgb(255 241 241);
}

.ulTo {
  display: flex;
  align-items: center;
  flex-direction: column;
  padding: 0;
}

.ulTo li {
  list-style-type: none;
  word-wrap: break-word;
  margin-top: 14px;
  font-size: 30px;
  background-color: rgb(224, 255, 214);
  border-radius: 10px;
  width: 70%;
}

.header {
  width: 100%;
  background-color: rgb(153, 0, 255);
  text-align: center;
}

.containerr {
  height: 46px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.header .containerr .logo {
  font-family: 'Rubik Mono One', sans-serif;
  width: 80px;
  color: #fff700;
  font-size: 30px;
  text-shadow: 2px 2px 3px rgb(251 255 0 / 45%),
    -2px -2px 3px rgb(255 145 0 / 45%);
  -webkit-text-stroke: 1px #fff700;
  -webkit-text-fill-color: transparent;
  letter-spacing: 1px;
  display: flex;
  flex-wrap: wrap;
  margin-right: 10px;
  margin-top: -6px;
}

#buttonAddPost {
  color: black;
  background-color: rgb(238, 178, 213);
  border-radius: 7px;
  display: flex;
  flex-wrap: wrap;
}

#buttonAddPost:hover {
  color: #ffffff;
  background-color: rgb(94, 255, 0);
}

#inputPostText {
  text-align: center;
  word-break: break-all;
  margin-left: 102px;
  margin-right: 102px;
  color: rgba(109, 140, 141, 0.781);
}

.liTodo {
  text-align: center;
  list-style-type: none;
  font-size: 27px;
  word-break: break-all;
}

.btnDelete {
  width: 70px;
  height: 30px;
  color: rgb(0, 0, 0);
  font-size: 11px;
  font-family: 'montserrat';
  text-decoration: none;
  border: 2px solid #ff7675;
  padding: 0px 0px;
  text-transform: uppercase;
  overflow: hidden;
  border-radius: 7px;
  background-color: #e9b6d8;
  margin-left: 5px;
}

.btnDelete:hover {
  color: antiquewhite;
  background-color: #ff0000;
}

.btnEdit {
  width: 70px;
  height: 30px;
  color: rgb(0, 0, 0);
  font-size: 11px;
  font-family: 'montserrat';
  text-decoration: none;
  border: 2px solid #3b3d38;
  padding: 0px 0px;
  text-transform: uppercase;
  overflow: hidden;
  border-radius: 7px;
  background-color: #d5edbb;
}

.btnEdit:hover {
  background-color: #a5de68;
}

.sumPosts {
  display: flex;
  flex-wrap: nowrap;
  flex-direction: column;
  align-items: center;
}

hr {
  margin: 0;
  color: inherit;
  border: 0;
  border-top: 1px solid;
  opacity: 0.25;
  width: 650px;
  display: flex;
  justify-content: center;
}
</style>
