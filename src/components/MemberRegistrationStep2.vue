<script>
  export default {
    name: 'MemberRegistrationStep2',
    props: {
      steps: Number,
      info: Object,
    },
    emits: ['prev', 'next'],
    methods: {
      searchAddresses() {
        const popupWidth = 500;
        const popupHeight = 600;

        new daum.Postcode({
          width: popupWidth,
          height: popupHeight,
          oncomplete: function(data) {
            this.$emit('info.address', data.address);
            console.log('data', data);
          }
        }).open({
          left: (window.screen.width / 2) - (popupWidth / 2),
          top: (window.screen.height / 2) - (popupHeight / 2)
        });
      },
      inputFocus({ refName = null }) {
        if (!refName) {
          return;
        }
        this.$refs[refName].focus();
      },
      inputValidation() {
        const info = this.info;
        const name = info.name;
        const cellphone = info.cellphone;
        const address = info.address;
        const detailAddress = info.detailAddress;

        const alertMessage = {
          name: '이름을 다시 확인해 주세요',
          cellphone: '연락처를 다시 확인해 주세요',
          address: '',
          detailAddress: '',
        }

        const regex = {
          nameKor: /^([가-힣]+){2,}$/,
          nameEn: /^([a-zA-Z]+){3,}$/,
          cellphone: /^010-?([0-9]{3,4})-?([0-9]{4})$/,
          cellphoneSpace: /^010 ([0-9]{3,4}) ([0-9]{4})$/,
          address: '',
          detailAddress: '',
        }

        // 이름 형식 확인
        if (
          !regex.nameKor.test(name)
          && !regex.nameEn.test(name)
        ) {
          alert(alertMessage.name);
          this.inputFocus({
            refName: 'name',
          });
          return false;
        }

        // 연락처 형식 확인
        if (
          !regex.cellphone.test(cellphone)
          && !regex.cellphoneSpace.test(cellphone)
        ) {
          alert(alertMessage.cellphone);
          this.inputFocus({
            refName: 'cellphone',
          });
          return false;
        }

        return true;
      },
      handleStepPrev() {
        this.$emit('prev');
      },
      handleStepNext() {
        if (!this.inputValidation()) {
          return;
        }
        this.$emit('next');
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
          ref="name"
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
          ref="cellphone"
        />
      </div>
      <div class="member-input">
        <div>
          <label for="member_address">주소</label>
          <button
            type="button"
            @click="searchAddresses"
          >
            주소 검색
          </button>
        </div>
        <input
          type="text"
          name="member_address"
          id="member_address"
          v-model="info.address"
          ref="address"
        />
      </div>
      <div class="member-input">
        <label for="member_detail_address">상세주소</label>
        <input
          type="text"
          name="member_detail_address"
          id="member_detail_address"
          v-model="info.detailAddress"
          ref="detailAddress"
        />
      </div>
    </div>
    <button type="button" @click="handleStepPrev">이전</button>
    <button
      type="button"
      @click="handleStepNext"
    >
      다음
    </button>
  </div>
</template>
