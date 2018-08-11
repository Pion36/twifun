<template>
  <div class='twifun'>
    <div class="header">
      <section class="hero is-default is-bold">
        <div class="hero-head">
          <nav class="navbar">
            <div class="container">
              <div class="navbar-brand">
                <a class="navbar-item title" href="../">
                  Twifun
                </a>
                <span class="navbar-burger burger" data-target="navbarMenu">
                  <span></span>
                  <span></span>
                  <span></span>
                </span>
              </div>
            </div>
          </nav>
        </div>
      </section>
    </div>
    <div class="container">
      <div class="columns">
        <div class="column is-5">
          <div class="box" style="text-align:left;">
            <h2 class="subtitle">Twifun</h2>
            <p>クラウドファンディングの目的</p>
            <input v-model="name" placeholder="目的を書こう">
            <p>目標額</p>
            <input v-model="target" placeholder="目標額を記入"  type="number" number> Ether
            <a class="button is-info is-outlined" v-on:click="MakeModal = true">作成</a>
            <a class="button is-info is-outlined" v-on:click="twitterapi()">Twitter</a>
          </div>
        </div>
        <div class="column is-7">
          <div class="box">
            <h2 class="subtitle">あなたのBox</h2>
            <div id="#boxs">
              <div v-for="(value, index) in YourBoxlist" :key="index">
                <div v-if="index % 3 == 0" class="columns">
                  <div class="column is-4 is-desktop box" style="margin:0 0px 12px 0px;">
                    <p>{{ YourBoxlist[index].purpose }}</p>
                    <p>目標額:{{ YourBoxlist[index].target }} Ether</p>
                    <p>達成率:{{ YourBoxlist[index].amount / YourBoxlist[index].target * 100}}%</p>
                    <a class="button is-info is-outlined" v-on:click="DetailBoxModal = true, showname = YourBoxlist[index].name, showindex = YourBoxlist[index].id, showtarget = YourBoxlist[index].target, showamount = YourBoxlist[index].amount, showlimit = YourBoxlist[index].limittime">詳細</a>
                  </div>
                  <div v-if="YourBoxlist[index+1]" class="column is-4 is-desktop box" style="margin:0 0px 12px 0px;">
                    <p>{{ YourBoxlist[index+1].purpose }}</p>
                    <p>目標額:{{ YourBoxlist[index+1].target }} Ether</p>
                    <p>達成率:{{ YourBoxlist[index+1].amount / YourBoxlist[index+1].target * 100}}%</p>
                    <a class="button is-info is-outlined" v-on:click="DetailBoxModal = true, showname = YourBoxlist[index+1].name, showindex = YourBoxlist[index+1].id, showtarget = YourBoxlist[index+1].target, showamount = YourBoxlist[index+1].amount, showlimit = YourBoxlist[index+1].limittime">詳細</a>
                  </div>
                  <div v-if="YourBoxlist[index+2]" class="column is-4 is-desktop box" style="margin:0 0px 12px 0px;">
                    <p>{{ YourBoxlist[index+2].purpose }}</p>
                    <p>目標額:{{ YourBoxlist[index+2].target }} Ether</p>
                    <p>達成率:{{ YourBoxlist[index+2].amount / YourBoxlist[index+2].target * 100}}%</p>
                    <a class="button is-info is-outlined" v-on:click="DetailBoxModal = true, showname = YourBoxlist[index+2].name, showindex = YourBoxlist[index+2].id, showtarget = YourBoxlist[index+2].target, showamount = YourBoxlist[index+2].amount, showlimit = YourBoxlist[index+2].limittime">詳細</a>
                  </div>
                </div>
              </div>
            </div>
            <a class="button is-info is-outlined" v-on:click='displayYourBoxs(web3.coinbase)'>表示</a>
          </div>
        </div>
      </div>
      <div class="columns">
        <div class="column is-12">
          <div class="box">
            <h2 class="subtitle">みんなのクラウドファンディング</h2>
            <div id="#boxs">
              <div v-for="(value, index) in AllBoxlist" :key="index">
                <div v-if="index % 3 == 0" class="columns">
                  <div class="column is-4 is-desktop box" style="margin:0 0px 12px 0px;">
                    <p>{{ AllBoxlist[index].purpose }}</p>
                    <p>目標額:{{ AllBoxlist[index].target }} Ether</p>
                    <p>達成率:{{ AllBoxlist[index].amount / AllBoxlist[index].target * 100}}%</p>
                    <a class="button is-info is-outlined" v-on:click="DetailBoxModal = true, showname = AllBoxlist[index].name, showindex = AllBoxlist[index].id, showtarget = AllBoxlist[index].target, showamount = AllBoxlist[index].amount, showlimit = AllBoxlist[index].limittime, tanin = true">詳細</a>
                  </div>
                  <div v-if="AllBoxlist[index+1]" class="column is-4 is-desktop box" style="margin:0 0px 12px 0px;">
                    <p>{{ AllBoxlist[index+1].purpose }}</p>
                    <p>目標額:{{ AllBoxlist[index+1].target }} Ether</p>
                    <p>達成率:{{ AllBoxlist[index+1].amount / AllBoxlist[index+1].target * 100}}%</p>
                    <a class="button is-info is-outlined" v-on:click="DetailBoxModal = true, showname = AllBoxlist[index+1].name, showindex = AllBoxlist[index+1].id, showtarget = AllBoxlist[index+1].target, showamount = AllBoxlist[index+1].amount, showlimit = AllBoxlist[index+1].limittime, tanin = true">詳細</a>
                  </div>
                  <div v-if="AllBoxlist[index+2]" class="column is-4 is-desktop box" style="margin:0 0px 12px 0px;">
                    <p>{{ AllBoxlist[index+2].purpose }}</p>
                    <p>目標額:{{ AllBoxlist[index+2].target }} Ether</p>
                    <p>達成率:{{ AllBoxlist[index+2].amount / AllBoxlist[index+2].target * 100}}%</p>
                    <a class="button is-info is-outlined" v-on:click="DetailBoxModal = true, showname = AllBoxlist[index+2].name, showindex = AllBoxlist[index+2].id, showtarget = AllBoxlist[index+2].target, showamount = AllBoxlist[index+2].amount, showlimit = AllBoxlist[index+2].limittime, tanin = true">詳細</a>
                  </div>
                </div>
              </div>
            </div>
            <a class="button is-info is-outlined" v-on:click='displayAllBoxs()'>表示</a>
          </div>
        </div>
      </div>
    </div>
    <b-modal :active.sync="DetailBoxModal">
      <div class="modal-card" style="width: auto">
           <header class="modal-card-head">
             {{showindex}}
             <p class="modal-card-title">{{ showname }}</p>
           </header>
           <section class="modal-card-body">
             <p>目標額:{{ showtarget }} Ether</p>
             <p>合計:{{ showamount }} Ether</p>
             <p>達成率:{{ showamount / showtarget * 100}}%</p>
             <p>期限：{{unixtodate(showlimit)}}</p>
             <p v-if="unixcurrent() <= showlimit * 1000">期限内です</p>
             <p v-if="unixcurrent() > showlimit * 1000" style="color:red;">期限を超えてしまいました</p>
           </section>
           <footer class="modal-card-foot">
             <a class="button is-info is-outlined" v-if="(unixcurrent() <= showlimit * 1000) && (showamount / showtarget * 100 < 100), tanin == true" v-on:click="DepositModal = true, exertid = showindex,exertname = showname">貯金</a>
             <a class="button is-info is-outlined" v-if="showamount / showtarget * 100 >= 100 && WithdrawActive && tanin == false" v-on:click="WithdrawModal = true, exertid = showindex,exertname = showname">引き出す</a>
             <a class="button is-info is-outlined" v-if="showamount / showtarget * 100 < 100 && WithdrawActive && tanin == false" v-on:click="PenaltyWithdrawModal = true, exertid = showindex,exertname = showname">引き出す</a>
             <button class="button" type="button" @click="DetailBoxModal = false, tanin = false">閉じる</button>
           </footer>
       </div>
    </b-modal>
    <b-modal :active.sync="MakeModal">
      <div class="modal-card" style="width: auto">
           <header class="modal-card-head">
             <p class="modal-card-title">以下の条件でクラウドファンディングを実行しますか？</p>
           </header>
           <section class="modal-card-body">
             <p>目的: {{ this.name }}</p>
             <p>目標額: {{ this.target }} Ether</p>
             <p>初期投入額: {{ this.amount }} Ether</p>
           </section>
           <footer class="modal-card-foot">
             <button class="button" type="button" @click="make()">はい(実行)</button>
             <button class="button" type="button" @click="MakeModal = false">閉じる</button>
           </footer>
       </div>
    </b-modal>
    <b-modal :active.sync="DepositModal">
      <div class="modal-card" style="width: auto">
           <header class="modal-card-head">
             <p class="modal-card-title">BoxにEtherを入れます</p>
           </header>
           <section class="modal-card-body">
             <p>名前: {{exertid}}:{{ exertname }}</p>
             <input v-model="amount" placeholder="目標額を記入" type="number" number> Ether
           </section>
           <footer class="modal-card-foot">
             <button class="button" type="button" @click="deposit(exertid,amount)">入れる</button>
             <button class="button" type="button" @click="DepositModal = false">閉じる</button>
           </footer>
       </div>
    </b-modal>
    <b-modal :active.sync="WithdrawModal">
      <div class="modal-card" style="width: auto">
           <header class="modal-card-head">
             <p class="modal-card-title">BoxからEtherを引き出します</p>
           </header>
           <section class="modal-card-body">
             <p>名前: {{ exertname }}</p>
             <p>目標額集めることができました。おめでたいです！</p>
           </section>
           <footer class="modal-card-foot">
             <button class="button" type="button" @click="withdraw(exertid)">引き出す</button>
             <button class="button" type="button" @click="WithdrawModal = false">閉じる</button>
           </footer>
       </div>
    </b-modal>
  </div>
