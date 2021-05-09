<script>
	import BouncingLoader from '$lib/BouncingLoader.svelte';
	import Pagination from '$lib/Pagination.svelte';
	import { onMount } from 'svelte';

	let notices = [];
	let loading = true;

	async function getNews(page = 1) {
		loading = true;
		const { data } = await fetch(
			`${
				import.meta.env.VITE_SVELTEKIT_API_PATH
			}/api/news?${new URLSearchParams({
				class_type: 0,
				support_type: 1,
				page
			})}`
		).then(res => res.json());

		loading = false;
		notices = data;
	}

	const onPageChange = page => getNews(page);

	onMount(getNews);
	// { list, total, current_page }
</script>

<svelte:head>
	<title>公告 - 薄荷BOHE加速器</title>
	<meta name="keywords" content="薄荷BOHE加速器" />
	<meta
		name="description"
		content="薄荷加速器专业的网络游戏加速工具，完美加速漫威复仇者联盟、彩虹六号、GTA5、糖豆人、无限法则、NBA2K21、战地等上百款海外游戏，有效解决游戏中出现的延迟、丢包、卡顿等问题"
	/>
</svelte:head>

<div class="jum">
	<div class="title mx-auto select-none">官方公告 Official Announcement</div>
</div>
<section class="mx-auto py-4">
	{#if loading}
		<BouncingLoader />
	{:else}
		<ul class="notices flex flex-col">
			{#each notices?.list as notice}
				<li class="notice cursor-pointer hover:shadow rounded p-4">
					<a sveltekit:prefetch href={`/notice/${notice.id}`}>
						<div class="title text-lg text-gray-800">
							{notice.title}
						</div>
						<div class="summary text-sm text-gray-400 mt-2">
							{notice.summary}
						</div>
					</a>
				</li>
			{/each}
		</ul>
		<Pagination
			pagination={{
				total: Math.ceil(notices.total / notices.per_page),
				index: notices.current_page
			}}
			{onPageChange}
		/>
	{/if}
</section>

<style lang="scss">
	.jum {
		height: 320px;
		background-image: url('/img/notice/block.png');
		background-size: 1920px 322px;
		background-position: center bottom;
		color: var(--primary);

		.title {
			width: 1200px;
			line-height: 320px;
			font-size: xxx-large;
		}
	}
	section {
		width: 1200px;

		ul.notices {
			li.notice {
				+ li {
					margin-top: 10px;
				}
			}
		}
	}
</style>
