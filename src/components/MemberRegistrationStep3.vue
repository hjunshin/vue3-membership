<script>
  export default {
    name: 'MemberRegistrationStep3',
    props: {
      steps: Number,
      info: Object,
    },
    emits: ['next'],
    methods: {
      handleStepNext() {
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
          />
          <label for="member_card_number2">
            <input
              type="text"
              name="member_card_number2"
              id="member_card_number2"
              maxlength="4"
            />
          </label>
          <label for="member_card_number3">
            <input
              type="text"
              name="member_card_number3"
              id="member_card_number3"
              maxlength="4"
            />
          </label>
          <label for="member_card_number4">
            <input
              type="text"
              name="member_card_number4"
              id="member_card_number4"
              maxlength="4"
            />
          </label>
        </div>
      </div>
    </div>
    <button
      type="button"
      @click="handleStepNext"
    >
      완료
    </button>
  </div>
</template>
