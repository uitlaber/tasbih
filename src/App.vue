<template>
  <div id="app">
      <p  v-if="currentItem">Әр қайталаған сайын шеңберді басыңыз</p>
      <button class="number" v-if="currentItem" @click="plus" v-text="number"></button>  
      <br>
       <span v-if="currentItem"> қалды - {{left}} </span>
      <br>
      <p><b>{{currentItem.text}}</b></p>
     
      <br>
      <p>{{currentItem.translate}}</p>
      <ul>
        <li v-for="item in items" v-bind:key="item.title" ><a href="#" @click.prevent="setCurrent(item)" >{{item.title}}</a> <span v-if="item.ready"> (Болды)</span>
         </li>
      </ul>
  </div>
</template>

<script>
export default {
  name: "App",
  computed: {
    left() {
      return this.currentItem.left;
    }
  },
  created() {
    if (localStorage.getItem("items") !== null) {
      this.items = JSON.parse(localStorage.getItem("items"));
    }
  },
  data() {
    return {
      number: 0,
      currentItem: false,
      items: [
        {
          ready: false,
          title: "Ықлас сүресін 100 рет",
          text:
            "Бисмилләһир рахмәнир рахим. Қуль һу уаллаһу аһаді. Аллаһус самаді. Ләм иәлиді, уә ләм иуләді. Уә ләм иәкуль ләһу куфууән ахаді.",
          translate:
            "Ықлас сүресінің қазақша мағынасы: «Алла біреу ақ. Алла мұңсыз. (әр Нәрсе Оған Мұқтаж). Ол тумады да туылмады. Әрі Оған ешкім тең емес».",
          count: 100,
          left: 100
        },
        {
          ready: false,
          title: "Қадыр сүресі – 100 рет",
          text:
            "Бисмилләһир рахманир рахим. Иннә әңзәлнәһу фи ләйләтил қадыр. Уә мә әдракә мә ләйләтул қадыр. Ләйләтул қадри хайрум минәл фи шәһр. Тәнәззәлул мәләикәту уәр руху фи һә биизни раббиһим мин кулли әмр. Сәләмун һиә хатта мәт ләғил фәжр.",
          translate:
            "1. Біз Оны (Құранды) қадір түні түсірдік. 2. Қадір түнінің не екенін білесің бе? (Аллаһ Тағала білдірмесе) қайдан білесің? 3. Қадір түні мың айдан да артық. 4. Ол түні Аллаһтың рұқсатымен кез-келген іс үшін Рух пен періштелер түседі. 5. (әсіресе ол түнді ғибадатпен өткізгендер үшін) таң атқанға дейін Аллаһтың рақымы мен есендігі жауады",
          count: 100,
          left: 100
        },
        {
          ready: false,
          title: "Лә иләһә иллаллаһ, Мухаммәдур расулуллаһ – 100 рет",
          text: "Лә иләһә иллаллаһ, Мухаммәдур расулуллаһ",
          translate: "Алладан басқа Тәңір жоқ, Мұхаммед оның елшісі.",
          count: 100,
          left: 100
        },
        {
          ready: false,
          title:
            "Әшһәду әллә иләһә иллаллаһ, уә әшһәду әннә Мухаммәдән ғабдуһу уә расулуһ – 100 рет.",
          text:
            "Әшһәду әллә иләһә иллаллаһ, уә әшһәду әннә Мухаммәдән ғабдуһу уә расулуһ",
          translate:
            "Алладан басқа ешбір тәңір жоқ және Мухаммед Оның Елшісі және құлы екендігіне куәлік беремін.",
          count: 100,
          left: 100
        },
        {
          ready: false,
          title: "Астәғфируллуһ – 500 рет",
          text: "Астәғфируллуһ",
          translate: "Алланың азабынан сақтасын.",
          count: 500,
          left: 500
        },
        {
          ready: false,
          title:
            "Лә иләһә иллаллаһ уахдәһу лә шарикәләһ, ләһул мулку уә ләһул хамду, уә һуә ғалә кулли шәйин қадиир – 100 рет",
          text:
            "Лә иләһә иллаллаһ уахдәһу лә шарикәләһ, ләһул мулку уә ләһул хамду, уә һуә ғалә кулли шәйин қадиир",
          translate: "",
          count: 100,
          left: 100
        }
      ]
    };
  },
  methods: {
    plus() {
      if (this.left == 0) {
        this.currentItem.ready = true;
      } else {
        this.number++;
        this.currentItem.left--;
      }
      localStorage.setItem("items", JSON.stringify(this.items));
    },
    setCurrent(item) {
      if (!item.ready) {
        this.currentItem = item;
        this.reset();
      }
    },
    reset() {
      this.number = this.currentItem.count - this.currentItem.left;
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

.number {
  font-size: 55px;
  border-radius: 100%;
  border: 1px solid #ccc;
  width: 100px;
  height: 100px;
  margin-bottom: 40px;
  cursor: pointer;
}
.number:focus {
  outline: none;
}

ul {
  list-style: none;
  padding-left: 0;
}

li {
  text-align: left;
  font-size: 18px;
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

a {
  text-decoration: none;
  color: #000ff;
}
</style>
