<script context="module">
	export async function load({ fetch }) {
		const {
			data: { total, current_page, list }
		} = await fetch(
			`${
				import.meta.env.VITE_SVELTEKIT_API_PATH
			}/api/news?${new URLSearchParams({
				size: 15,
				class_type: 0,
				support_type: 1
			})}`
		).then(res => res.json());

		return {
			props: {}
		};
	}
</script>

<svelte:head>
	<title>薄荷网游加速器-专业游戏加速器延时低至毫秒，免费试用</title>
	<meta
		name="keywords"
		content="专线加速器,免费加速器,电竞加速器,游戏加速器,网游加速器,加速器下载,薄荷加速器"
	/>
	<meta
		name="description"
		content="【bohe】薄荷加速器是一款专业网络游戏加速工具，完美加速NBA2K21、彩虹六号、GTA5、糖豆人、绝地求生、使命召唤等上千款游戏，有效解决游戏中出现的延迟、丢包、卡顿等问题"
	/>
</svelte:head>

<section class="section-1">
	<img
		src="/img/index/block-title.png"
		alt="薄荷加速器，免费也可以是精品备份"
		width="870"
		height="56"
		class="mx-auto"
	/>
	<h3 class="mx-auto text-center text-white text-xl mt-32">
		多端支持 免费加速
	</h3>
	<div class="flex items-center justify-center mt-10">
		<button class="download-btn rounded py-4 px-8">立即免费使用</button>
	</div>
</section>

<section class="section-2 flex flex-col items-center justify-between">
	<div class="platforms flex gap-x-10 mt-10">
		<div
			class="platfrom shadow bg-white hover:shadow-lg cursor-pointer transition-shadow"
		/>
		<div
			class="platfrom shadow bg-white hover:shadow-lg cursor-pointer transition-shadow"
		/>
		<div
			class="platfrom shadow bg-white hover:shadow-lg cursor-pointer transition-shadow"
		/>
		<div
			class="platfrom shadow bg-white hover:shadow-lg cursor-pointer transition-shadow"
		/>
	</div>
	<div class="infos flex gap-x-10">
		<div
			class="info shadow bg-white hover:shadow-lg cursor-pointer transition-shadow"
		/>
		<div
			class="info shadow bg-white hover:shadow-lg cursor-pointer transition-shadow"
		/>
		<div
			class="info shadow bg-white hover:shadow-lg cursor-pointer transition-shadow"
		/>
		<div
			class="info shadow bg-white hover:shadow-lg cursor-pointer transition-shadow"
		/>
	</div>

	<div class="fragments flex mt-10 overflow-x-hidden">
		<div
			class="fragment flex-1 cursor-pointer relative flex flex-col justify-end p-10"
		>
			<img src="/img/index/game.png" alt="游戏" class="absolute inset-0" />
			<h3 class="title text-2xl text-green-500 mb-5">游戏</h3>
			<p class="desc text-white">
				PC游戏、平台游戏、主机游戏、手机游戏全部支持
			</p>
		</div>
		<div
			class="fragment flex-1 cursor-pointer relative flex flex-col justify-end p-10"
		>
			<img src="/img/index/music.png" alt="音乐" class="absolute inset-0" />
			<h3 class="title text-2xl text-green-500 mb-5">音乐</h3>
			<p class="desc text-white">网易云音乐、QQ音乐、酷狗音乐完美播放</p>
		</div>
		<div
			class="fragment flex-1 cursor-pointer relative flex flex-col justify-end p-10"
		>
			<img src="/img/index/website.png" alt="网页" class="absolute inset-0" />
			<h3 class="title text-2xl text-green-500 mb-5">网页</h3>
			<p class="desc text-white">
				支持海外用户贴吧、论坛、垂直社区回国加速服务
			</p>
		</div>
		<div
			class="fragment flex-1 cursor-pointer relative flex flex-col justify-end p-10"
		>
			<img src="/img/index/video.png" alt="视频" class="absolute inset-0" />
			<h3 class="title text-2xl text-green-500 mb-5">视频</h3>
			<p class="desc text-white">
				爱奇艺、优酷、腾讯视频全支持，随时随地嗨看欧洲杯
			</p>
		</div>
	</div>
</section>

<style lang="scss">
	section {
		&.section-1 {
			height: 509px;
			background: linear-gradient(
				to left,
				var(--bohe-primary) 0,
				var(--bohe-second) 100%
			);
			padding-top: 167px;

			button {
				background-color: #2b2d38;
				color: var(--bohe-primary);
				outline: 0;
				border-radius: 3px;
				box-shadow: 0px 0px 10px 4px rgba(157, 241, 229, 0.5);
				&:hover {
					box-shadow: 0px 0px 20px 5px rgba(157, 241, 229, 0.7);
				}
			}
		}

		&.section-2 {
			height: 1111px;

			.platfrom {
				width: 200px;
				height: 60px;
				border-radius: 3px;
			}

			.info {
				width: 270px;
				height: 300px;
				border-radius: 5px;
			}

			.fragment {
				width: 480px;
				height: 600px;
				img {
					z-index: -1;
				}
			}
		}
	}
</style>
