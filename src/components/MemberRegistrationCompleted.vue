<script>
  export default {
    name: "MemberRegistrationCompleted",
    props: {
      steps: Number,
    },
  }
</script>

<template>
  <div class="member-step" v-if="steps === 4">
    <h2>회원가입 완료</h2>
  </div>
</template>
