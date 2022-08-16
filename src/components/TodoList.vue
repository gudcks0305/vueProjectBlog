<template>
  <div class="TodoList grid grid-cols-4 gap-4">
    <div
      class="max-w-sm rounded overflow-hidden shadow-lg"
      :key="list.postId"
      v-for="list in todoList"
    >
      <img
        class="w-full"
        :src="list.profileImageUrl"
        alt="Sunset in the mountains"
      />
      <div class="px-6 py-4">
        <div class="font-bold text-xl mb-2">{{ list.postId }}</div>
        <p class="text-gray-700 text-base">
          <!--{{ list.content }} !-->
        </p>
      </div>
      <div class="px-6 pt-4 pb-2">
        <span
          class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2"
          >#photography</span
        >
        <span
          class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2"
          >#travel</span
        >
        <span
          class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2"
          >#winter</span
        >
      </div>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
import axios from 'axios'
import PostData from '../dataClass/PostData'
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  // eslint-disable-next-line
  data() {
    return {
      todo: 'String',
      todoList: []
    }
  },
  // eslint-disable-next-line
  mounted() {
    this.getPostData()
  },
  methods: {
    // eslint-disable-next-line
    push() {
      this.todoList.push(this.todo)
    },
    // eslint-disable-next-line
    getPostData() {
      axios
        .get('')
        .then((res) => {
          for (let i = 0; i < res.data.body.data.content.length; i++) {
            let data = res.data.body.data.content[i]
            let pd = new PostData(
              data.postId,
              data.content,
              data.category.categoryName,
              data.memberInfo.nickname,
              data.memberInfo.profileImageUrl
            )
            console.log(data.memberInfo)
            this.todoList.push(pd)
          }
        })
        .catch((err) => {
          console.log(err)
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
