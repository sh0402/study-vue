<template>
	<v-menu offset-y v-if="!$store.state.fireUser">
		<template v-slot:activator="{ on }">
			<v-btn icon v-on="on">
				<v-icon>mdi-account</v-icon>
			</v-btn>
		</template>

		<v-card>
			<v-card-title>Login</v-card-title>
			<v-divider />
			<v-card-actions>
				<v-btn color="red" dark @click="signInWithGoogle" block>
					<v-icon left>mdi-google</v-icon>
					Google Log in
				</v-btn>
				<v-card-actions>
					<v-btn color="blue" dark @click="signInWithFacebook" block
						><v-icon left>mdi-facebook</v-icon> 페이스북으로 로그인</v-btn
					>
				</v-card-actions>
			</v-card-actions>
		</v-card>
	</v-menu>
</template>

<template>
	<v-menu offset-y v-else>
		<template v-slot:activator="{ on }">
			<v-btn icon v-on="on">
				<v-avatar size="32">
					<v-img
						:src="'https://www.google.com/images/branding/googlelogo/2x/googlelogo_color_272x92dp.png'"
					></v-img>
				</v-avatar>
			</v-btn>
		</template>

		<v-card>
			<v-card-title>Information</v-card-title>
			<v-card-actions>
				<v-btn color="" dark @click="signOut" block> Log out </v-btn>
			</v-card-actions>
		</v-card>
	</v-menu>
</template>

<script>
export default {
	data() {
		return {
			loading: true
		}
	},
	methods: {
		async signInWithGoogle() {
			const provider = new this.$firebase.auth.GoogleAuthProvider()
			this.$firebase.auth().languageCode = 'ko'
			this.loading = false
			try {
				const sn = await this.$firebase.auth().signInWithPopup(provider)
				this.$store.commit('setFireUser', sn.user)
			} finally {
				this.loading = false
			}
		},
		signOut() {
			this.$firebase.auth().signOut()
		},
		signInWithFacebook() {
			throw Error('나중에 만들께요')
		}
	}
}
</script>

<style></style>
