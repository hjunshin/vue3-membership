<script>
  export default {
    name: "MemberRegistrationStep1",
    props: {
      steps: Number,
      info: Object,
    },
    emits: ["next"],
    methods: {
      inputFocus({ refName = null }) {
        if (!refName) {
          return;
        }
        this.$refs[refName].focus();
      },
      inputValidation() {
        const info = this.info;
        const email = info.email;
        const password = info.password;
        const passwordConfirm = info.passwordConfirm;

        const alertMessage = {
          email: '이메일을 다시 확인해 주세요',
          password: '비밀번호를 다시 확인해 주세요',
          passwordConfirm: '비밀번호 확인을 다시 확인해 주세요',
          passwordUnequal: '비밀번호가 일치하지 않습니다',
        }

        const regex = {
          email: /([\w-\.]+)@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.)|(([\w-]+\.)+))([a-zA-Z]{2,4}|[0-9]{1,3})(\]?)$/,
          password: /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$/,
        }

        // 이메일 형식 확인
        if (!regex.email.test(email)) {
          alert(alertMessage.email);
          this.inputFocus({
            refName: 'email',
          });
          return false;
        }

        // 비밀번호 형식 확인
        if (!regex.password.test(password)) {
          alert(alertMessage.password);
          this.inputFocus({
            refName: 'password',
          });
          return false;
        }

        // 비밀번호 확인 형식 확인
        if (!regex.password.test(passwordConfirm)) {
          alert(alertMessage.passwordConfirm);
          this.inputFocus({
            refName: 'passwordConfirm',
          });
          return false;
        }

        // 비밀번호와 비밀번호 확인 동일 여부 확인
        if (password !== passwordConfirm) {
          alert(alertMessage.passwordUnequal);
          this.inputFocus({
            refName: 'passwordConfirm',
          });
          return false;
        }

        return true;
      },
      handleStepNext() {
        if (!this.inputValidation()) {
          return;
        }
        this.$emit("next");
      },
    },
    mounted() {
      this.inputFocus({
        refName: 'email',
      });
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
          ref="email"
        />
      </div>
      <div class="member-input">
        <label for="member_password">비밀번호</label>
        <input
          type="password"
          name="member_password"
          id="member_password"
          v-model="info.password"
          ref="password"
        />
      </div>
      <div class="member-input">
        <label for="member_password_confirm">비밀번호 확인</label>
        <input
          type="password"
          name="member_password_confirm"
          id="member_password_confirm"
          v-model="info.passwordConfirm"
          ref="passwordConfirm"
        />
      </div>
    </div>
    <button
      type="button"
      @click="handleStepNext"
    >
      다음
    </button>
  </div>
</template>
