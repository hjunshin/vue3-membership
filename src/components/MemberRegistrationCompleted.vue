<script>
  export default {
    name: 'MemberRegistrationCompleted',
    props: {
      steps: Number,
      info: Object,
    },
  }
</script>

<template>
  <div class="member-step" v-if="steps === 4">
    <h2>회원가입 완료</h2>
    <p>
      '{{info.name}}'님<br />
      회원가입 되었습니다.
    </p>
    <dl>
      <dt>이메일:</dt>
      <dd>{{info.email}}</dd>
      <dt>주소:</dt>
      <dd>
        {{info.address}}<br />
        {{info.detailAddress}}
      </dd>
      <dt>연락처:</dt>
      <dd>{{info.cellphone}}</dd>
    </dl>
  </div>
</template>
