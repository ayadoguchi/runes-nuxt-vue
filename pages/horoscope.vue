<template>
  <div>
    <div class="map">
      <div class="result" v-if="result">
        <span :class='[result.icon.length > 1 ? result.icon : ""]' class="rune size-XL">
          <span v-if="result.icon.length === 1">{{ result.icon }}</span>
        </span>
      </div>
    </div>
    <vs-alert v-if="result" class="mb20">
      <template #title>
        {{result.title}}
      </template>
      <p>{{result.discription}}</p>
      <p>{{result.unnsei}}</p>
    </vs-alert>
     <div class="center">
      <vs-button
        square
        icon
        :active="active == 0"
        @click="uranai(); active = 0"
      >
        占う
      </vs-button>
    </div>
  </div>
</template>

<script>
  export default {
    data:() => ({
      active: 0,
      result: null,
      runes: [{
        'position': 1,
        'title': 'フェオ',
        'icon': 'V',
        'discription': '家畜、財産、英語のfee',
        'unnsei': '何らかの報酬を得る。物事が複利的に発展していく。'
      },
      {
        'position': 2,
        'title': 'ウル',
        'icon': 'U',
        'discription': '野生の牛（オウルコス）',
        'unnsei': '猪突猛進。勇猛果敢。一途。野生のパワー。'
      },
      {
        'position': 3,
        'title': 'ソーン',
        'icon': 'SS',
        'discription': '巨人、トゲ、助言',
        'unnsei': '慎重さを要する。計画的な足止め。危険回避。'
      },
      {
        'position': 4,
        'title': 'アンスール',
        'icon': 'A',
        'discription': '口、オーディーン神、英語のanswer',
        'unnsei': '言葉のコミュニケーション。メール。情報。専門知識。'
      },
      {
        'position': 5,
        'title': 'ラド',
        'icon': 'R',
        'discription': '車輪、旅',
        'unnsei': '移動、変化。転職。遠方からの情報。車、バイク。運送業。'
      },
      {
        'position': 6,
        'title': 'ケン',
        'icon': 'KK',
        'discription': 'たいまつの火',
        'unnsei': '知恵。ひらめき。やる気。情熱。'
      },
      {
        'position': 7,
        'title': 'ギューフ',
        'icon': 'JJ',
        'discription': 'ギフト、愛情、才能',
        'unnsei': 'やさしさ。恋愛。人類愛。人を助ける事。プレゼント。'
      },
      {
        'position': 8,
        'title': 'ウィン',
        'icon': 'Q',
        'discription': '喜び、満足',
        'unnsei': 'うれしい結果。十分良くやっている。自画自賛。'
      },
      {
        'position': 9,
        'title': 'ハガル',
        'icon': 'HH',
        'discription': '雹（ひょう）',
        'unnsei': '不可避の変化。予想外のトラブル。破壊を伴う変革。'
      },
      {
        'position': 10,
        'title': 'ニイド',
        'icon': 'N',
        'discription': 'need、欠乏、忍耐',
        'unnsei': '身動きとれない。しがらみ。タロットの吊られた男。'
      },
      {
        'position': 11,
        'title': 'イス',
        'icon': 'II',
        'discription': '氷、英語のIce',
        'unnsei': '停滞。安定。冬眠。計画の凍結。冷えた関係。'
      },
      {
        'position': 12,
        'title': 'ヤラ',
        'icon': 'J',
        'discription': '一年、収穫',
        'unnsei': '収穫までのプロセス。日々の努力が大事。季節の巡り。'
      },
      {
        'position': 13,
        'title': 'ユル',
        'icon': 'E',
        'discription': 'イチイの木、死と再生、弓',
        'unnsei': '180度の方向転換。根本的な変化。くされ縁を絶つ。脱皮。'
      },
      {
        'position': 14,
        'title': 'ペオース',
        'icon': 'P',
        'discription': 'ダイスカップ、ギャンブル、神の手',
        'unnsei': '天に委ねる。思わぬ展開。意外な事実が発覚。パルプンテ。'
      },
      {
        'position': 15,
        'title': 'エオロー',
        'icon': 'X',
        'discription': '友情、保護',
        'unnsei': '頼もしい仲間。横の人間関係。霊的に守られている。'
      },
      {
        'position': 16,
        'title': 'シゲル',
        'icon': 'Z',
        'discription': '太陽、勝利',
        'unnsei': '自信満々。威風堂々。まぶしすぎる人。'
      },
      {
        'position': 17,
        'title': 'ティール',
        'icon': 'T',
        'discription': 'ティール神（マルス）、父性',
        'unnsei': '男性性。向上心。精神力。戦略をもって前進する。'
      },
      {
        'position': 18,
        'title': 'ペオーク',
        'icon': 'B',
        'discription': 'カバの木、母性、成長',
        'unnsei': '成長を見守る。母親的な役割。おせっかい。世話焼き。'
      },
      {
        'position': 19,
        'title': 'エオー',
        'icon': 'EE',
        'discription': '馬、変化',
        'unnsei': '変化。自由独立。散歩、ドライブ。職人気質。'
      },
      {
        'position': 20,
        'title': 'マン',
        'icon': 'M',
        'discription': '人間',
        'unnsei': '人間関係。相互扶助。人のふり見てわがふり直す。'
      },
      {
        'position': 21,
        'title': 'ラーグ',
        'icon': 'L',
        'discription': '水、女性性',
        'unnsei': 'ロマンス。感性。霊感。意志薄弱。幻想。流れに乗る。'
      },
      {
        'position': 22,
        'title': 'イング',
        'icon': 'MM',
        'discription': '豊穣、イング神、フレイ神',
        'unnsei': '満足のいく成果。ゴールに到達。一段落。完了。'
      },
      {
        'position': 23,
        'title': 'オセル',
        'icon': 'O',
        'discription': '故郷',
        'unnsei': '家族のしがらみ。歴史、伝統、文化。不動産。遺産。'
      },
      {
        'position': 24,
        'title': 'ダエグ',
        'icon': 'D',
        'discription': '一日、太陽の運行',
        'unnsei': '重要なルーチンワーク。一歩一歩。日常茶飯事。'
      },
      {
        'position': 25,
        'title': 'ブランク',
        'icon': '',
        'discription': '宿命',
        'unnsei': '今が運命の分岐点。他のルーンを強調。物事は白紙である。'
      }]
    }),
    methods: {
      uranai: function () {
        let rand = Math.floor(Math.random() * this.runes.length);
        this.result = this.runes[rand];
      }
    }
  }
