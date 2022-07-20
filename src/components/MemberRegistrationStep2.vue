<script>
  export default {
    name: "MemberRegistrationStep2",
    props: {
      steps: Number,
    },
    emits: ["prev", "next"],
    methods: {
      handleStepPrev() {
        this.$emit("prev");
      },
      handleStepNext() {
        this.$emit("next");
      },
    },
  }
</script>

<template>
  <div class="member-step" v-if="steps === 2">
    <h2>회원가입 2단계</h2>
    <div class="member-input-list">
      <div class="member-input">
        <label for="member_name">이름</label>
        <input type="text" name="member_name" id="member_name" maxlength="20" />
      </div>
      <div class="member-input">
        <label for="member_cellphone">연락처</label>
        <input type="text" name="member_cellphone" id="member_cellphone" maxlength="13" />
      </div>
      <div class="member-input">
        <label for="member_address">주소</label>
        <input type="text" name="member_address" id="member_address" />
      </div>
      <div class="member-input">
        <label for="member_detail_address">상세주소</label>
        <input type="text" name="member_detail_address" id="member_detail_address" />
      </div>
    </div>
    <button type="button" @click="handleStepPrev">이전</button>
    <button type="button" @click="handleStepNext">다음</button>
  </div>
</template>
