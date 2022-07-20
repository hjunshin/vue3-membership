<script>
  export default {
    name: "MemberRegistrationStep3",
    props: {
      steps: Number,
      info: Object,
    },
    emits: ["next"],
    methods: {
      handleStepNext() {
        this.$emit("next");
      },
      // 유효성 체크
      handleValidation() {
        this.handleStepNext();
      },
    },
  }
</script>

<template>
  <div class="member-step" v-if="steps === 3">
    <h2>회원가입 3단계</h2>
    <div class="member-input-list">
      <div class="member-input">
        <label for="">카드번호</label>
        <div class="input">
          <input type="text" name="" id="">
          <label for=""><input type="text" name="" id=""></label>
          <label for=""><input type="text" name="" id=""></label>
          <label for=""><input type="text" name="" id=""></label>
        </div>
      </div>
    </div>
    <button type="button" @click="handleValidation">완료</button>
  </div>
</template>