</template>

<script>
import Twitter from 'node-twitter-api'

export default {
  name: 'Top',
  data () {
    return {
      name: null,
      target: null,
      limit: 31536000,
      amount: null,
      YourBoxlist: [],
      AllBoxlist: [],
      showindex: null,
      showname: null,
      showtarget: null,
      showamount: null,
      showlimit: null,
      WithdrawActive: true,
      DetailBoxModal: false,
      MakeModal: false,
      DepositModal: false,
      WithdrawModal: false,
      exertid: null,
      exertname: null,
      twitterID: 5555555,
      tanin: false
    }
  },
  computed: {
    web3 () {
      return this.$store.state.web3
    }
  },
  mounted () {
    this.$store.dispatch('getContractInstance')
    var burger = document.querySelector('.burger')
    var menu = document.querySelector('#' + burger.dataset.target)
    burger.addEventListener('click', function () {
      burger.classList.toggle('is-active')
      menu.classList.toggle('is-active')
    })
  },
  methods: {
    twitterapi: function () {
      var twitter = new Twitter({
        consumerKey: 'cB12zexX5r9ThpBEchOgi8GZC',
        consumerSecret: 'hyhHfRATViWdBLWCn0vNYj7HsAZGnsjE2usihYijfRnue5ICZo',
        callback: 'http://localhost:8080'
      })

      twitter.getRequestToken(function (error, requestToken, requestTokenSecret, results) {
        if (error) {
          console.log('Error getting OAuth request token : ' + error)
        } else {
          this.$session.start()
          this.$session.set('token', requestToken)
          this.$session.set('secret', requestTokenSecret)
          console.log('requestToken: ' + requestToken)
        }
      })
    },
    unixcurrent: function () {
      var current = Date.now()
      return current
    },
    unixtodate: function (unixtime) {
      var d = new Date(unixtime * 1000 + 32400)
      var year = d.getFullYear()
      var month = d.getMonth() + 1
      var day = d.getDate()
      var hour = ('0' + d.getHours()).slice(-2)
      var min = ('0' + d.getMinutes()).slice(-2)
      var sec = ('0' + d.getSeconds()).slice(-2)
      return (year + '-' + month + '-' + day + ' ' + hour + ':' + min + ':' + sec)
    },
    getBoxDetails: function (id) {
      var self = this
      return new Promise(function (resolve, reject) {
        self.$store.state.contractInstance().Boxs.call(id, function (err, result) {
          if (!err) {
            console.log(result)
            resolve(result)
          }
        })
      })
    },
    BoxToOwner: function (id) {
      this.$store.state.contractInstance().BoxToOwner.call(id, function (err, result) {
        if (!err) {
          console.log(result)
          return result
        }
      })
    },
    getBoxByOwner: function (owner) {
      var self = this
      return new Promise(function (resolve, reject) {
        self.$store.state.contractInstance().getBoxByOwner.call(owner, function (err, result) {
          if (!err) {
            var array = new Array(result.length)
            for (var i = 0; i < result.length; i++) {
              array[i] = result[i].c[0]
            }
            return array
          }
        })
      })
    },
    displayYourBoxs: function (owner) {
      var self = this
      self.YourBoxlist = []
      Promise.resolve(owner)
        .then(function (value) {
          return new Promise((resolve, reject) => {
            self.$store.state.contractInstance().getBoxByOwner.call(owner, function (err, result) {
              if (!err) {
                var array = new Array(result.length)
                for (var i = 0; i < result.length; i++) {
                  array[i] = result[i].c[0]
                }
                resolve(array)
              }
            })
          })
        })
        .then(function (array) {
          return Promise.all([
            new Promise((resolve, reject) => {
              var loop = Promise.resolve()
              for (var i = 0; i < array.length; i++) {
                (function (i) {
                  loop = loop.then(function () {
                    return new Promise(function (resolve, reject) {
                      self.$store.state.contractInstance().Boxs.call(array[i], function (err, result) {
                        if (!err) {
                          var kari = {}
                          kari['purpose'] = result[0]
                          kari['target'] = result[1].c[0] / 10000
                          kari['amount'] = result[2].c[0] / 10000
                          kari['starttime'] = result[3].c[0]
                          kari['limittime'] = result[4].c[0]
                          kari['id'] = array[i]
                          self.YourBoxlist.push(kari)
                          // オブジェクトを作って
                          // そのオブジェクトを配列の中に入れていく
                          resolve()
                        }
                      })
                    })
                  })
                })(i)
              }
              console.log('表示')
              resolve()
            })
          ])
        })
    },
    displayAllBoxs: function () {
      var self = this
      self.AllBoxlist = []
      Promise.resolve()
        .then(function (value) {
          return new Promise((resolve, reject) => {
            self.$store.state.contractInstance().getBoxlength.call(function (err, result) {
              if (!err) {
                resolve(result)
              }
            })
          })
        })
        .then(function (long) {
          return Promise.all([
            new Promise((resolve, reject) => {
              var loop = Promise.resolve()
              for (var i = 0; i < long; i++) {
                (function (i) {
                  loop = loop.then(function () {
                    return new Promise(function (resolve, reject) {
                      self.$store.state.contractInstance().Boxs.call(i, function (err, result) {
                        if (!err) {
                          var kari = {}
                          kari['purpose'] = result[0]
                          kari['target'] = result[1].c[0] / 10000
                          kari['amount'] = result[2].c[0] / 10000
                          kari['starttime'] = result[3].c[0]
                          kari['limittime'] = result[4].c[0]
                          kari['id'] = i
                          self.AllBoxlist.push(kari)
                          // オブジェクトを作って
                          // そのオブジェクトを配列の中に入れていく
                          resolve()
                        }
                      })
                    })
                  })
                })(i)
              }
              console.log('表示')
              resolve()
            })
          ])
        })
    },
    make: function () {
      var self = this
      Promise.resolve()
        .then(function () {
          return new Promise((resolve, reject) => {
            self.$store.state.contractInstance().makeBox(self.name, self.target * 1000000000000000000, self.twitterID, {
              gas: 300000,
              value: 0,
              from: self.$store.state.web3.coinbase
            }, (err, result) => {
              if (err) {
                console.log(err)
              } else {
                self.name = null
                self.target = null
                self.limit = null
                self.amount = null
                resolve()
              }
            })
          })
        })
      self.MakeModal = false
    },
    deposit: function (id, amount) {
      console.log(id)
      console.log(amount)
      var self = this
      Promise.resolve()
        .then(function () {
          return new Promise((resolve, reject) => {
            self.$store.state.contractInstance().deposit(id, {
              gas: 300000,
              value: self.$store.state.web3.web3Instance().toWei(amount, 'ether'),
              from: self.$store.state.web3.coinbase
            }, (err, result) => {
              if (err) {
                console.log(err)
              } else {
                console.log(self.amount)
                self.amount = null
                resolve()
              }
            })
          })
        })
      self.exertid = null
      self.exertname = null
      self.DepositModal = false
      self.DetailBoxModal = false
      console.log('貯金する')
    },
    withdraw: function (id) {
      this.WithdrawActive = false
      console.log(id)
      var self = this
      Promise.resolve()
        .then(function () {
          return new Promise((resolve, reject) => {
            self.$store.state.contractInstance().withdraw(id, {
              gas: 300000,
              value: 0,
              from: self.$store.state.web3.coinbase
            }, (err, result) => {
              if (err) {
                console.log(err)
              } else {
                self.WithdrawActive = true
                resolve()
              }
            })
          })
        })
      self.exertid = null
      self.exertname = null
      self.WithdrawModal = false
      self.DetailBoxModal = false
      console.log('引き出す')
    }
  }
}
</script>

<style>
.title {
  color:white;
}
</style>

<!-- Add 'scoped' attribute to limit CSS to this component only -->
<style scoped>
</style>
