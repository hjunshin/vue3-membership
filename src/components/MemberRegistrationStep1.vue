<script>
  export default {
    name: "MemberRegistrationStep1",
    data() {
      return {
        isBtnDisabled: true,
      }
    },
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
        const info = this.info;
        const email = info.email;
        const password = info.password;
        const passwordConfirm = info.passwordConfirm;

        const regex = {
          email: /([\w-\.]+)@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.)|(([\w-]+\.)+))([a-zA-Z]{2,4}|[0-9]{1,3})(\]?)$/,
          password: '',
        }

        if (!regex.email.test(email)) {
          return;
        }

        this.handleStepNext();
      },
    },
  }
</script>

<template>
  <div class="member-step" v-if="steps === 1">
    <h2>회원가입 1단계</h2>
    <div class="member-input-list">
      <div class="member-input">
        <label for="member_email">이메일</label>
        <input
          type="email"
          name="member_email"
          id="member_email"
          v-model="info.email"
        />
      </div>
      <div class="member-input">
        <label for="member_password">비밀번호</label>
        <input
          type="password"
          name="member_password"
          id="member_password"
          v-model="info.password"
        />
      </div>
      <div class="member-input">
        <label for="member_password_confirm">비밀번호 확인</label>
        <input
          type="password"
          name="member_password_confirm"
          id="member_password_confirm"
          v-model="info.passwordConfirm"
        />
      </div>
    </div>
    <button
      type="button"
      :disabled="isBtnDisabled"
      @click="handleValidation"
    >
      다음
    </button>
  </div>
</template>
