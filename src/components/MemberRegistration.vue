<script setup>
  import MemberRegistrationStep1 from './MemberRegistrationStep1.vue'
  import MemberRegistrationStep2 from './MemberRegistrationStep2.vue'
  import MemberRegistrationStep3 from './MemberRegistrationStep3.vue'
  import MemberRegistrationCompleted from './MemberRegistrationCompleted.vue'
</script>

<script>
  export default {
    name: "MemberRegistration",
    data() {
      return {
        member: {
          steps: 1,
        }
      }
    },
    methods: {
      // 회원가입 다음 단계
      handleStepNext() {
        this.member.steps++;
      },
      // 회원가입 이전 단계
      handleStepPrev() {
        this.member.steps--;
      },
    },
  }
</script>

<template>
  <div class="member-form">
    <h1>회원가입</h1>
    <form onsubmit="return false;">
      <fieldset>
        <legend>회원가입 정보 입력란</legend>
        <MemberRegistrationStep1
          :steps="member.steps"
          @next="handleStepNext"
        />
        <MemberRegistrationStep2
          :steps="member.steps"
          @next="handleStepNext"
          @prev="handleStepPrev"
        />
        <MemberRegistrationStep3
          :steps="member.steps"
          @next="handleStepNext"
          @prev="handleStepPrev"
        />
        <MemberRegistrationCompleted
          :steps="member.steps"
          @next="handleStepNext"
        />
      </fieldset>
    </form>
  </div>
</template>
