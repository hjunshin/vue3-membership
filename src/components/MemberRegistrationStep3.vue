<script>
  export default {
    name: 'MemberRegistrationStep3',
    props: {
      steps: Number,
      info: Object,
    },
    emits: ['next'],
    methods: {
      cardNumberValidation({ cardNumber = null }) {
        if (!cardNumber) {
          return;
        }

        const cardNumberReverse = cardNumber.split('').reverse();
        let cardNumberArray = Array.from(cardNumberReverse);
        const cardLastNumber = Number(cardNumberArray.pop());

        cardNumberArray = cardNumberReverse.map((number, index) => {
          if(index % 2 === 0) {
            return number * 2;
          } else {
            return number;
          }
        });

        cardNumberArray = cardNumberReverse.map((number) => {
          if(number > 9) {
            return number - 9;
          } else {
            return number;
          }
        });

        let sumCardNumber = cardNumberArray.reduce((acc, curr) => acc + curr, 0);
        sumCardNumber += cardLastNumber;

        const modulus =  sumCardNumber % 10;
        return !modulus;
      },
      inputFocus({ refName = null }) {
        if (!refName) {
          return;
        }
        this.$refs[refName].focus();
      },
      inputValidation() {
        const info = this.info;
        const cardNumber1 = info.cardNumber1;
        const cardNumber2 = info.cardNumber2;
        const cardNumber3 = info.cardNumber3;
        const cardNumber4 = info.cardNumber4;

        const alertMessage = {
          cardNumber: '카드번호를 다시 확인해 주세요',
          cardNumberValid: '카드번호가 유효하지 않습니다',
        }

        if (!cardNumber1 || cardNumber1.length < 4) {
          alert(alertMessage.cardNumber);
          this.inputFocus({
            refName: 'cardNumber1',
          });
          return false;
        }

        if (!cardNumber2 || cardNumber2.length < 4) {
          alert(alertMessage.card);
          this.inputFocus({
            refName: 'cardNumber2',
          });
          return false;
        }

        if (!cardNumber3 || cardNumber3.length < 4) {
          alert(alertMessage.card);
          this.inputFocus({
            refName: 'cardNumber3',
          });
          return false;
        }

        if (!cardNumber4 || cardNumber4.length < 4) {
          alert(alertMessage.card);
          this.inputFocus({
            refName: 'cardNumber4',
          });
          return false;
        }

        const cardNumber = cardNumber1 + cardNumber2 + cardNumber3 + cardNumber4;
        const cardNumberValid = this.cardNumberValidation({ cardNumber });

        if (!cardNumberValid) {
          alert(alertMessage.cardNumberValid);
          return false;
        }

        return true;
      },
      handleStepNext() {
        if (!this.inputValidation()) {
          return;
        }
        this.$emit('next');
      },
    },
  }
</script>

<template>
  <div class="member-step" v-if="steps === 3">
    <h2>회원가입 3단계</h2>
    <div class="member-input-list">
      <div class="member-input">
        <label for="member_card_number1">카드번호</label>
        <div class="input">
          <input
            type="text"
            name="member_card_number1"
            id="member_card_number1"
            inputmode="numeric"
            maxlength="4"
            v-model="info.cardNumber1"
            ref="cardNumber1"
          />
          <label for="member_card_number2">
            <input
              type="text"
              name="member_card_number2"
              id="member_card_number2"
              inputmode="numeric"
              maxlength="4"
              v-model="info.cardNumber2"
              ref="cardNumber2"
            />
          </label>
          <label for="member_card_number3">
            <input
              type="text"
              name="member_card_number3"
              id="member_card_number3"
              inputmode="numeric"
              maxlength="4"
              v-model="info.cardNumber3"
              ref="cardNumber3"
            />
          </label>
          <label for="member_card_number4">
            <input
              type="text"
              name="member_card_number4"
              id="member_card_number4"
              inputmode="numeric"
              maxlength="4"
              v-model="info.cardNumber4"
              ref="cardNumber4"
            />
          </label>
        </div>
      </div>
    </div>

    <div class="btn-wrap">
      <button
        type="button"
        @click="handleStepNext"
      >
        완료
      </button>
    </div>
  </div>
</template>
