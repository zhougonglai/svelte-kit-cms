<script context="module">
	export async function load({ page: { params }, fetch }) {
		const { data } = await fetch(
			`${import.meta.env.VITE_SVELTEKIT_API_PATH}/api/news/${params.id}`
		).then(res => {
			console.log(res);
			return res.json();
		});

		return {
			props: {
				title: data.title,
				content: data.content,
				publish_time: data.publish_time
			}
		};
	}
</script>

<script>
	export let title;
	export let content;
	export let publish_time;
</script>

<svelte:head>
	<title>{title} - 薄荷BOHE加速器</title>
	<meta name="keywords" content="薄荷BOHE加速器" />
	<meta
		name="description"
		content="薄荷加速器专业的网络游戏加速工具，完美加速漫威复仇者联盟、彩虹六号、GTA5、糖豆人、无限法则、NBA2K21、战地等上百款海外游戏，有效解决游戏中出现的延迟、丢包、卡顿等问题"
	/>
</svelte:head>

<section class="mx-auto py-4 flex justify-between">
	<article>
		<ul class="breadcrumb">
			<li class="breadcrumb-item">
				<a sveltekit:prefetch href="/">首页</a>
			</li>
			<li class="breadcrumb-item">
				<a sveltekit:prefetch href="/news">全部</a>
			</li>
			<li class="breadcrumb-item active">{title}</li>
		</ul>
		<h1 class="mt-4 text-xl">{title}</h1>
		<h3 class="my-2">
			发布・{publish_time}
		</h3>
		<hr class="my-2" />
		{@html content}
	</article>
	<aside />
</section>

<style lang="scss">
	section {
		width: 1200px;

		article {
			width: 860px;
		}

		aside {
			width: 320px;
		}
	}

	.breadcrumb {
		display: flex;

		&-item {
			&:not(.active) {
				color: gray;
				&:hover {
					color: black;
				}
				&::after {
					content: '>';
					margin: 0 0.75em;
				}
			}
		}
	}
</style>
