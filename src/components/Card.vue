<template>
   <div class="card">
     <div class="card-goods">
         <div class="goods-img">
           <img src="../assets/goods.png" alt="">
         </div>
         <div class="goods-info">
               <h3>电子保修卡</h3>
               <p>伸缩式铝合金手杖<span>老人拐杖</span></p>
               <p>伸缩助行器</p>
               <p>1年保修</p>
         </div>
     </div>
     <div class="card-form">
       <label for="">
           <span>商品SPU</span><input type="text">
       </label>
      <label for="">
           <span>购买日期</span><input id="datePicker" type="text">
       </label>
       <label for="phone">
           <span>手机号码<em>*</em></span><input type="text" name="tel" v-model="tel">
       </label>
      <label for="" class="phone">
           <div class="code">
                <em>验证码</em>
                <input type="text" placeholder="请输入动态验证码">
                <button class="btn" v-bind:disabled="codeDisable" @click="getCode" >
                    <span v-if="codeStart">{{time+'秒'}}</span>
                    <span v-if="!codeStart">发送动态密码</span>
                </button>
           </div>
       </label>
       <input type="submit" class="submit" text="提交">
     </div>
      <!--弹出框 -->
            <div class="tanchu" v-show="showTan">
                <span>{{msg}}</span>
            </div>
   </div>
</template>
<script>
import weui from 'weui';
export default {
  name: "Card",
  data() {
    return {
      msg: "",
      tel: "",
      time: 60,
      codeStart: false,
      codeDisable: false
    };
  },
  methods: {
    getCode: function() {
      // 校验手机号码
      let reg = /^1(([378][0-9])|(5[^4,\D])|(4[579])|(9[89])|(66))\d{8}$/;
      if (!reg.test(this.tel)) {
        this.showTan = true;
        this.msg = "请输入正确的手机号码！";
        let me = this;
        setTimeout(function() {
          me.showTan = false;
        }, 2000);
        return false;
      }
      this.time = "60";
      this.codeDisable = true;
      this.codeStart = true;
      let me = this;
      let timer = window.setInterval(function() {
        if (me.time-- <= 0) {
          me.codeStart = false;
          me.codeDisable = false;
          window.clearInterval(timer);
        }
      }, 1000);
    }
  }
};
</script>
<style scoped>
.card {
  width: 100%;
  height: 450px;
  margin: 0 auto;
  background: url(../assets/bg.png) no-repeat;
  background-size: 100% 100%;
}

.card .card-goods {
  width: 80%;
  height: 250px;
  display: flex;

  position: relative;
  left: 80px;
  top: 100px;
}

.card .card-goods .goods-img {
  width: 150px;
  height: 150px;
  margin: 10px 15px;
}

.card .card-goods .goods-img img {
  width: 100%;
}

.card .card-goods .goods-info {
  flex: 1;
}

.card .card-goods .goods-info h3 {
  font-size: 36px;
  margin: 10px 0;
}
.card .card-goods .goods-info p {
  font-size: 14px;
  line-height: 40px;
  color: grey;
}

.card .card-goods .goods-info p:nth-of-type(3) {
  line-height: 60px;
  color: coral;
}

.card .card-form {
  width: 100%;
  margin-top: 200px;
}

.card .card-form label {
  width: 100%;
  height: 120px;
  line-height: 120px;
  display: flex;
  border-bottom: 1px solid #f1f1f1;
}
.card .card-form label span {
  width: 120px;
  font-size: 24px;
  margin: 0 30px;
}

.card .card-form label input {
  flex: 1;
  padding: 0 10px;
  margin: 35px 20px;
  height: 50px;
  border: none;
}
.card .card-form label:nth-of-type(3) {
  border: none;
}
.card .card-form label:nth-of-type(3) span {
  color: coral;
}
.card .card-form label:nth-of-type(3) span em {
  font-size: 30px;
  margin: 0 10px;
}
.card .card-form label.phone {
  width: 100%;
  height: 120px;
  line-height: 120px;
  display: flex;
  flex-direction: column;
}
.card .card-form label.phone .title {
  width: 100%;
  height: 60px;
  display: flex;
}
.card .card-form label.phone .title span {
  width: 120px;
  height: 80px;
  line-height: 80px;
  display: block;
  color: coral;
}

.card .card-form label.phone .title input {
  flex: 1;
}

.card .card-form label.phone .code {
  flex: 1;
}

.card .card-form label.phone .code em {
  width: 100px;
  height: 50px;
  line-height: 50px;
  margin: 0 30px;
  font-style: normal;
}

.card .card-form label.phone .code input {
  width: 300px;
  padding: 0 10px;
  font-size: 20px;
  height: 50px;
  line-height: 50px;
  margin: 0;
}
.card .card-form label.phone .code .btn {
  display: inline-block;
  background: #fff;
  border: none;
}
.card .card-form label.phone .code .btn span {
  width: 200px;
  height: 50px;
  line-height: 50px;
  border: 0;
  background: #fff;
  color: coral;
  border-left: 1px solid #ccc;
  margin: 0 20px;
  padding: 0 20px;
}

.card .card-form .submit {
  display: block;
  width: 90%;
  height: 80px;
  margin: 200px auto;
  background: coral;
  border: none;
  color: #fff;
  font-size: 30px;
}

.card .tanchu {
  width: auto;
  height: 100px;
  padding: 0 5px;
  font-size: 20px;
  line-height: 100px;
  text-align: center;
  border-radius: 10px;
  position: absolute;
  top: 50%;
  left: 50%;
  color: #fff;
  background: rgba(0, 0, 0, 0.3);
  transform: translate(-50%, -50%);
}
</style>

