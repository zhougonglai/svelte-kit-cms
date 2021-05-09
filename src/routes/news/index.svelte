<script>
	import BouncingLoader from '$lib/BouncingLoader.svelte';
	import { onMount } from 'svelte';
	let newses = [],
		loading = true;

	async function getNews() {
		loading = true;
		const { data } = await fetch(
			`${
				import.meta.env.VITE_SVELTEKIT_API_PATH
			}/api/news?${new URLSearchParams({
				class_type: 2,
				support_type: 1
			})}`
		).then(res => res.json());

		return data.list;
	}

	onMount(async () => {
		newses = await getNews();
		loading = false;
	});
</script>

<svelte:head>
	<title>资讯 - 薄荷BOHE加速器</title>
	<meta name="keywords" content="薄荷BOHE加速器" />
	<meta
		name="description"
		content="薄荷加速器专业的网络游戏加速工具，完美加速漫威复仇者联盟、彩虹六号、GTA5、糖豆人、无限法则、NBA2K21、战地等上百款海外游戏，有效解决游戏中出现的延迟、丢包、卡顿等问题"
	/>
</svelte:head>

<section class="mx-auto py-4">
	<ul class="activitys flex flex-col">
		{#if loading}
			<BouncingLoader />
		{:else}
			{#each newses as news}
				<li class="activity cursor-pointer hover:shadow rounded p-4">
					<a
						sveltekit:prefetch
						href={`/news/${news.id}`}
						class="grid grid-flow-col overflow-hidden"
					>
						<div class="cover mr-2 row-span-4 flex items-center justify-center">
							<img
								src={`${import.meta.env.VITE_SVELTEKIT_FILEPATH}${
									news.image_url
								}`}
								alt={news.title}
							/>
						</div>
						<div class="title col-span-2 text-lg text-gray-800">
							{news.title}
						</div>
						<div
							class="summary row-span-2 col-span-2 text-sm text-gray-400 mt-2"
						>
							{news.summary}
						</div>
						<div class="status">
							<time
								>{news.publish_time_year}-{news.publish_time_month}-{news.publish_time_day}</time
							>
						</div>
					</a>
				</li>
			{/each}
		{/if}
	</ul>
</section>

<style lang="scss">
	section {
		width: 1200px;

		ul.activitys {
			li.activity {
				+ li {
					margin-top: 10px;
				}

				a {
					.cover {
						width: 240px;
						height: 140px;
					}

					.summary {
						flex: 1;
					}
				}
			}
		}
	}
</style>
