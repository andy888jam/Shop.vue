<template>
  <div class="main__left-content">
    <h3 class="main__left-content__check">結帳</h3>
    <div class="main__left-content__stepper-panel">
      <!-- stepper -->
      <div class="stepper-wrapper">
        <div class="step" v-for="step in steps" :key="step.id">
          <div class="step-circle checked" v-if="step.stepNum <= page - 1">
            &#10004;
          </div>
          <div class="step-circle active" v-else-if="step.stepNum === page">
            {{ step.stepNum }}
          </div>
          <div class="step-circle" v-else>{{ step.stepNum }}</div>
          <span class="connect-line active-line" v-if="step.stepNum <= page && step.stepNum > 1"></span>
          <span class="connect-line" v-else-if="step.stepNum > 1"></span>
          <div class="label-container">{{ step.content }}</div>
        </div>
      </div>
    </div>
    <!-- form -->
    <div class="form">
      <!-- first page -->
      <div class="part" v-show="page === 1">
        <!-- step title -->
        <div class="form__movement-title">
          <h4 class="form__movement-title-text">寄送地址</h4>
        </div>
        <!-- form content -->
        <div class="form__info">
          <div class=" form-row-1 d-flex justify-content-between">
            <div class="form-row form__info__title">
              <label for="">稱謂</label>
              <div class="select-wrapper">
                <select name="title" required>
                  <option value="sir" selected>先生</option>
                  <option value="miss">小姐</option>
                </select>
              </div>
            </div>
            <div class="form-row form__info__name">
              <label for="">姓名</label
              ><input id="name" type="text" placeholder="請輸入姓名" required />
            </div>
          </div>
          <div class="form-row-2"> 
            <div class="form-row form__info__telephone">
              <label for="">電話</label
              ><input
                id="telephone"
                type="text"
                placeholder="請輸入行動電話"
                required
              />
            </div>
            <div class="form-row form__info__email">
              <label for="">Email</label
              ><input
                id="email"
                type="text"
                placeholder="請輸入電子郵件"
                required
              />
            </div>
          </div>
          <div class="form-row-3"> 
            <div class="form-row form__info__city">
              <label for="">縣市</label>
              <div class="select-wrapper">
                <select name="city" id="" required>
                  <option value="" selected>請選擇縣市</option>
                  <option value="taipei">台北</option>
                  <option value="taichung">台中</option>
                  <option value="kaohsiung">高雄</option>
                </select>
              </div>
            </div>
            <div class="form-row form__info__address">
              <label for="">地址</label
              ><input id="addess" type="text" placeholder="請輸入地址" required />
            </div>
          </div>
        </div>
      </div>
      <!-- second page -->
      <div class="part" v-show="page === 2">
        <!-- step title -->
        <div class="form__movement-title">
          <h4 class="form__movement-title-text">運送方式</h4>
        </div>
        <!-- form content -->
        <div class="form__transport">
          <div class="form__transport-standard">
            <input name="transport" type="radio" value="standard" checked @click="free"/>
            <label for="" class="transport-detail">
              <p class="transport-way">
                標準運送<br /><span>約3~7個工作天</span>
              </p>
              <p class="transport-price">免費</p>
            </label>
          </div>
          <div class="form__transport-express">
            <input name="transport" type="radio" value="express"  @click="transportFee"/>
            <label for="" class="transport-detail">
              <p class="transport-way">
                DHL貨運<br /><span>48小時內送達</span>
              </p>
              <p class="transport-price">$500</p>
            </label>
          </div>
        </div>
      </div>
      <!-- third page -->
      <div class="part" v-show="page === 3">
        <!-- step title -->
        <div class="form__movement-title">
          <h4 class="form__movement-title-text">付款資訊</h4>
        </div>
        <!-- form content -->
        <div class="form__payment">
          <div class="form-row form__payment__holder">
            <label for="">持卡人姓名</label
            ><input id="card-holder" type="text" placeholder="John Doe" />
          </div>
          <div class="form-row form__payment__card-number">
            <label for="">卡號</label
            ><input
              id="card-number"
              type="text"
              placeholder="1111 2222 3333 4444"
            />
          </div>
          <div class="d-flex justify-content-between">
            <div class="form-row form__payment__expire">
              <label for="">有效期限</label
              ><input id="expiration-date" type="text" placeholder="MM/YY" />
            </div>
            <div class="form-row form__payment__cvc">
              <label for="">CVC/CCV</label
              ><input id="cvc" type="text" placeholder="123" />
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="container main__button">
      <button class="prev" v-show="isSeen" @click="prevPage">
        &larr;上一步
      </button>
      <button class="next" @click="nextPage" v-if="page <= 2">下一步&rarr;</button>
      <button class="next" @click="nextPage" v-else>確認下單</button>
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      page: 1,
      isSeen: false,
      steps: [
        {
          id: 1,
          stepNum: 1,
          content: "寄送地址",
        },
        {
          id: 2,
          stepNum: 2,
          content: "運送方式",
        },
        {
          id: 3,
          stepNum: 3,
          content: "付款資訊",
        },
      ],
    };
  },
  methods: {
    nextPage() {
      if (this.page >= 3) {
        return;
      }
      this.page++;
      this.isSeen = true;
    },
    prevPage() {
      if (this.page <= 1) {
        return;
      }
      this.page--;
      if(this.page === 1) {
        this.isSeen = false;
      }
    },
    free() {
      this.$emit('free','免費')
    },
    transportFee() {
      this.$emit('transit', '$500')
    }
  },
};
</script>

