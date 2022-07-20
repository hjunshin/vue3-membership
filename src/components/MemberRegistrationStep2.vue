<script>
  export default {
    name: "MemberRegistrationStep2",
    data() {
      return {
        isBtnDisabled: true,
      }
    },
    props: {
      steps: Number,
      info: Object,
    },
    emits: ["prev", "next"],
    methods: {
      handleStepPrev() {
        this.$emit("prev");
      },
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
  <div class="member-step" v-if="steps === 2">
    <h2>회원가입 2단계</h2>
    <div class="member-input-list">
      <div class="member-input">
        <label for="member_name">이름</label>
        <input
          type="text"
          name="member_name"
          id="member_name"
          maxlength="20"
          v-model="info.name"
        />
      </div>
      <div class="member-input">
        <label for="member_cellphone">연락처</label>
        <input
          type="text"
          name="member_cellphone"
          id="member_cellphone"
          maxlength="13"
          v-model="info.cellphone"
        />
      </div>
      <div class="member-input">
        <div>
          <label for="member_address">주소</label>
          <button type="button">주소 검색</button>
        </div>
        <input
          type="text"
          name="member_address"
          id="member_address"
          v-model="info.address"
        />
      </div>
      <div class="member-input">
        <label for="member_detail_address">상세주소</label>
        <input
          type="text"
          name="member_detail_address"
          id="member_detail_address"
          v-model="info.detailAddress"
        />
      </div>
    </div>
    <button type="button" @click="handleStepPrev">이전</button>
    <button
      type="button"
      :disabled="isBtnDisabled"
      @click="handleValidation"
    >
      다음
    </button>
  </div>
</template>
