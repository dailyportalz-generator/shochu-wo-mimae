<!-- src/components/InputQuestion.vue -->
<template>
  <form @submit.prevent="handleSubmit" class="input-question">
    <dl>
      <dt>ではさっそく、暑中見舞いを出す相手の名前を書こう！</dt>
      <dd>
        <input v-model="name" type="text" required>
        <select v-model="title" required>
            <option :value="1">さん</option>
            <option :value="2">くん</option>
            <option :value="3">ちゃん</option>
            <option :value="4">様</option>
            <option :value="5">殿</option>
            <option :value="6">選手</option>
            <option :value="7">総理</option>
            <option :value="8">総書記</option>  
        </select>
      </dd>
    </dl>
    <button>次へ</button>
  </form>
</template>

<script>
export default {
    data(){
        return{
            name: '',
            title:1
        }
    },
    methods:{
        handleSubmit(){
            this.$emit('start', {
                name: this.name,
                title:this.title
            })
        }
    }
}
</script>

<style scoped>
.input-question {
  margin-bottom: 24px;
  padding-bottom: 24px;
  border-bottom: dotted 1px #c6c6c6;
}

h3 {
  font-size: 1em;
}

dd {
  margin: 16px 0 0;
  padding: 0 0 8px 0;
}

button {
  width: 60px;
}

input[type='text'] {
  margin-right: 20px;
}
</style>