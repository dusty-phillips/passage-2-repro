<script lang="ts">
	import '@passageidentity/passage-elements/passage-auth';
	import { Passage } from '@passageidentity/passage-js';

	const passage = new Passage('fy4RrKFzAplSbEFxzTMtTVG0');

	let userInfo = null;

	passage.currentUser
		.userInfo()
		.then((u) => {
			console.log('success userInfo');
			userInfo = u;
		})
		.catch((e) => {
			console.log('error user info, refreshing token', e);
			return passage.session.refresh();
		})
		.then((r) => console.log('success refresh', r))
		.catch((e) => console.log('error refresh', e));

	$: console.log(userInfo);
</script>

{#if userInfo}
	<h1>
		Logged in as {userInfo.email}
	</h1>
{/if}

<passage-auth app-id="fy4RrKFzAplSbEFxzTMtTVG0"></passage-auth>

<style>
	h1 {
		color: blue;
	}
</style>