<style scoped>
/* 初始設定 */
* {
  box-sizing: border-box;
}

/* 掛載用css */
.d-flex {
  display: flex;
}
.justify-content-between {
  justify-content: space-between;
}

.main__left-content__check {
  padding-bottom: 30px;
  font-size: 32px;
}

.stepper-wrapper {
  width: 100%;
  display: flex;
  justify-content: space-between;
}
.step {
  display: flex;
  flex-direction: row;
  align-items: center;
  text-align: center;
  position: relative;
}
.step-circle {
  padding: 3px 0;
  text-align: center;
  height: 32px;
  width: 32px;
  border-radius: 50%;
  background-color: white;
  color: #e5e5e5;
  border: solid 1px #e5e5e5;
}

.active {
  background-color: white;
  color: black;
  border: solid 1px black;
}

.checked {
  padding: 3px 0;
  text-align: center;
  background-color: black;
  color: white;
  border: solid 1px black;
}

.step-circle {
  height: 32px;
  width: 32px;
  border-radius: 50%;
  border: solid 1px;
  position: relative;
}
.connect-line {
  display: block;
  height: 1px;
  width: 60px;
  background-color: #e5e5e5;
  position: absolute;
  top: 16px;
  right: calc(50% + 100px);
}

.active-line {
  background-color: black;
}

.label-container {
  margin-left: 10px;
}

/* form區域 */

.form-row {
  margin-bottom: 16px;
}

.form-row > label {
  display: block;
  margin-bottom: 8px;
  font-weight: 700;
  color: #808080;
  font-size: 12px;
}

.form-row-1, .form-row-2, .form-row-3 {
  display: grid;
  grid-template-columns: repeat(6, 1fr) ;
  column-gap: 1rem;
}

.form__info__title {
  grid-column: 1 / 3;
}
.form__info__name {
  grid-column: 3 / 7;
}
.form__info__telephone{
  grid-column: 1 / 4;
}
.form__info__email{
  grid-column: 4 / 7;
}
.form__info__city {
  grid-column: 1 / 3;
}
.form__info__address {
  grid-column: 3 / 7;
}

.form__payment__holder,
.form__payment__card-number {
  width: 65%;
}

.form__payment__expire,
.form__payment__cvc {
  width: 47%;
}

input,
select {
  border: 1px solid #4a4a4a;
  border-radius: 4px;
  font-size: 12px;
  padding: 12px 0 12px 16px;
  width: 100%;
  color: #999999;
}

input[type="radio"] {
  -webkit-appearance: none;
  border-radius: 50%;
  width: 20px;
  height: 20px;
  margin: 0;
  padding: 0;
  cursor: pointer;
  margin-right: 20px;
  margin-left: 20px;
}
input[type="radio"]:checked {
  box-shadow: inset 0 0 0 5px black;
}

.form__transport-standard,
.form__transport-express {
  display: flex;
  align-items: center;
  border: 1px solid #f0f0f5;
  border-radius: 4px;
  height: 60px;
  margin-bottom: 24px;
  width:90%;
}
.form__transport-standard .transport-way,
.form__transport-express .transport-way {
  width: 100%;
  font-size: 14px;
  margin-right: 186px;
}

.transport-price {
  font-size: 12px;
  width: 20%;
  margin: auto 0;
}

.form__transport-standard span,
.form__transport-express span {
  font-size: 12px;
}

.transport-detail {
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 85%;
}

.form__movement-title-text {
  margin: 24px 0;
  font-size: 24px;
  font-weight: 700;
}

/* 上下一步按鈕區域 */
.main__button {
    width: 100%;
    grid-column: 1 / 7;
    display: grid;
    grid-template-columns: repeat(6, 1fr);
  }

.prev {
  width: 50%;
  height: 46px;
  margin: 24px 0 40px;
  color: black;
  grid-column: 1 / 3;
  text-align: left;

}

.next {
  width: 100%;
  height: 46px;
  margin: 24px 0 40px;
  background-color: #F67599;
  border-radius: 8px;
  color: white;
  grid-column: 5 / 7;
}


</style>