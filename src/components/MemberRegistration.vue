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
          info: {
            email: '',
            password: '',
            passwordConfirm: '',
            name: '',
            cellphone: '',
            postCode: '',
            address: '',
            detailAddress: '',
          }
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
    }
  }
</script>

<template>
  <header>
      <h1>회원가입</h1>
  </header>
  <main>
    <div class="member-form">
      <form onsubmit="return false;">
        <fieldset>
          <legend>회원가입 정보 입력란</legend>
          <MemberRegistrationStep1
            :steps="member.steps"
            :info="member.info"
            @next="handleStepNext"
          />
          <MemberRegistrationStep2
            :steps="member.steps"
            :info="member.info"
            @next="handleStepNext"
            @prev="handleStepPrev"
          />
          <MemberRegistrationStep3
            :steps="member.steps"
            :info="member.info"
            @next="handleStepNext"
            @prev="handleStepPrev"
          />
          <MemberRegistrationCompleted
            :steps="member.steps"
            :info="member.info"
            @next="handleStepNext"
          />
        </fieldset>
      </form>
    </div>
  </main>
</template>