</script>


<style lang="scss">
@font-face {
  font-family: 'rune';
  src: url("~assets/fonts/RuneAMN_Sans_1.20171016.otf");
}
.center {
  text-align: center;;
}
.mb20 {
  margin-bottom: 20px;
}
.vs-button {
  display: inline-block;
}
.rune {
  font-family: rune;
  &.size-L {
    font-size: 30px;
  }
  &.size-XL {
    font-size: 34px;
    position: absolute;
    top: 35%;
    left: 35%;
    color: antiquewhite;
    font-weight: bold;
    background: rgba(0, 0, 0, 0.8);
    border-radius: 100px;
    width: 60px;
    height: 60px;
    text-align: center;
    display: table;
    padding-top: 12px;
  }
  &.EE {
    &:before {
      content: '\016D6';
    }
  }
  &.MM {
    &:before {
      content: '\016DC';
    }
  }
  &.KK {
    &:before {
      content: '\016B2';
    }
  }
  &.II {
    &:before {
      content: '\016C1';
    }
  }
  &.HH {
    &:before {
      content: '\016BA';
    }
  }
  &.SS {
    &:before {
      content: '\016A6';
    }
  }
  &.JJ {
    &:before {
      content: '\016B7';
    }
  }
}
.map {
  max-width: 200px;
  max-height: 200px;
  margin: 10px auto;
  position: relative;
  background-image: url("~assets/MagicCircle_RuneAMN_20141019.svg");
  background-size: auto 200px;
  background-repeat: no-repeat;
  height: 200px;
  background-position: center center;
}
</style>
