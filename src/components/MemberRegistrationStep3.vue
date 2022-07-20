<script>
  export default {
    name: "MemberRegistrationStep3",
    props: {
      steps: Number,
    },
    emits: ["next"],
    methods: {
      handleStepNext() {
        this.$emit("next");
      },
    },
  }
</script>

<template>
  <div class="member-step" v-if="steps === 3">
    <h2>회원가입 3단계</h2>
    <div class="member-input-list">
      <div class="member-input">
      </div>
    </div>
    <button type="button" @click="handleStepNext">완료</button>
  </div>
</template>
