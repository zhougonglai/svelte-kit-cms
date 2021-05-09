<script context="module">
	export async function load({ page: { query } }) {
		return {
			props: {
				tab: query.has('tab') ? query.get('tab') : 'default'
			}
		};
	}
</script>

<script>
	export let tab = 'default';

	const tabs = {
		menus: {
			default: 'BOHE加速器',
			company: '公司介绍',
			contact: '联系我们',
			join: '加入我们'
		}
	};
</script>

<svelte:head>
	<title>{tabs.menus[tab]}</title>
</svelte:head>

<section>
	<div class="tabs">
		<div class="tab-bars">
			<div class="tab-bar">
				{tabs.menus[tab]}
			</div>
		</div>
	</div>
</section>
