<template>
  <div class="main__left-content">
    <h3 class="main__left-content__check">結帳</h3>
    <div class="main__left-content__stepper-panel">
      <!-- stepper -->
      <div class="stepper-wrapper">
        <div class="step active">
          <div class="step-circle"></div>
          <div class="label-container">寄送地址</div>
        </div>
        <div class="step">
          <div class="step-circle"></div>
          <span class="connect-line"></span>
          <div class="label-container">運送方式</div>
        </div>
        <div class="step">
          <div class="step-circle"></div>
          <span class="connect-line"></span>
          <div class="label-container">付款資訊</div>
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
          <div class="d-flex justify-content-between">
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
      <!-- second page -->
      <div class="part" v-show="page === 2">
        <!-- step title -->
        <div class="form__movement-title">
          <h4 class="form__movement-title-text">運送方式</h4>
        </div>
        <!-- form content -->
        <div class="form__transport">
          <div class="form__transport-standard">
            <input name="transport" type="radio" value="standard" checked />
            <label for="">
              <p class="transport-way">
                標準運送<br /><span>約3~7個工作天</span>
              </p>
            </label>
            <p class="transport-price">免費</p>
          </div>
          <div class="form__transport-express">
            <input name="transport" type="radio" value="express" />
            <label for="">
              <p class="transport-way">
                DHL貨運<br /><span>48小時內送達</span>
              </p>
            </label>
            <p class="transport-price">$500</p>
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
      <button class="prev" :class="{ show: isSeen }" @click="prevPage">
        &larr;上一步
      </button>
      <button class="next" @click="nextPage">下一步&rarr;</button>
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      page: 1,
      isSeen: false,
    };
  },
  methods: {
    nextPage() {
      if (this.page >= 3) {
        return;
      }
      this.page++;
    },
    prevPage() {
      if (this.page <= 1) {
        return;
      }
      this.page--;
    },
  },
};
</script>

<style scoped>
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

.form__info__title {
  width: 40%;
}
.form__info__name {
  width: 50%;
}
.form__payment__expire,
.form__payment__cvc {
  width: 45%;
}

input, select {
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
}
.form__transport-standard .transport-way,
.form__transport-express .transport-way {
  width: 100%;
  font-size: 14px;
  margin-right: 186px;
}
.form__transport-standard .transport-price,
.form__transport-express .transport-price {
  font-size: 12px;
  margin-bottom: 22px;
}
.form__transport-standard span,
.form__transport-express span {
  font-size: 12px;
}


.form__movement-title-text {
  margin: 24px 0;
  font-size: 24px;
  font-weight: 700;
}
</style>