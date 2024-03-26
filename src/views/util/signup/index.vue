<template>
	<div class="sub-page">
		<main class="main">
			<div class="util-form join">
				<h2>회원가입</h2>
				<div class="input-wrap">
					<div class="input-form">
						<div style="position: relative">
							<input
								autocomplete="off"
								type="text"
								ref="userId"
								title="아이디"
								placeholder="아이디를 입력해 주세요."
								v-model="userId"
							/>
							<button type="button" class="id_check" @click="checkDuplicateId">
								중복확인
							</button>
						</div>
						<input
							autocomplete="off"
							type="password"
							ref="password"
							title="비밀번호"
							placeholder="비밀번호를 입력해 주세요."
							v-model="password"
						/>
						<input
							autocomplete="off"
							type="text"
							ref="nickName"
							title="닉네임"
							placeholder="닉네임을 입력해 주세요."
							v-model="nickName"
						/>
						<input
							autocomplete="off"
							type="text"
							ref="email"
							title="이메일"
							placeholder="이메일을 입력해 주세요."
							v-model="email"
						/>
						<input
							autocomplete="off"
							type="text"
							ref="phoneNumber"
							title="휴대폰번호"
							placeholder="휴대폰번호를 입력해 주세요.('-'(하이픈) 제외)"
							v-model="phoneNumber"
						/>
					</div>
					<div class="btn-area join">
						<button type="button" @click="actionSignup">회원가입</button>
					</div>
				</div>
			</div>
		</main>
	</div>
</template>

<script>
import axiosHandler from '@/api/proxyHandler';

export default {
	data() {
		return {
			userId: '',
			password: '',
			nickName: '',
			email: '',
			phoneNumber: '',
		};
	},

	mounted() {
		this.$refs.userId.focus();
	},

	methods: {
		checkDuplicateId() {
			console.log(this.userId);
		},

		validationInfo() {
			if (
				!this.userId ||
				!this.password ||
				!this.nickName ||
				!this.email ||
				!this.phoneNumber
			) {
				alert('회원정보를 입력 후 다시 시도해 주세요.');
				return false;
			}

			// const idRegex = /^[a-zA-Z0-9!@#$%^&*()_+=\\[\\]{};':\\"|,.<>\/?]{5,20}$/;
			// const passwordRegex =
			// 	/^(?=.*[a-zA-Z])(?=.*[\d])(?=.*[!@#$%^&*()_+\-=\\[\\]{};':\\"|,.<>?]).{9,20}$/;
			// const nickNameRegex =
			// 	/^[가-힣a-zA-Z0-9!@#$%^&*()_+=\\[\\]{};':\\"|,.<>\/?]{2,50}$/;
			// const emailRegex = /^[a-zA-Z0-9]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$/;
			// const phoneNumberRegex = /^\d{3}\d{3,4}\d{4}$/;

			// if (!idRegex.test(this.userId)) {
			// 	alert('아이디가 잘못되었습니다. 다시 입력해주세요.');
			// 	this.userId = '';
			// 	this.$refs.userId.focus();
			// 	return false;
			// }

			// if (!passwordRegex.test(this.password)) {
			// 	alert('비밀번호가 잘못되었습니다. 다시 입력해주세요.');
			// 	this.password = '';
			// 	this.$refs.password.focus();
			// 	return false;
			// }

			// if (!nickNameRegex.test(this.nickName)) {
			// 	alert('닉네임이 잘못되었습니다. 다시 입력해주세요.');
			// 	this.nickName = '';
			// 	this.$refs.nickName.focus();
			// 	return false;
			// }

			// if (!emailRegex.test(this.email)) {
			// 	alert('이메일이 잘못되었습니다. 다시 입력해주세요.');
			// 	this.email = '';
			// 	this.$refs.email.focus();
			// 	return false;
			// }

			// if (!phoneNumberRegex.test(this.phoneNumber)) {
			// 	alert('핸드폰번호가 잘못되었습니다. 다시 입력해주세요.');
			// 	this.phoneNumber = '';
			// 	this.$refs.phoneNumber.focus();
			// 	return false;
			// }

			return true;
		},

		async actionSignup() {
			if (!this.validationInfo()) return;

			const params = {
				userId: this.userId,
				password: this.password,
				nickName: this.nickName,
				email: this.email,
				phoneNumber: this.phoneNumber,
			};

			const res = await axiosHandler('post', '/api/user', params);

			console.log(res);
			if (res.data.result === 'ERROR') {
				alert(res.data.data.message);
				return;
			}

			alert('회원가입이 완료되었습니다.');
			this.$router.push('/login');
		},
	},
};
</script>
