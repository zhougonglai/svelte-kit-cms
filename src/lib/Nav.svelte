<script>
	export let section;
</script>

<header class="bg-black text-white flex justify-center">
	<nav class="flex">
		<img alt="logo" src="/img/logo.png" class="logo self-center" />

		<ul class="nav-list flex justify-between">
			<li class="text-center">
				<a
					sveltekit:prefetch
					href="/"
					class:selected={section === ''}
					class="block opacity-70 hover:opacity-100"
				>
					首页
				</a>
			</li>
			<li class="text-center">
				<a
					sveltekit:prefetch
					href="/activitys/"
					class:selected={section === 'activitys'}
					class="block opacity-70 hover:opacity-100"
				>
					热门活动
				</a>
			</li>
			<li class="text-center">
				<a
					sveltekit:prefetch
					href="/notice/"
					class:selected={section === 'notice'}
					class="block opacity-70 hover:opacity-100"
				>
					官方公告
				</a>
			</li>
			<li class="text-center">
				<a
					sveltekit:prefetch
					href="/support"
					class:selected={section === 'support'}
					class="block opacity-70 hover:opacity-100"
				>
					游戏支持
				</a>
			</li>
			<li class="text-center">
				<a
					sveltekit:prefetch
					href="/news/"
					class:selected={section === 'news'}
					class="block opacity-70 hover:opacity-100"
				>
					资讯
				</a>
			</li>
			<li class="text-center">
				<a
					sveltekit:prefetch
					href="/about"
					class:selected={section === 'about'}
					class="block opacity-70 hover:opacity-100"
				>
					关于BOHE
				</a>
			</li>
		</ul>

		<div class="inline-flex flex-1 justify-end">
			<button class="w-40">登录</button>
		</div>
	</nav>
</header>

<style lang="scss">
	nav {
		height: 100px;
		width: 1200px;
		line-height: 100px;

		.flex {
			width: 1200px;
		}

		.logo {
			width: 152px;
			height: 45px;
		}

		ul.nav-list {
			flex-basis: 500px;

			a {
				position: relative;
				width: 100px;
				&.selected {
					opacity: 1;
					&:before {
						content: '';
						position: absolute;
						background: linear-gradient(
							180deg,
							var(--bohe-primary) 0%,
							var(--bohe-second) 100%
						);
						height: 10px;
						top: 0;
						left: 0;
						right: 0;
					}
				}
			}
		}
	}
</style>
