<template>
  <div id="app">

    <template>
      <span v-if="step < 10"><b>step{{step+1}}</b></span>
      <InputQuestion
        key="start"
        v-if="step === 0"
        @start="handleStart"
      />

      <SelectQuestion
        key="image"
        v-if="step === 1"
        v-model="questions.image"
        @next="handleNext"
        :message="messageList[0]"
        :choices="choicesList[0]"
      />

      <SelectQuestion
        key="question2"
        v-if="step === 2"
        v-model="questions.q1"
        @next="handleNext"
        :message="messageList[1]"
        :choices="choicesList[1]"
      />

      <SelectQuestion
        key="question3"
        v-if="step === 3"
        v-model="questions.q2"
        @next="handleNext"
        :message="messageList[2]"
        :choices="choicesList[2]"
      />

      <SelectQuestion
        key="question4"
        v-if="step === 4"
        v-model="questions.q3"
        @next="handleNext"
        :message="messageList[3]"
        :choices="choicesList[3]"
      />

      <SelectQuestion
        key="question5"
        v-if="step === 5"
        v-model="questions.q4"
        @next="handleNext"
        :message="messageList[4]"
        :choices="choicesList[4]"
      />

      <SelectQuestion
        key="question6"
        v-if="step === 6"
        v-model="questions.q5"
        @next="handleNext"
        :message="messageList[5]"
        :choices="choicesList[5]"
      />

      <SelectQuestion
        key="question7"
        v-if="step === 7"
        v-model="questions.q6"
        @next="handleNext"
        :message="messageList[6]"
        :choices="choicesList[6]"
      />

      <SelectQuestion
        key="question8"
        v-if="step === 8"
        v-model="questions.q7"
        @next="handleNext"
        :message="messageList[7]"
        :choices="choicesList[7]"
      />

      <SelectQuestion
        key="question9"
        v-if="step === 9"
        v-model="questions.q8"
        @next="handleNext"
        :message="messageList[8]"
        :choices="choicesList[8]"
      />

    </template>

    <SyochuResult
      :step="step"
      :questions="questions"
    />
  </div>
</template>

<script>
import InputQuestion from './components/InputQuestion.vue'
import SelectQuestion from './components/SelectQuestion.vue'
import SyochuResult from './components/SyochuResult.vue'
import { parse } from 'querystring'

export default {
  name: 'app',
  data() {
    return {
      step: 0,
      questions: {
        name: '',
        title: 1,
        image: 1,
        q1: 1,
        q2: 1,
        q3: 1,
        q4: 1,
        q5: 1,
        q6: 1,
        q7: 1,
        q8: 1
      }
    }
  },
  components: {
    InputQuestion,
    SelectQuestion,
    SyochuResult
  },
  mounted() {
    const params = parse(location.search.replace('?', ''))
    const isValid = ['name', 'title', 'q1', 'q2', 'q3', 'q4', 'q5', 'q6', 'q7', 'q8'].every((val) => {
      if (!params[val]) {
        return false
      }
      if (val != 'name' && parseInt(params[val]) < 1) {
        return false
      }
      return true
    })
    if (isValid) {
      const questions = {
        name: params.name,
        title: parseInt(params.title),
        q1: parseInt(params.q1),
        q2: parseInt(params.q2),
        q3: parseInt(params.q3),
        q4: parseInt(params.q4),
        q5: parseInt(params.q5),
        q6: parseInt(params.q6),
        q7: parseInt(params.q7),
        q8: parseInt(params.q8)
      }
      this.questions = questions
      this.step = 9
    }
  },
  methods: {
    handleNext() {
      this.step ++
    },
    handleStart(startData) {
      this.questions.name = startData.name
      this.questions.title = startData.title
      this.handleNext()
    }
  },
  computed: {
    messageList() {
      return [
        'この辺に、夏っぽい挿し絵でも入れておこう。どれを入れる？',
        '暑中見舞いの相手は、キミとどんな関係の人？',
        'その人とは、どのくらい会ってない？',
        'この夏、どのくらい暑い？',
        'この暑い日々、相手のお身体についてどういたわる？',
        'ところで、ＴＵＢＥについてどう思う？',
        'この夏、自分はどんな風にお過ごし？',
        '最後にとくに言っておきたいことは？',
        'では最後に、しめの挨拶を！'
      ]
    },
    choicesList() {
      return [
        ['夏の風物詩（食べ物）', '夏の風物詩（動物）', '夏の風物詩（機械）', '夏の風物詩（昆虫）', '夏の風物詩（人間）'],
        ['仕事相手', '友達', '恋人', '知らない人'],
        ['１日', '１週間', '１ヶ月', '１年', '１０年', '２０年'],
        ['ヘコむほど', 'やる気が出ないほど', '脱ぎたくなるほど', '燃えるほど'],
        ['風邪について', '疲労について', '病気について', '食べ過ぎについて'],
        ['萌え～', '萎え～'],
        ['ファンタジーに', 'ごきげんに', 'スイミングに', 'リローデッドに'],
        ['励まし', 'エール', '助言', '苦言', '注意', '警告', '暴言', '失言'],
        ['アメリカンに', 'ダンディーに', 'ローカルに', 'コミカルに']
      ]
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}

#app {
  font-family: sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  max-width: 440;
  font-size: 12px;
  padding: 0 50px;
}
</style>