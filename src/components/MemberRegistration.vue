<script setup>
  import MemberRegistrationStep1 from './MemberRegistrationStep1.vue'
  import MemberRegistrationStep2 from './MemberRegistrationStep2.vue'
  import MemberRegistrationStep3 from './MemberRegistrationStep3.vue'
  import MemberRegistrationCompleted from './MemberRegistrationCompleted.vue'
</script>

<template>
  <div class="member-form">
    <h1>회원가입</h1>
    <form onsubmit="return false;">
      <fieldset>
        <legend>회원가입 정보 입력란</legend>
        <MemberRegistrationStep1 />
        <MemberRegistrationStep2 />
        <MemberRegistrationStep3 />
        <MemberRegistrationCompleted />
      </fieldset>
    </form>
  </div>
</template>

