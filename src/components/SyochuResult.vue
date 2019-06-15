<template>
  <div class="syochu-result">
    <div class="syochu-result_main">
      <img src="@/assets/hagaki_up.gif" alt>
      <div style="display: flex;align-items: stretch">
        <img src="@/assets/hagaki_l.gif" alt>
        <div class="syochu-result__message">
          <p v-if="step">
            {{questions.name}} {{titleList[questions.title-1]}}
          </p>
          <img :key="result" v-if="step !== 1 && step !== 0" :src="imageList[questions.image-1]">
          <template v-for="(results, questionNumber) in resultsList">
            <p v-if="step > questionNumber+2" :key="questionNumber">
              <template v-for="(result, resultIndex) in results">
                <span :key="result" v-if="questions[`q${questionNumber+1}`] === resultIndex+1">{{result}}</span>
              </template>
            </p>
          </template>
        </div>
        <img src="@/assets/hagaki_r.gif" alt>
      </div>
      <img src="@/assets/hagaki_btm.gif" alt>
    </div>
  </div>
</template>

<script>
import { stringify } from 'querystring'
export default {
  props: {
    questions: Object,
    step: Number
  },
  computed: {
    titleList() {
      return [ 'さん', 'くん', 'ちゃん', '様', '殿', '選手', '総理', '総書記' ]
    },
    imageList() {
      return [
          require('@/assets/y1301.gif'),
          require('@/assets/y1302.gif'),
          require('@/assets/y1303.gif'),
          require('@/assets/y1304.gif'),
          require('@/assets/y1305.gif')
      ]
    },
    resultsList() {
      return [
        [
          '仕事でお忙しい中、失礼致します。',
          '私への迷惑な写メール送信でお忙しい中、失礼致します。',
          'ＴＳＵＮＡＭＩのような恋でお忙しい中、失礼致します。',
          '何をしてるのかも誰かも知りませんが、失礼致します。'
        ],
        [
          '「とくダネ」の小倉並みに毎日会っておりますが、あらためて暑中を見舞わせて頂きます。',
          '先週、大相撲名古屋場所の話をうっすら話したとき以来ですが、あらためて暑中を見舞わせて頂きます。',
          '一月ほど前、鶴瓶師匠の開チン映像について熱く議論したとき以来ですが、あらためて暑中を見舞わせて頂きます。',
          '昨年、ワールドカップでお互いにわかサッカーファンになったとき以来ですが、あらためて暑中を見舞わせて頂きます。',
          '「夏の日の1993」をclass風にデュエットしていた時以来、もうかれこれ１０年お会いしておりませんが、あらためて暑中を見舞わせて頂きます。',
          'ファミコンのマリオで殺し合いをしてた時以来、もうかれこれ２０年お会いしておりませんが、あらためて暑中を見舞わせて頂きます。'
        ],
        [
          'あまりの暑さで、顔がニコラスケイジのようになってしまうほどのこの夏、いかがお過ごしでしょうか。',
          'あまりの暑さで、夏に野球をやることの不毛さに気づき甲子園も中止になるほどのこの夏、いかがお過ごしでしょうか。',
          'あまりの暑さで、立ち振る舞いが高見盛のようになってしまうほどのこの夏、いかがお過ごしでしょうか。',
          'あまりの暑さで、アミノ酸も燃焼してしまうほどのこの夏、いかがお過ごしでしょうか。'
        ],
        [
          'いまさらＳＡＲＳに感染されたりしておりませんでしょうか。',
          '16連射し過ぎて、指を痛めたりしておりませんでしょうか。',
          'パナウェーブを浴び過ぎて、お身体を害されたりしておりませんでしょうか。',
          '悪魔の実を食べ過ぎて、お身体がゴムゴムになったりしておりませんでしょうか。'
        ],
        [
          '一方、夏にはＴＵＢＥのシングルは迷わず即買いの私と言えば、',
          '一方、夏にはＴＵＢＥよりもＴＵＲＵＢＥ（鶴瓶）の方が好きな私と言えば、'
        ],
        [
          'この夏は、クリアした「ＦＦⅩ－２」のレベル上げに日々いそしんでおります。',
          'この夏は、「ごきげんよう」の小堺の華麗な話術を毎日かかさず堪能することに日々注力しております',
          'この夏は、「世界水泳」に深い感銘を受け、日々「けのび」の上達にいそしんでおります。',
          'この夏は、この世の中は仮想現実マトリックスだと信じ、日々鍛練に励んでおります。'
        ],
        [
          'では暑い日が続きますが、その誰よりも豊富なトリビアを武器に世の中を渡っていってください。',
          'では暑い日が続きますが、これからもベイスターズを応援し続けてください。',
          'では暑い日が続きますが、「ゲームは１日１時間」だけは遵守していただけたらと思います。',
          'では暑い日が続きますが、にわか阪神ファンとして阪神の勝敗に一喜一憂していってください。',
          'では暑い日が続きますが、会うたびに「ゲッツ」を連発してくるのはもうやめて頂けたらと思います。',
          'では暑い日が続きますが、事件は現場で起きているということだけは忘れないでください。',
          'では暑い日が続きますが、その朝青龍並みの品格で頑張って生きていってください。',
          'では暑い日が続きますが、法で裁けない少年犯罪者の人権など認めず、これからも生きていってください。'
        ],
        [
          "では、I'll be back.",
          'では、ゲッツ！',
          'では、Ｓ・Ａ・Ｇ・Ａ・佐賀。',
          'では、だっふんだぁ。'
        ]
      ]
    }
  },
  methods: {
    handleClickRestart() {
      location.href = location.href.replace(location.search, '')
    }
  }
}
</script>

<style scoped>
img {
  user-select: none;
}
.syochu-result {
  width: 526px;
  margin: 0 auto;
}
.syochu-result_main {
  font-size: 0;
}
.syochu-result__message {
  padding: 16px;
  font-size: 12px;
  flex: 0.77;
  min-height: 150px;
}
.syochu-result__message p:first-child {
  margin-top: 0;
}
.syochu-result_build {
  text-align: right;
}
.syochu-result_share {
  font-size: 12px;
}
.syochu-result_shareurl {
  width: 100%;
}
.syochu-result_share {
  display: flex;
  align-items: center;
}
input {
  margin: 4px 10px 4px 0;
  flex: 1;
}
</style>